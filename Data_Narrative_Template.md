## Data Narrative for GRMPY

### Important Links (should all be on GitHub):
* Data Processing Flow Diagram:
Manually deleted NIFTIs --> ran BIDS validate on all data --> uploaded to CuBIDS --> added metadata fields --> removed PHI --> checked into datalad --> deleted faulty IntendedFors, took care of fieldmaps that were incorrect by fixing the heuristic and recreating on flywheel and then fixing manually on CUBIC --> deleted extra sessions for participants on Flywheel and CUBIC (removed niftis/json)--> removed ASL data by merging into 0 in summary csv and renaming all columns when applying CuBIDS--> however, the use-datalad flag was not working. Reverted to prior state and ran cubids-apply again without that flag. Was successful. -->  removed participants with BOLD scans under 3 mins, variant num of volumes for DWI


   
### Plan for the Data 

* Why does PennLINC need this data?
Analysis of GRMPY data. 
* For which project(s) is it intended? Please link to project pages below:
[GRMPY](https://pennlinc.github.io/grmpyproject/)
* What is our goal data format?
   * i.e. in what form do we want the data by the end of the "Curation" step? BIDS? Something else? 
   In BIDS format, then fMRIPrep processed


### Data Acquisition

* Who is responsible for acquiring this data?
 Acquired previously. 
* Do you have a DUA? Who is allowed to access the data?
-
* Where was the data acquired? 
SC3T, HUP6... Acquired from FlyWheel, collected previously as [specified](https://pennlinc.github.io/grmpyproject/)
* Describe the data. What type of information do we have? Things to specify include:
   - number of subjects: 231
   - types of images: func, perf, anat, dwi

### Download and Storage 

* Who is responsible for downloading this data?
Kahini Mehta
* From where was the data downloaded?
Flywheel
* Where is it currently being stored?
Flywheel, CUBIC, Datalad
* What form is the data in upon intial download (DICOMS, NIFTIS, something else?)
NIFTIs- BIDS format from Flywheel
* Are you using Datalad? If so, at which point did you check the data into datalad?
Yes. After adding metadata and removing sensitive fields. 
* Is the data backed up in a second location? If so, please provide the path to the backup location:
CUBIC: /cbica/projects/GRMPY/backup

### Curation Process

* Who is responsible for curating this data?
Kahini Mehta
* GitHub Link to curation scripts/heuristics: 
[https://github.com/PennLINC/Flywheel_Curation/tree/master/Projects/GRMPY_822831](https://github.com/PennLINC/Flywheel_Curation/tree/master/Projects/GRMPY_822831); see heuristic version 4
* GitHub Link to final CuBIDS csvs: [https://github.com/kahinimehta/GRMPYGithub](https://github.com/kahinimehta/GRMPYGithub)
* Describe the Curation Process. Include a list of the initial and final validation errors and warnings.
See data processing flow diagram and BIDS validation list. 
* Describe additions, deletions, and metadata changes (if any).
Used cubids-add-nifti-info, cubids-remove-metadata-fields as described [here](https://pennlinc.github.io/docs/TheWay/CuratingBIDSonDisk/). Metadata fields removed include patient sex, acquisition datetime & weight. Looked at summary.csv to remove faulty IntendedFor (eg: sub 99949 had an IntendedFor in their dwi) and re-curate subjects with unused fmaps in Flywheel and manually fix on cubics by making sure all fieldmaps had the same values in IntendedFor. 

### Preprocessing Pipelines 
* For each pipeline (e.g. QSIPrep, fMRIPrep, XCP, C-PAC), please fill out the following information:
   * Pipeline Name: fMRIPrep
   * Who is responsible for running preprocessing pipelines/audits on this data?
   Kahini Mehta
   * Where are you running these pipelines? CUBIC? PMACS? Somewhere else?
   CUBIC
   * Did you implement exemplar testing? If so, please fill out the information below:
      * Path to exemplar dataset:
      * Path to exemplar outputs:
      * GitHub Link to exemplar audit:
    * For production testing, please fill out the information below:
      * Path to production inputs:
      * GitHub Link to production outputs:
      * GitHub Link to production audit: 

### Post Processing 

* Who is using the data/for which projects are people in the lab using this data?
Kahini Mehta, GRMPY project
   * Link to project page(s) here: [https://pennlinc.github.io/grmpyproject/](https://pennlinc.github.io/grmpyproject/)
* For each post-processing analysis that has been run on this data, fill out the following
   * Who performed the analysis?
   Kahini Mehta
   * Where it was performed (CUBIC, PMACS, somewhere else)?
   CUBIC
   * GitHub Link(s) to result(s)
   * Did you use pennlinckit?  Not yet.
      * https://github.com/ennLINC/PennLINC-Kit/tree/main/pennlinckit  



# BIDS Validation

Upon [first](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation1/GRMPY-validation.csv) run of the validator, we found 315 errors:

[ERROR CODE1 + Naming Issue]: 314
[ERROR CODE55 + JSON file incorrectly formatted]: 1

Attempts to resolve: 
1. Removed all the files that shouldn't be in the directory from running cubids-group
2. Manually added "Name" back to dataset_description.json

Upon [second](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation2/GRMPY-validation.csv) run of the validator, we found 311 errors:

[ERROR CODE1 + Naming Issue]: 311
However, these errors are due to ASL files which will later be replaced and can be ignored for now. Warnings of note include: 
[WARNING CODE25 + EVENTS_TSV_MISSING]: 251, chosen to ignore at this point and consider adding the tsvs later
After looking at the summary sheet, worked to fix faulty IntendedFors and other errors regarding unused FieldMaps. Satisfied with validation results, proceeded to optimization. 

Upon [third](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation3) run of the group, we found some unused fieldmaps to be fixed: fixed these by editing paths manually on cubic, re-running group. 

Upon [fourth](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation4) run of the group, we fixed most of the errors, but made some changes where the IntendedFors of certain files had some errors. 

Upon [fifth](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation5/GRMPY-validation.csv) run of the group, we fixed most of the errors - still some typos in some IntendedFors in the fmaps, fixed those after looking at summary sheet. 

Upon [sixth](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation6/GRMPY-validation.csv) run of the group, one last IntendedFor to fix.  

Upon [seventh](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation7/GRMPY-validation.csv) run of the group, we were satisfied. 

Performed [eighth](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation8/GRMPY-validation.csv) run of the group after deleting extra session. Fixed issues of concern. 

Performed [ninth](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation9/GRMPY-validation.csv) run of the group after deleting ASL data via CuBIDS apply. 

Due to error in applying cubids changes, [tenth](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation10/GRMPY-validation.csv) run of the group after cubids-undo. However, still some errors. Used git hard --resest to revert to initial state, ran validation again. 

Performed [eleventh](https://github.com/kahinimehta/GRMPYGithub/blob/main/Validation11/GRMPY-validation.csv) run of the group after reverting back; same results as run 8. 