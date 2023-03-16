# LArSoft Guide
###### tags: `fermilab` `larsoft` `computing` `microboone` `icarus` `sbnd`

* [Generic Steps](#Generic-Steps)
* [FHiCL Files](#FHiCL-Files)
* [SBNSoftware](#SBNSoftware)
* [Problems](#Problems)


`config_dumper <file_name>` to see FHiCL configuration files for generating the sample

`samweb get-metadata <artROOT_file_name>`

Textfilegen, GENIE inputs for event generation.

[LAr Properties](https://lar.bnl.gov/properties/#basic-prop)

## Generic Steps
0. All in one example [Ref](https://microboone-docdb.fnal.gov/cgi-bin/sso/RetrieveFile?docid=37799&filename=An%20Introduction%20to%20LArSoft%20and%20uboonecode.pdf&version=1):
    ```bash
    source /cvmfs/uboone.opensciencegrid.org/products/setup_uboone_mcc9.sh
    ups list uboonecode -aK+
	setup uboonecode v08_00_00_61 -q e17:prof
	ups active
	cd /uboone/app/users/<username>/LarsoftTutorial
	mkdir uboonecode_v08_00_00_61
	cd uboonecode_v08_00_00_61
	mrb newDev
	source localProducts*/setup
	cd srcs
	mrb g -t v08_00_00_61 ubana
	cd $MRB_BUILDDIR
	mrbsetenv
	mrb i -j4
	mrbslp
    ```

The breakdown:
1. Install `setup` command:

    `source /grid/fermiapp/products/uboone/setup_uboone_mcc9.sh`
    
2. Setup products([Useful Checks](#Useful-Checks)):

    `setup <product_name> <version> -q <qualifier>`

    example: `setup uboonecode v08_00_00_55 -q e17:prof`
    
3. Create a working directory and make environments:

    ```
    mkdir <NAME_of_product_version>
    cd <NAME_of_product_version>
    mrb newDev
    source localProducts*/setup #Setup alias, e.g. MRB_BUILDDIR, MRB_PROJECT, MRB_SOURCE ...
    ```
    
    
4. Add package in `srcs/` directory
    
    `mrb g -t <TAG> <package name> `
    Without `-t` tag, we take the default version
    example tag is `v08_00_00_55`

5. Compile the code

    ```
    cd $MRB_BUILDDIR
    mrbsetenv
    mrb i -j4
    mrbslp
    ```
    


### Setup for uboonecode
[Quick Starter](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Uboone_guide)

1. Initialize environment
```
source /grid/fermiapp/products/uboone/setup_uboone.sh
setup uboonecode <version> -q <qualifiers>
```
2. Create a directory to store the code
`mkdir <new_directory> && cd <new_directory>`

3. Set local alias
```
mrb newDev
# If you want to specify version use the following
mrb newDev -v <version> -q <qualifiers>
source localProducts*/setup
```
4. Get the actual software under `srcs/` directory
```
cd srcs
mrb g <package name> 
# or try this line
mrb gitCheckout -t <version> <package name>
```
Use `ups active | grep -i "[product name or version]"` to find out what current version of package is being used for the current uboonecode.

6. Compile the local version:
```
mrbsetenv
mrb i -j4
```

a quick install using `make install -j4`
7. The code now can be called via `lar -c <FHiCL name>.fcl`; find the `job/` directory for FHiCL file!

### See code version?
Check `/cvmfs/sbnd.opensciencegrid.org/products/sbnd/sbndcode`
for sbndcode

### Manager MRB products
[Tutorial (2015)](https://indico.fnal.gov/event/9928/sessions/12914/attachments/75526/90595/lecture2.pdf)

`mrb -h` to get the manual

Alias:
|Symbol|meaning|
|---|---|
|$MRB_BUILDDIR|`build*` directory|
|$MRB_SOURCE|`src` directory|

#### Add package under the path
after `mrb gitCheckout -t <version> <package name>`, use `mrb uc` to update the `CMakeLists.txt`

### Manager UPS products
Enable a product
`setup <product_name> <version>`

Disable a product
`unsetup <product_name>`


### Useful Checks
See what versions of a package are available
`ups list -aK+ <package_name>`

Check what version of package is used in the current product 
`ups active | grep -i "[package name or version]"` 


## Code reference
- [LArSoft Github](https://github.com/LArSoft)
- [LArSoft Documentation](https://nusoft.fnal.gov/larsoft/doxsvn/html/annotated.html)
- [MicroBooNE Analysis ](https://cdcvs.fnal.gov/redmine/projects/ubana/repository)(see upper right corner of the page for more)
- [MicroBooNE Simulations](https://cdcvs.fnal.gov/redmine/projects/ubsim/repository)


### Server structures
Can find ICARUS setup here: `/cvmfs/icarus.opensciencegrid.org/products/icarus`

## Alias
`$FW_SEARCH_PATH` - file search path.
`$FHICL_FILE_PATH` - FHiCL search path.

## FHiCL Files
cppcheck
valgrind


[uboone guide](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Guide_to_Using_FCL_files_in_MicroBooNE)
[sbnd guide](https://cdcvs.fnal.gov/redmine/projects/sbndcode/wiki/Job_configurations)

### Structure
- `process_name` defines a unique name of the job
- `services` defines the general configuration
- `source` defines the input file
- `outputs` defines the output file
- `physics` defines the module in-used
    - producers
    - filters
    - analyzers
- optional: `BEGIN_PROLOG/END_PROLOG` defines alias
- redefine variables (example): `physics.producers.eventweight.genie_module_label: flux`





#### Locations of sample FHiCL files
- **uboone**: `/cvmfs/uboone.opensciencegrid.org/products/uboonecode/v08_00_00_55/job/`
- **sbnd**: `/cvmfs/sbnd.opensciencegrid.org/products/sbnd/sbndcode/v09_48_01/fcl`

`$FW_SEARCH_PATH` contains all possible paths of FHiCL files

`$FHICL_FILE_PATH` is the location of shared FHiCL files:


#### Dumpper
Check what you can dump here: `/cvmfs/larsoft.opensciencegrid.org/products/lardata/v08_02_00_12/job`

To show all information included in a FHiCL file:

`fhicl-dump <filename>.fcl`

`eventdump.fcl` print out what is inside a art-root:
`lar -c eventdump.fcl <name>.root`

Print out [MCTruth](https://github.com/LArSoft/larsim/tree/develop/larsim/MCDumpers) information under the product type `std::vector<simb::MCTruth>`:

`lar -c dump_mctruth.fcl -s <name>.root`

`lar -c dump_mcparticles.fcl -s <name>.root`


output will be saved in a `.log` file

---
### Specific Task

#### Event Generation
Generate events using the command
`lar -n <#events> -c <name>.fcl`

#### Weight Events

Weight events using 
`lar -c <name>.fcl <inputroot>.root`




---
## SBNSoftware
[SBNwiki](https://sbnsoftware.github.io/)

### Sbncode usage
The core CAFMaker FHiCL file now locates in sbncode:
`sbndcode/sbndcode/JobConfigurations/standard/caf/cafmakerjob_sbnd.fcl`




## artROOTs

Check producer names of a artROOT file:
```
rootstat.py <artroot_file_name>
```


## Event Productions
For sbnd, the event production chain goes as:
```
prodoverlay_corsika_cosmics_proton_genie_fullosc_spill_gsimple-configh-v1_tpc.fcl
g4_sce.fcl
detsim_sce.fcl
reco1_sce.fcl
reco2_sce.fcl
cafmakerjob_sbnd_sce_genie_and_fluxwgt.fcl
```

## Tools
artROOT dumpper, a TreeReader at ubana is available to do so:
`https://cdcvs.fnal.gov/redmine/projects/ubana/repository/revisions/master/show/ubana/TreeReader`

### Gallery Event Display
`source /sbnd/app/users/mdeltutt/static_evd/setup.sh`

`evd.py -s <path to artROOT files>`
Note: `-s` for SBND, `-i` for ICARUS


### Pandora Event Display
[See this workshop](https://indico.ph.ed.ac.uk/event/91/timetable/#20211102.detailed)



## Make PeLEE ntuples

[Tutorial page](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/Searchingfornues_ntuples)



## Problems

### Can't find fhicl file
If a file is in your module, but the job said it is not found. 

- Make sure it is also found in your `localProducts*`.
- Make sure you have run `mrb uc` at `/src` directory to properly add the customized module.
- Then recompile & make tar.


### Can't find alias directory
Can't find `$MRB_SOURCE` & no output from `source local*/setup`?

Try use `setup ninja v1_8_2` after setting up uboonecode

### From `mrbsetenv` in `build*/` directory
```
----------- check this block for errors -----------------------
ERROR: 
ERROR: directories not specified
ERROR: USAGE: setup_products <input-directory> <build-directory>
ERROR: 
----------------------------------------------------------------
```
Solution:`source local*/setup`

```
ERROR: Version conflict
```
Solution: Update `src/<package name>/ups/product_deps`
or you can use `unsetup <conflicted tool>`?


### mrb version errors

drinkingkazu  11:04
Hi all!  Below is a message I shared in sbn. might be useful/relevant here (uboone) unless fix is already put in place.

I just ran into an issue building my local software (not important but icaruscode sbncode larana if you wonder) using mrb on gpvm/build machine. Basically, the same installation that was working till a few hours ago stopped working, and I get a strange message upon setting up the area:
```
ERROR:
ERROR: this 
area expects mrb < v5_00_00 (found v5_18_01)!
ERROR:
```
If you get this message, you might be in the same boat.
QUICK SOLUTION
If you just want a solution, try doing this:
```
unsetup mrb
setup mrb -o
```
... then your routine commands to setup your local installation. Hope that solves it for you.

**WHAT'S GOING ON?**

So if you care learning why... what I think happening is that mrb default version that is set up when you `source /cvmfs/icarus.opensciencegrid.org/products/icarus/setup_icarus.sh` may have changed.
As the error message says, mine is now indeed `v5_18_01` and this is set by sourcing that script.
Just for fun, I pulled `larsoft` version `v09_29_00` and tried to build w/ `icaruscode` and/or `larana`. Didn't work. The issue is `srcs/CMakeLists.txt` that is produced by `mrb` not going well w/ our now-"old" structured `CMakeLists.txt` in software repositories.

A solution is either:
- Downgrade your mrb version to one of v4 variants and you can continue using your existing local installations OR pull and setup a new local installation (this is what 2 lines of commands above unsetup mrb; setup mrb -o does, -o for setting up an "older" version). NOTE this works with larsoft up to version v09_29_00. I don't think it works with v09_31_00 which presumably migrated to a newer version of mrb
- ... alternatively enforce this in experiment setup script (icarus one above)
- Update CMakeLists.txt (and possibly more, like ups/product_deps, but not sure) in software repos so that it works with the latest mrb


### Add a new package in `src/` and make them linked

