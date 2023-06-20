[![GitHub Actions](https://github.com/bids-standard/bids-examples/workflows/validate_datasets/badge.svg)](https://github.com/bids-standard/bids-examples/actions)

The content of this repository can also be viewed here:

**https://bids-standard.github.io/bids-examples/**

# bids-examples

This repository contains a set of
[BIDS-compatible](https://bids.neuroimaging.io/) datasets with **empty raw data
files**. These datasets can be useful to:

1. write lightweight software tests
1. serve as an example on how a BIDS dataset can be structured

**ALL RAW DATA FILES IN THIS REPOSITORY ARE EMPTY!**

However for some of the data, the headers containing the metadata are still
intact. (For example the NIfTI headers for `.nii` files, the BrainVision data
headers for `.vhdr` files, or the OME-XML headers for `.ome.tif` files.)

Headers are intact for the following datasets:

- `synthetic`
- Most EEG or iEEG data in BrainVision format (e.g., `eeg_matchingpennies`)

## Validating BIDS examples

The next three sections mention a few details on how the `bids-examples` can be
validated using `bids-validator`.

For general information on the `bids-validator`, including installation and
usage, see the
[bids-validator README file](https://github.com/bids-standard/bids-validator#quickstart).

### Validating individual examples

Since all raw data files in this repository are empty, the `bids-validator` must
to be configured to not report empty data files as errors. (See more on
bids-validator configuration in the
[bids-validator README](https://github.com/bids-standard/bids-validator#configuration).)

Just run the validator as follows (using the `eeg_matchingpennies` dataset as an
example, and assuming you are in a command line at the root of the
`bids-examples` repository):

`bids-validator eeg_matchingpennies --config.ignore=99`

The `--config.ignore=99` "flag" tells the bids-validator to ignore empty data
files rather than to report the "empty file" error .

For datasets that contain NIfTI `.nii` files, you also need to add the
`ignoreNiftiHeaders` flag to the `bids-validator` call, to suppress the issue
that NIfTI headers are not found.

For example:

`bids-validator ds003 --config.ignore=99 --ignoreNiftiHeaders`

### Validating all examples

If you want to validate all examples in one go, you can use the `run_tests.sh`
script that is provided in this repository. This script makes use of the
`bidsconfig.json` configuration file for the `bids-validator`, and appropriately
handles some special case examples (see
[Validator Exceptions](#validator-exceptions)).

Simply run `bash run_tests.sh` in a command line from the root of the
`bids-examples` repository.

### Validator exceptions

Some datasets may include a custom `.bids-validator-config.json` to ignore
errors generated from idiosyncrasies of the datasets as they existed on
creation.

| name          | errors ignored                                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| genetics_ukbb | SliceTiming values for tasks is larger than given TR, EchoTime1 and EchoTime2 are not provided for any of the phasediff files. |

Other datasets may include a `.SKIP_VALIDATION` file, to skip the validation
with the continuous integration service. This is useful for datasets that
_cannot_ pass at the moment due to lack of coverage in the
[bids-validator](https://github.com/bids-standard/bids-validator).

Note however, that the `.SKIP_VALIDATION` file only impacts the continuous
integration service, or validation when run with the `run_tests.sh` script (see
[Validating all examples](#validating-all-examples)). This file does **not**
have any effect when running `bids-validator` from custom scripts, the web-based
validator, docker, or from the command line.

| name              | why skipped                                            |
| ----------------- | ------------------------------------------------------ |
| ds000001-fmriprep | lack of coverage for "derivatives" in `bids-validator` |

## Contributing

We are happy to receive contributions in the form of:

- updates to existing examples, or the [dataset index](#dataset-index)
- new examples
  - only if they cover aspects that are currently not covered by existing
    examples
  - only if a maintainer can be found for this dataset
- suggestions on how to improve the bids-examples repository

For more information, please see our
[CONTRIBUTING.md](./CONTRIBUTING.md)
file or open a
[new GitHub Issue](https://github.com/bids-standard/bids-examples/issues/new)
and ask us directly.

## Dataset index
<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->



### ASL

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name   | description                                                                                   | datatypes        | suffixes                                  | link to full data             | maintained by                            |
|:-------|:----------------------------------------------------------------------------------------------|:-----------------|:------------------------------------------|:------------------------------|:-----------------------------------------|
| asl001 | T1w, asl (GE, PCASL, 3D_SPIRAL), m0scan within timeseries                                     | anat, perf       | T1w, asl, aslcontext, asllabeling         | [link](https://osf.io/yru2q/) | [@patsycle](https://github.com/patsycle) |
| asl002 | T1w, asl (Philips, PCASL, 2D_EPI), m0scan as separate scan                                    | anat, perf       | T1w, asl, aslcontext, asllabeling, m0scan | [link](https://osf.io/yru2q/) | [@patsycle](https://github.com/patsycle) |
| asl003 | T1w, asl (Siemens, PASL, multiTI), M0scan as separate scan                                    | anat, perf       | T1w, asl, aslcontext, asllabeling, m0scan | [link](https://osf.io/yru2q/) | [@patsycle](https://github.com/patsycle) |
| asl004 | T1w, asl (Siemens, PCASL, multiPLD with pepolar), m0scan separate scans with pepolar appraoch | anat, fmap, perf | T1w, asl, aslcontext, asllabeling, m0scan | [link](https://osf.io/yru2q/) | [@patsycle](https://github.com/patsycle) |
| asl005 | T1w, asl (Siemens, PCASL, singleTI, 3D_GRASE), m0scan as separate scan                        | anat, perf       | T1w, asl, aslcontext, asllabeling, m0scan | [link](https://osf.io/yru2q/) | [@patsycle](https://github.com/patsycle) |

### EEG

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name                          | description                                                                                                        | datatypes   | suffixes                                       | link to full data                               | maintained by                                  |
|:------------------------------|:-------------------------------------------------------------------------------------------------------------------|:------------|:-----------------------------------------------|:------------------------------------------------|:-----------------------------------------------|
| eeg_cbm                       | Rest EEG. European Data Format (.edf)                                                                              | eeg         | channels, eeg, events, scans                   | n/a                                             | [@cpernet](https://github.com/cpernet)         |
| eeg_ds003645s_hed             | Shows usage of Hierarchical Event Descriptor (HED) in events files                                                 | eeg         | channels, eeg, events                          | [link](https://openneuro.org/datasets/ds003645) | [@VisLab](https://github.com/VisLab)           |
| eeg_ds003645s_hed_inheritance | HED annotation with multiple inherited sidecars                                                                    | eeg         | channels, eeg, events                          | [link](https://openneuro.org/datasets/ds003645) | [@VisLab](https://github.com/VisLab)           |
| eeg_ds003645s_hed_library     | HED annotation using HED library vocabularies (schema).                                                            | eeg         | channels, eeg, events                          | [link](https://openneuro.org/datasets/ds003645) | [@VisLab](https://github.com/VisLab)           |
| eeg_ds003645s_hed_longform    | HED annotation using tags in long form.                                                                            | eeg         | channels, eeg, events                          | [link](https://openneuro.org/datasets/ds003645) | [@VisLab](https://github.com/VisLab)           |
| eeg_face13                    | Deconstructing the early visual electrocortical response to face and house stimuli. EDF format                     | eeg         | channels, coordsystem, eeg, electrodes, events | n/a                                             | [@andesha](https://github.com/andesha)         |
| eeg_matchingpennies           | Offline data of BCI experiment decoding left vs. right hand movement. BrainVision data format (.eeg, .vhdr, .vmrk) | eeg         | channels, eeg, events                          | [link](https://doi.org/10.17605/OSF.IO/CJ2DR)   | [@sappelhoff](https://github.com/sappelhoff)   |
| eeg_rishikesh                 | Mind wandering experiment. EEG data in Biosemi (.bdf) format                                                       | eeg         | channels, eeg, events                          | [link](https://openneuro.org/datasets/ds001787) | [@arnodelorme](https://github.com/arnodelorme) |

### iEGG

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name                   | description                                                                                                    | datatypes              | suffixes                                                               | link to full data                                                           | maintained by                                |
|:-----------------------|:---------------------------------------------------------------------------------------------------------------|:-----------------------|:-----------------------------------------------------------------------|:----------------------------------------------------------------------------|:---------------------------------------------|
| ieeg_epilepsy          | multiple sessions, tutorial                                                                                    | anat, ieeg             | T1w, channels, coordsystem, electrodes, events, ieeg, scans            | [link](https://neuroimage.usc.edu/bst/getupdate.php?s=tutorial_epimap_bids) | [@ftadel](https://github.com/ftadel)         |
| ieeg_epilepsyNWB       | multiple sessions, tutorial — derivative dataset of `ieeg_epilepsy` showcasing the NWB file format alternative | anat, ieeg             | T1w, channels, coordsystem, electrodes, events, ieeg, scans            | [link](https://neuroimage.usc.edu/bst/getupdate.php?s=tutorial_epimap_bids) | [@TheChymera](https://github.com/TheChymera) |
| ieeg_epilepsy_ecog     | multiple sessions, tutorial                                                                                    | anat, ieeg             | T1w, channels, coordsystem, electrodes, events, ieeg, photo, scans     | [link](https://neuroimage.usc.edu/bst/getupdate.php?s=sample_ecog)          | [@ftadel](https://github.com/ftadel)         |
| ieeg_filtered_speech   | recordings of three seizures                                                                                   | ieeg                   | channels, coordsystem, electrodes, events, ieeg, photo                 | n/a                                                                         | [@choldgraf](https://github.com/choldgraf)   |
| ieeg_motorMiller2007   | Cue-based hand & tongue movement data                                                                          | ieeg                   | channels, coordsystem, electrodes, events, ieeg                        | n/a                                                                         | [@dorahermes](https://github.com/dorahermes) |
| ieeg_visual            | Stimulus dependence of gamma oscillations in human visual cortex                                               | anat, ieeg             | T1w, channels, coordsystem, electrodes, events, ieeg                   | n/a                                                                         | [@dorahermes](https://github.com/dorahermes) |
| ieeg_visual_multimodal | n/a                                                                                                            | anat, fmap, func, ieeg | T1w, bold, channels, coordsystem, electrodes, epi, events, ieeg, sbref | n/a                                                                         | [@irisgroen](https://github.com/irisgroen)   |

### MEG

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name     | description                                                                                                          | datatypes                       | suffixes                                                                                                                      | link to full data                                              | maintained by                              |
|:---------|:---------------------------------------------------------------------------------------------------------------------|:--------------------------------|:------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------|:-------------------------------------------|
| ds000117 | A multi-subject, multi-modal human neuroimaging dataset of 19 subjects on a MEG visual task                          | anat, beh, dwi, fmap, func, meg | T1w, beh, bold, channels, coordsystem, dwi, events, headshape, magnitude1, magnitude2, meg, phasediff, scans                  | [link](https://openneuro.org/datasets/ds000117/)               | [@RikHenson](https://github.com/RikHenson) |
| ds000246 | Auditory dataset used for Brainstorm’s general online tutorial                                                       | anat, meg                       | ChannelGroupSet, ClassFile, MarkerFile, T1w, channels, coordsystem, default, headshape, meg, params, photo, processing, scans | [link](https://openneuro.org/datasets/ds000246/versions/00001) | [@guiomar](https://github.com/guiomar)     |
| ds000247 | Five minutes, eyes-open, resting-state MEG data from 5 subjects. This is a sample from The Open MEG Archive (OMEGA). | anat, meg                       | ClassFile, T1w, bad, channels, coordsystem, default, headshape, meg, params, processing, scans                                | [link](https://openneuro.org/datasets/ds000247/versions/00001) | [@guiomar](https://github.com/guiomar)     |
| ds000248 | MNE sample data: Data with visual and auditory stimuli                                                               | anat, meg                       | FLASH, T1w, channels, coordsystem, events, meg, scans                                                                         | [link](https://openneuro.org/datasets/ds000248/versions/00001) | [@agramfort](https://github.com/agramfort) |

### Microscopy

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name         | description                                                                                     | datatypes   | suffixes                      | link to full data                              | maintained by                                |
|:-------------|:------------------------------------------------------------------------------------------------|:------------|:------------------------------|:-----------------------------------------------|:---------------------------------------------|
| micr_SEM     | Example SEM dataset in PNG format with 1 sample imaged over 2 sessions                          | micr        | SEM, photo, samples, sessions | [link](https://doi.org/10.5281/zenodo.5498378) | [@jcohenadad](https://github.com/jcohenadad) |
| micr_SEMzarr | Example SEM dataset in PNG and OME-ZARR format with 1 sample imaged over 2 sessions             | micr        | SEM, samples, sessions        | n/a                                            | [@TheChymera](https://github.com/TheChymera) |
| micr_SPIM    | Example SPIM dataset in OME-TIFF format with 2 samples from the same subject with 4 chunks each | micr        | SPIM, photo, samples          | [link](https://doi.org/10.5281/zenodo.5517223) | [@jcohenadad](https://github.com/jcohenadad) |

### Motion

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name                    | description                                                                                               | datatypes   | suffixes                                                      | link to full data                                       | maintained by                                    |
|:------------------------|:----------------------------------------------------------------------------------------------------------|:------------|:--------------------------------------------------------------|:--------------------------------------------------------|:-------------------------------------------------|
| motion_dualtask         | older and younger participants walking while performing discrimination task                               | eeg, motion | channels, eeg, events, motion, scans                          | n/a                                                     | [@sjeung](https://github.com/sjeung)             |
| motion_spotrotation     | participants rotated heading using full-body motion or joystick                                           | eeg, motion | channels, coordsystem, eeg, electrodes, events, motion, scans | [link](https://openneuro.org/datasets/ds004460)         | [@sjeung](https://github.com/sjeung)             |
| motion_systemvalidation | Example dataset of two different motion captured system recorded almost simultaneously, but no brain data | motion      | channels, motion, scans                                       | [link](https://doi.org/10.6084/m9.figshare.20238006.v2) | [@JuliusWelzel](https://github.com/JuliusWelzel) |

### MRI

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name                   | description                                                                                 | datatypes                       | suffixes                                                                                                     | link to full data                                              | maintained by                              |
|:-----------------------|:--------------------------------------------------------------------------------------------|:--------------------------------|:-------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------|:-------------------------------------------|
| 7t_trt                 | n/a                                                                                         | anat, fmap, func                | T1map, T1w, bold, magnitude1, magnitude2, phasediff, physio, scans, sessions                                 | [link](https://bit.ly/2H0Z6Qt)                                 | n/a                                        |
| ds000117               | A multi-subject, multi-modal human neuroimaging dataset of 19 subjects on a MEG visual task | anat, beh, dwi, fmap, func, meg | T1w, beh, bold, channels, coordsystem, dwi, events, headshape, magnitude1, magnitude2, meg, phasediff, scans | [link](https://openneuro.org/datasets/ds000117/)               | [@RikHenson](https://github.com/RikHenson) |
| ds001                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000001/versions/00006) | n/a                                        |
| ds002                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000002/versions/00002) | n/a                                        |
| ds003                  | single task, single run                                                                     | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000003/versions/00001) | n/a                                        |
| ds005                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000005/versions/00001) | n/a                                        |
| ds006                  | single task, multiple sessions, multiple runs                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000006/versions/00001) | n/a                                        |
| ds007                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000007/versions/00001) | n/a                                        |
| ds008                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000008/versions/00001) | n/a                                        |
| ds009                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2, scans                                                                          | [link](https://openneuro.org/datasets/ds000009/versions/00002) | n/a                                        |
| ds011                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000011/versions/00001) | n/a                                        |
| ds051                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000051/versions/00001) | n/a                                        |
| ds052                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000052/versions/00001) | n/a                                        |
| ds101                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events                                                                                            | [link](https://openneuro.org/datasets/ds000101/versions/00004) | n/a                                        |
| ds102                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events                                                                                            | [link](https://openneuro.org/datasets/ds000102/versions/00001) | n/a                                        |
| ds105                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events                                                                                            | [link](https://openneuro.org/datasets/ds000105/versions/00001) | n/a                                        |
| ds107                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events                                                                                            | [link](https://openneuro.org/datasets/ds000107/versions/00001) | n/a                                        |
| ds108                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events                                                                                            | [link](https://openneuro.org/datasets/ds000108/versions/00002) | n/a                                        |
| ds109                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events                                                                                            | [link](https://openneuro.org/datasets/ds000109/versions/00001) | n/a                                        |
| ds110                  | single task, multiple runs                                                                  | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000110/versions/00001) | n/a                                        |
| ds113b                 | forrest gump watching, multiple sessions, multiple runs                                     | func                            | bold, events                                                                                                 | [link](https://openneuro.org/datasets/ds000113/versions/1.3.0) | n/a                                        |
| ds114                  | multiple tasks, multiple runs                                                               | anat, dwi, func                 | T1w, bold, dwi, events                                                                                       | [link](https://openneuro.org/datasets/ds000114/versions/1.0.1) | n/a                                        |
| ds116                  | multiple tasks, multiple runs                                                               | anat, func                      | T1w, bold, events, inplaneT2                                                                                 | [link](https://openneuro.org/datasets/ds000116/versions/00003) | n/a                                        |
| ds210                  | multiple tasks, multiple runs                                                               | func                            | bold, physio                                                                                                 | [link](https://openneuro.org/datasets/ds000210/versions/00002) | n/a                                        |
| eeg_rest_fmri          | Resting state with simultaneous fMRI. BrainVision data format (.eeg, .vhdr, .vmrk)          | anat, dwi, eeg, func            | T1w, bold, dwi, eeg                                                                                          | n/a                                                            | [@cpernet](https://github.com/cpernet)     |
| genetics_ukbb          | multiple tasks, T1w, DTI, BOLD, genetic info                                                | anat, dwi, fmap, func           | FLAIR, T1w, bold, dwi, events, info, magnitude1, phasediff                                                   | n/a                                                            | [@cpernet](https://github.com/cpernet)     |
| ieeg_visual_multimodal | n/a                                                                                         | anat, fmap, func, ieeg          | T1w, bold, channels, coordsystem, electrodes, epi, events, ieeg, sbref                                       | n/a                                                            | [@irisgroen](https://github.com/irisgroen) |
| synthetic              | A synthetic dataset                                                                         | anat, beh, func                 | T1w, beh, bold, events, physio, scans, sessions, stim                                                        | n/a                                                            | [@effigies](https://github.com/effigies)   |

### NIRS

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name               | description                                                             | datatypes   | suffixes                                                             | link to full data                              | maintained by                                            |
|:-------------------|:------------------------------------------------------------------------|:------------|:---------------------------------------------------------------------|:-----------------------------------------------|:---------------------------------------------------------|
| fnirs_automaticity | 24 subjects performing (non-)automatic finger tapping and foot stepping | nirs        | channels, coordsystem, events, nirs, optodes, practicelogbook, scans | [link](https://doi.org/10.34973/vesb-mh30)     | [@robertoostenveld](https://github.com/robertoostenveld) |
| fnirs_tapping      | Example fNIRS measurement with three conditions from five subjects      | nirs        | channels, coordsystem, events, nirs, optodes, scans                  | [link](https://doi.org/10.5281/zenodo.5529797) | [@rob_luke](https://github.com/rob_luke)                 |

### PET

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name   | description     | datatypes   | suffixes         | link to full data                                | maintained by                                |
|:-------|:----------------|:------------|:-----------------|:-------------------------------------------------|:---------------------------------------------|
| pet001 | T1w, PET, blood | anat, pet   | T1w, blood, pet  | n/a                                              | [@mnoergaard](https://github.com/mnoergaard) |
| pet002 | T1w, PET        | anat, pet   | T1w, pet         | [link](https://openneuro.org/datasets/ds001420/) | [@mnoergaard](https://github.com/mnoergaard) |
| pet003 | T1w, PET, blood | anat, pet   | T1w, blood, pet  | n/a                                              | [@mnoergaard](https://github.com/mnoergaard) |
| pet004 | PET, blood      | pet         | blood, pet       | n/a                                              | [@mnoergaard](https://github.com/mnoergaard) |
| pet005 | T1w, PET        | anat, pet   | T1w, events, pet | n/a                                              | [@mnoergaard](https://github.com/mnoergaard) |

### qMRI

<!--
TABLE BELOW IS GENERATED AUTOMATICALLY.
DO NOT EDIT DIRECTLY.
-->

| name           | description                                                                              | datatypes   | suffixes                                               | link to full data             | maintained by                                                |
|:---------------|:-----------------------------------------------------------------------------------------|:------------|:-------------------------------------------------------|:------------------------------|:-------------------------------------------------------------|
| qmri_irt1      | Inversion Recovery T1 mapping                                                            | anat        | IRT1                                                   | `not publicly availabe`       | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_megre     | Multi-Echo Gradient-Echo for T2star mapping.                                             | anat        | MEGRE                                                  | `not publicly availabe`       | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_mese      | Multi-Echo Spin-Echo for T2 or Myelin Water Fraction (MWF) mapping.                      | anat        | MESE                                                   | `not publicly availabe`       | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_mp2rage   | MP2RAGE for T1 mapping                                                                   | anat        | MP2RAGE, defacemask                                    | [link](https://osf.io/k4bs5/) | [@Gilles86](https://github.com/Gilles86)                     |
| qmri_mp2rageme | Multi-echo MP2RAGE                                                                       | anat, fmap  | MP2RAGE, TB1map                                        | [link](https://osf.io/k4bs5/) | [@Gilles86](https://github.com/Gilles86)                     |
| qmri_mpm       | Multi-parametric mapping for R1, R2star, MTsat and PD mapping                            | anat, fmap  | MPM, RB1COR, TB1EPI, magnitude1, magnitude2, phasediff | [link](https://osf.io/k4bs5/) | [@ChristophePhillips](https://github.com/ChristophePhillips) |
| qmri_mtsat     | Example dataset for T1 and MTsat mapping. Includes a double-angle B1+ mapping example.   | anat, fmap  | MTS, TB1DAM                                            | [link](https://osf.io/k4bs5/) | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_qsm       | Chimap using fast QSM                                                                    | anat        | T1w                                                    | `not publicly availabe`       | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_sa2rage   | Fast B1+ mapping using SA2RAGE                                                           | fmap        | TB1SRGE                                                | `not publicly availabe`       | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_tb1tfl    | B1+ mapping with TurboFLASH readout.                                                     | fmap        | TB1TFL                                                 | `not publicly availabe`       | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
| qmri_vfa       | Variable Flip Angle T1 mapping. Includes an Actual Flip Angle (AFI) B1+ mapping example. | anat, fmap  | TB1AFI, VFA                                            | [link](https://osf.io/k4bs5/) | [@agahkarakuzu](https://github.com/agahkarakuzu)             |
