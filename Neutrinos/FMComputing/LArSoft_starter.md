# LArSoft

* [First Step](#First-Step)
* [FHiCL Files](#FHiCL-Files)
* [SBNSoftware](#SBNSoftware)
* [Problems](#Problems)

## First Step
[Quick Starter](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Uboone_guide)

1. Initialize environment
```
source /grid/fermiapp/products/uboone/setup_uboone.sh
setup uboonecode <version> -q <qualifiers>
```
2. Create a directory to store the code
`mkdir <new_directory> && cd <new_directory>`
4. Set local alias
```
mrb newDev
# If you want to specify version use the following
mrb newDev -v <version> -q <qualifiers>
source localProducts*/setup
```
5. Get the actual software under `srcs/` directory
```
cd srcs
mrb g <package name>
# or try this line
mrb gitCheckout -t <version> <package name>
```
6. Compile the local version:
```
mrbsetenv
mrb i -j4
```
7. The code now can be called via `lar -c <FHiCL name>.fcl`; find the `job/` directory for FHiCL file!

### Add package under the path
after `mrb gitCheckout -t <version> <package name>`, use `mrb uc` to update the `CMakeLists.txt`

### Useful Checks
See what versions are available
`ups list -aK+ <uboonecode/sbndcode>`

See what is active
`ups active`

## FHiCL Files
Fermilab Hierarchical Configuration Language (FHiCL) files

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

#### Useful commands
Alias of location of shared FHiCL files:
`$FHICL_FILE_PATH`

To show all information included in a FHiCL file:
`fhicl-dump <filename>.fcl`

#### Locations of sample FHiCL files
- uboone: `/cvmfs/uboone.opensciencegrid.org/products/uboonecode/v08_00_00_55/job/`
- sbnd: `/cvmfs/sbnd.opensciencegrid.org/products/sbnd/sbndcode/v09_24_00/fcl/`

*`$FW_SEARCH_PATH` contains all possible paths of FHiCL files*
#### Dumpper

Print out what is inside a art-root:
`lar -c eventdump.fcl <name>.root`


---
### Specific Task

#### Event Generation
Generate events using the command
`lar -n <#events> -c <name>.fcl`

#### Weight Events

Weight events using
`lar -c <name>.fcl <inputroot>.root`


## Using Grid to submit jobs
[Grid](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Tutorial_for_Analyzers_and_Using_the_Gird)

You need:
- XML for configuration `*.xml`
- Your version of code in a tarball `*.tar`
    - Build your code and use `make_tar_uboone.sh` local.tar
    - (at sbnd) use `make_tar_sbnd.sh <output.tar.gz>`
- List of input roots `*.txt`

### Online Monitor
[My Profile](https://fifemon.fnal.gov/monitor/d/000000116/user-batch-details?orgId=1&var-cluster=fifebatch&var-user=klin)

### Commands
Submit a job

If a job is held, check [this](https://fifemon.fnal.gov/monitor/d/000000146/why-are-my-jobs-held?orgId=1&var-user=klin) may help.

`project.py --xml fluxreader_mcc9.xml --stage flux --submit`


Check status
`jobsub_q --user=klin`

Remove job with ID
`jobsub_rm --jobid=<id>`

Get logs
`jobsub_fetchlog --jobid <cluster ID#>@<host address>`

Example: `jobsub_fetchlog --jobid 47928378@jobsub02.fnal.gov`

---
## SBNSoftware
[SBNwiki](https://sbnsoftware.github.io/)


## Problems

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
