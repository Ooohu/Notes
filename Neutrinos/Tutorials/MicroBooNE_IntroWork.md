# The MicroBooNE Experiment

###### tags: `fermilab` `microboone`

Topics cover
* [About the Detector](#🐋About-the-Detector)
* [Triggers](#🐤Triggers)
* [Resources](#🐤Resources)
* [Address Book](#🐤Address)
* [Analysis Tools](#🐋Analysis-Tools)
* [Pandora Ntuples](#🐤Pandora-Ntuples)

Quick link to apps
* [Grid](#🐤Grid)
* [Samweb](#🐤Samweb)

## RANDOM NOTES

Temporary treatment of a broken jobsub_lite:
```
unsetup jobsub_client v_lite
setup jobsub_client v1_3_5
```


Statistical error dominated scnario makes the smearing matrix more diagonal-symmetric-like.

EXT behaves the same across runs; Beam behaves differently, when the beam intensity changes.
EXT/neutrino ratio may change for each POT during runs.


### Dumpper
Check what you can dump here: `/cvmfs/larsoft.opensciencegrid.org/products/lardata/v08_02_00_12/job`

To show all information included in a FHiCL file:

`fhicl-dump <filename>.fcl`

`eventdump.fcl` print out what is inside a art-root:
`lar -c eventdump.fcl <name>.root`

Print out [MCTruth](https://github.com/LArSoft/larsim/tree/develop/larsim/MCDumpers) information under the product type `std::vector<simb::MCTruth>`:

`lar -c dump_mctruth.fcl -s <name>.root`

`lar -c dump_mcparticles.fcl -s <name>.root`

output will be saved in a `.log` file

[Reference](https://internal.dunescience.org/doxygen/classlarg4_1_1ParticleListActionService.html) of end process:
- conv
- LowEnConversion
- Pair - pair production
- compt - compton scattering
- Compt 
- Brem - bremstrahlung
- phot - photoelectric effect
- Photo
- Ion - ionization
- annihil - annihilation

### Validation plan?
Remove cosmic statistically, i.e. data - EXT

numu inclusive selection
CC 1 pi0 selection


## 🐋About the Detector
[MicroBooNE Proposal (2007)](https://lss.fnal.gov/archive/test-proposal/0000/fermilab-proposal-0974.pdf)
[MicroBooNE design (2017)](https://arxiv.org/abs/1612.05824)

Features of MicroBooNE:
- Small detector reduce misid events with higher signal to noise ratio compared to MiniBooNE.
- The development of ICARUS allows MicroBooNE to build fast, cost less, and deliver physics qucily.
- Cold electronics demonstrate "low noise electronics", allowing a large sample of neutrino teractions.


### Readouts
FPGA chooses what data to store after triggers.

Data acquisition system (DAQ)

Readout Board

What is light-yield?

### Beams



Spills - when the beam is on, protons are shot at ?? frequency. Each spill is the time protons are shot to the target; and there are pulse between spills, such that we can record external data as comsic background.

Triggers - triggers tell the detector when to start taking data.

How Runs are defined?

Swizzled data?



### 🐤Triggers
[HNL internal note (2019)](MicroBooNE-doc-25427-v3)

Triggers are used to determine when to take data to avoid events without beam induced signals.

- Hardware triggers are issued by the accelerator(BNB or NuMI) indicating whenever a neutrino spill is approaching the detector.
- Software triggers are from the detector. They are appled on events passing the hardware triggers. PMT output information, the amount of light and the number of PMTs have detected light, determines when to start taking data.


Level-1 trigger - accelerator gate & random trigger (for cosmic)

Level-2 trigger - software trigger using PMT information

HW trigger - trigger counts from events


```mermaid
graph LR
A[On-beam]-->B[Trigger];
B[Off-beam]
```


## 🐤Resoruces
For at work site:
```
usname:uboone
pswd:$uBneutrino!
```
Financial resources:
- Neutrino Physics Center Fellowships
- Intensity Frontier Fellowships
- URA - Visiting scholars Program

Learning resources:
- International neutrino Summer School 
- Fermilab Colloquia
- Wine & CHeese seminars


## 🐤Address

- uboone FHiCL files location:
`/cvmfs/uboone.opensciencegrid.org/products/uboonecode/v08_00_00_64/job/` 
- generator script:
`/cvmfs/uboone.opensciencegrid.org/products/uboonecode/v08_00_00_64/slf7.x86_64.e17.prof/bin/`
- Home directory:
`/nashome/k/$USER`
- Scratch:
`/pnfs/uboone/scratch/users/$USER`
- Persistent:
`/pnfs/uboone/persistent/users/$USER`


## 🐤Grid
NOW USE TOKENS, click the prompted website for authentication.

To use grid ([tutorial](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Tutorial_for_Analyzers_and_Using_the_Gird)), you need:
- XML for configuration `*.xml`
- Your version of code in a tarball `*.tar`
    - Build your code and use `make_tar_uboone.sh local.tar`
    - (at sbnd) use `make_tar_sbnd.sh <output.tar.gz>`
- List of input roots `*.txt` 

To submit a job:
`project.py --xml fluxreader_mcc9.xml --stage flux --submit`

[How to run overlay job](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/How_to_run_overlay_jobs_with_filtered_events_at_generation)

[Production work flow](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/MCC9_Production_Fhicls)

[NuMI work flow](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/NuMI_Production_fcls)

#### Online Monitor
A useful online grid monitor: [The fifemon](https://fifemon.fnal.gov/monitor/d/000000116/user-batch-details?orgId=1&var-cluster=fifebatch&var-user=klin)

Job summary at the [dag page](https://fifemon.fnal.gov/monitor/d/000000188/dag-cluster-summary?orgId=1)

For [held](https://fifemon.fnal.gov/monitor/d/000000146/why-are-my-jobs-held?orgId=1&var-user=klin) jobs.

Emails from `fife-support@fnal.gov` also provide links to summary of finished jobs.

Can get to the same page following 
`fifemon-->AG Cluster Summary [bottom right]`, and type the `JOBSUBJOBID`

#### Local job management
- `jobsub_release --jobid=<id@server.fnal.gov>` relese a job from held
- `jobsub_q --user=klin` check status 
- `jobsub_rm klin` remove my jobs 
- `jobsub_fetchlog --jobid <Cluster ID>@<server>` get logs of a job 

To run multiple stages, need to use the `check` to get  `files.list` in the `book` directory to pass files to different stages:
```
project.py --xml <xml> --stage <stage1> --submit
project.py --xml <xml> --stage <stage1> --check 
project.py --xml <xml> --stage <stage2> --submit
```

To fix partially failed jobs, tune the xml and run the `makeup` option:
```
project.py --xml <xml> --stage <stage1> --submit
project.py --xml <xml> --stage <stage1> --check 
project.py --xml <xml> --stage <stage1> --makeup
```

For ntuples, use the following check commands instead:
`project.py --xml <xml> --stage <stage1> --checkana`

##### XML Elements for `project.py`
[POMS production project reference](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Best_practices_for_configuring_POMS_production_projects#About-copying-and-streaming)

XML grammar :`<elemnt>value</elemnt>`

|XML Elements| Values| 
|---|---|
|`<resource>`| Nodes to run the job <ul><li> `DEDICATED` uBooNE specific nodes </li> <li> `OPPORTUNISTIC` Fermi-shared nodes </li> <li> `OFFSITE` non-Fermi machines</li> </ul>|Nodes to run the job|
|`<initsource> `| local path of a bash script|
|`<initscript> ` | local path of a bash script|
|`<datatieer`| file types declared to SAM |
|`<schema>`|[Tools](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Xrootdtips) to copy files <ul><li>`gsiftp` copy file using `gridftp` (for non-root files)</li> <li>`root` remotely access files without copying</li> </ul>|
|`<jobsub>` | additional commands for the `jobsub` client|

Specific commands for `jobsub` client under element:
|Argument|Attributes|Meaning|
|---|---|---|
|`--expected-lifetime=<attribute>`|`short`/`medium`/`long`/`1h`/`8h`, etc.| Run time of the job before it got cancel.|


## 🐤Samweb
[SAM wiki](https://cdcvs.fnal.gov/redmine/projects/uboonecode/wiki/Sam)

[SAM tutorial](https://microboone-docdb.fnal.gov/cgi-bin/sso/ShowDocument?docid=20557)


`<sam_def>` can be found in production websites:
- [MicroBooNE Production](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/Mcc9)
    - [BNB Samples](https://microboone-exp.fnal.gov/at_work/AnalysisTools/mc/mcc9.0/details_v13.html)
    - [NuMI Samples](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/NuMI_Samples)
- [SBNWiki Production](https://sbnsoftware.github.io/sbn/sbnprod_wiki/sample)


`samweb list-files --summary defname:<sam_def>` gives overview of samples.

`samweb list-files defname:<sam_def>` gives list of files under sam_def

`samweb locate-file <file_name_form_list-files>` locates the file directory

`samweb get-metadata my_filename.root` gives the metadata of a root file


Get events by event number:
`samweb list-files defname:<samdef> and run_number=<run>.<subrun>`

[MicroBooNE NuMI Production chain](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/MCC9_Production_Fhicls)

#### Prestaging files
Check if a `file` at `<dirctory>` is on tape or staged to disk:

`cat <directory>".(get)(<filename>)(locality)"`:
- `ONLINE_AND_NEARLINE` means the file is on tape and staged to disk.
- `ONLINE` means the file is available, but it is not stored to tape.
- `NEARLINE` means the file is on tape, and it needs to be staged
    to stage the file
    ```
    kx509
    samweb prestage-dataset --defname=<your_dataset_name_here>
    ```

`samweb prestage-dataset --defname=my_def_name` prestage files to be used


### Problems
Prompt:`SSL error: [SSL: SSLV3_ALERT_CERTIFICATE_EXPIRED] sslv3 alert certificate expired (_ssl.c:877)`
Solution: type `kx509`

---



## 🐋Analysis Tools
- [Pandora Software Development Kit (SDK)](https://arxiv.org/abs/1708.03135)
  Focus on pattern-recognition (shower or track) based on 2D clustering of hits. Multiple algorithms applied for multiple purposes. 

- [WireCell imaging](https://arxiv.org/abs/2110.13961)
  Use the charge and sparsity information along with the time and geometry to reconstruct 3d events.

- [CNN](https://arxiv.org/abs/2010.08653)
  Convolution Neutral Network (CNN) assign probabilities of particle identities of each single detected particles.

### Reconstruction from Hits
> Track is track, but shower sometimes looks like tracks too?

#### Pandora Approach
[Pandora Source Code](https://github.com/PandoraPFA)
Pandora first tags comsic muon to distinguish cosmic (long track objects) from neutrino candidate events (include tracks & showers); then the rest of hits were further reconstructed as tracks and showers:

![Multi-algorithm Reconstruciton Path](https://i.imgur.com/wvyPtsL.png)


#### WireCell Approach
[Wire-Cell 3D imaging](https://arxiv.org/pdf/2011.01375) is built based on time, geometry, and charge information. Along different time slices (each is 2$\mu$s long), more than dozens of 1d projection views were used via *tiling* and *charge solving* to recover a loss of information, which comes from the use of wire plances instead of pixelated readout.

1. Tiling is to merge consecutive hit cells (cells with hit infomation) from a time slice. An example of a cell is the black trangle shown in the picture, where the black lines are imaginary boundries between wires. Each blue dot labels a hit cell, and all together sharing the blue boundary as a blob. A blob can be formed via 2-plane tiling or 3-plane tiling.
![](https://i.imgur.com/sCynP6l.png)
2. Charge solving is to remove blobs with no physical meaning. This process can recover loss information from a cell with information coming from 2 of 3 wires, as well as removing unwanted signals from problematic wires.

With additional clustering and charge-light matching processes, wire-cell imaging provide inputs for neutrino interaction identifications via two parts: 1. reconstruct vertex through 3D imaging and deep neural network (DNN); 2. reconstruct the particle flow tree.
![](https://i.imgur.com/A8lBnjF.png)


#### CNN Approach
Use U-ResNet (U-Net and residual network) to analyze pixels of images. Inter-pixel correlation to identify neutrino interactions at a vertex.

Q: No backward projection of photon showers, right?


##### Web Sites (Useful?)
[Analysis Tools](https://microboone-exp.fnal.gov/at_work/AnalysisTools/)

[Run4 Validation](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/Run4_Validation)


#### BeamWindow configuration
Listed at [NuMI Wiki](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/NuMI_Documentation#How-to-do-NuMI-POT-counting)
Can also find them using: `config_dumper <artROOT_FILE> | grep BeamWindow`

| |`BeamWindowStartTime` | `BeamWindowEndTime`|
|---|---|---|
|BNB Data| 3.19 | 4.87|
|BNB EXT | 3.57 | 5.25|
|NuMI Data| 3.2 | 4.8 |
|NuMI EXT| 6 | 15.8 |

#### NuMI special
[NuMI Flux Study (2021)](https://microboone-docdb.fnal.gov/cgi-bin/sso/RetrieveFile?docid=32401&filename=MCC9_Nue_Cross_Section_Internal_Notev2.8.pdf&version=23)

[RHC/RHC data @ NuMI MicroBooNE-doc-32600-v1](https://microboone-docdb.fnal.gov/cgi-bin/sso/ShowDocument?docid=32600) 
FHC - Front horn current (+200 kA), this gives higher neutrino flux. 
RHC - Rear horn current (-200 kA), this gives higher anti-neutrino flux. 

Prediction of flux:
|Mode|$\nu_\mu$|$\bar{\nu}_\mu$|$\nu_e$|$\bar{\nu}_e$|
|---|---|---|---|---|
|FHC|51.1%|33.4%|14.2%|1.3%|
|RHC|42.2%|43.9%|11.7%|2.3%|


#### Configurations
0+6
4+6
6+6

|Beam | Runs | POT|
|---|---|---|
|NuMI FHC| Run1 |2e20 |
|NuMI RHC| Run3 |5.014e20 |
|NuMI RHC| Run4a |8.3e18 |




##### NuMI POT Scaling
POT Scaling @ [NuMI Wiki](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/NuMI_Documentation#How-to-do-NuMI-POT-counting)

[Marco's normalization guide](https://microboone-docdb.fnal.gov/cgi-bin/sso/RetrieveFile?docid=15204&filename=normalisation_v2.0.0.pdf&version=2)

Read Trigger/POT information using SAM definition:
- BNB: `/uboone/app/users/zarko/getDataInfo.py -v2 -d <SAM_DEF>`
- NuMI: `/uboone/app/users/guzowski/slip_stacking/getDataInfo.py -v4 --format-numi --prescale --horncurr -d <SAM_DEF>`

or use run list, in case you have an ntuple:
- NuMI: `/uboone/app/users/zarko/getDataInfo.py -v3 --format-numi --prescale --run-subrun-list run_subrun_list.txt`
where `run_subrun_list.txt` contains `run# subrun#` should look like

``` 
1245 22
1255 2
```


$data POT = tortgt\_wcut$

$EXTPOT = tortgt\_wcut*\dfrac{EA9CNT\_wcut}{EXT\_NUMIwin\_FEMBeamTriggerAlgo}$

Example:
```!
$ /uboone/app/users/zarko/getDataInfo.py -v3 --format-numi --prescale -d run4a_numi_beam_on_pandora_reco2_v08_00_00_63_run4a_reco2_beam_good
Definition run4a_numi_beam_on_pandora_reco2_v08_00_00_63_run4a_reco2_beam_good contains 217 files
           EXT         Gate1        EA9CNT        tor101        tortgt   EA9CNT_wcut   tor101_wcut   tortgt_wcut
     7910853.0      372484.0      380931.0     8.914e+18     8.883e+18      333194.0     8.347e+18      8.32e+18
Warning!! NuMI data for some of the requsted runs/subruns is not in the database.
2 runs missing NuMI data (number of subruns missing the data): 19600 (37),19700 (1),

	EXT_unbiased_PrescaleAlgo                          158217.060000
	NUMI_unbiased_PrescaleAlgo                         5959.744000
	EXT_HSN_c0_FEMBeamTriggerAlgo                      1582170.600000
	EXT_BNBwin_2017Dec_SWTrigger5PE_FEMBeamTriggerAlgo 7910853.000000
	EXT_NUMIwin_FEMBeamTriggerAlgo                     1384399.275000
	NUMI_2018May_FEMBeamTriggerAlgo                    372484.000000
	EXT_NUMIwin_2018May_FEMBeamTriggerAlgo             1384399.275000
	NUMI_FEMBeamTriggerAlgo                            372484.000000
	EXT_BNBwin_FEMBeamTriggerAlgo                      7910853.000000
```
- `*_wcut` is the beam quality cut
- `tortgt` POT monitor at the target
- `EA9CNT` the number of HW triggers



### 🐤Pandora Ntuples
[Variable Cheat Sheet](https://docs.google.com/spreadsheets/d/1ic-eCVBsAWkp9RsxCpzXQglkNnIf7GwO5Uvl5FzM8G0/edit#gid=0)

#### gLEE
[SinglePhotonAnalysis Module](https://cdcvs.fnal.gov/redmine/projects/ubana/repository/show/ubana/SinglePhotonAnalysis?rev=UBOONE_SUITE_v08_00_00_64)
Data notes (Sep. 2021): MicroBooNE-doc-26979-v2
SinglePhoton (May 2021): MicroBooNE-doc-32837-v9


#### PeLEE

[Production XML](https://github.com/kvjmistry/NueXSec/tree/master/xml)

[Software Installation](https://cdcvs.fnal.gov/redmine/projects/uboone-physics-analysis/wiki/Searchingfornues_ntuples)

[searchingfornues Tool](https://github.com/ubneutrinos/searchingfornues)

[searchingfornues (NuMI version, before v08_00_00_65)](https://github.com/kvjmistry/searchingfornues/blob/numi_tag_022820/Selection/AnalysisTools/EventWeightTree_tool.cc#L160-L164)