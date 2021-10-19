## Data Narrative for GRMPY

### Important Links (should all be on GitHub):
* Data Processing Flow Diagram:
- Manually deleted NIFTIs --> ran BIDS validate on all data --> uploaded to CuBIDS


* DSR GitHub Project Page(Curation/Validation and Processing Queue Status):
   * Cards for tracking the curation and validation portion of the dataset. This page should be updated every time you perform an action on the data. 
   * Cards for tracking the progress of containerized pipeline runs on the data. 
   
### Plan for the Data 

* Why does PennLINC need this data?
- Analysis of GRMPY data. 
* For which project(s) is it intended? Please link to project pages below:
- [GRMPY](https://pennlinc.github.io/grmpyproject/)
* What is our goal data format?
   * i.e. in what form do we want the data by the end of the "Curation" step? BIDS? Something else? 
   - In BIDS format, then fMRI processed


### Data Acquisition

* Who is responsible for acquiring this data?
- Acquired previously. 
* Do you have a DUA? Who is allowed to access the data?
* Where was the data acquired? 
- Acquired from FlyWheel, collected previously as [specified](https://pennlinc.github.io/grmpyproject/)
* Describe the data. What type of information do we have? Things to specify include:
   * number of subjects: 231
   * types of images: func, perf, anat

### Download and Storage 

* Who is responsible for downloading this data?
- Kahini Mehta
* From where was the data downloaded?
- Flywheel
* Where is it currently being stored?
- Flywheel, CUBIC
* What form is the data in upon intial download (DICOMS, NIFTIS, something else?)
- Dicoms, NIFTIs- BIDS format from Flywheel
* Are you using Datalad? If so, at which point did you check the data into datalad?
- Yes. Not yet. 
* Is the data backed up in a second location? If so, please provide the path to the backup location:
- CUBIC: /cbica/projects/GRMPY/dropbox/backup

### Curation Process

* Who is responsible for curating this data?
- Kahini Mehta
* GitHub Link to curation scripts/heurstics: 
- [https://github.com/kahinimehta/GRMPYGithub](https://github.com/kahinimehta/GRMPYGithub)
* GitHub Link to final CuBIDS csvs: 
* Describe the Curation Process. Include a list of the initial and final validation errors and warnings.
- Began with Flywheel and fw-heudiconv for curating into BIDS format & deleted duplicate NIFTIs + removed unnecessary BIDS data for attachments. 
* Describe additions, deletions, and metadata changes (if any).
- Used cubids-add-nifti-info, cubids-remove-metadata-fields as described [here](https://pennlinc.github.io/docs/TheWay/CuratingBIDSonDisk/)
### Preprocessing Pipelines 
* For each pipeline (e.g. QSIPrep, fMRIPrep, XCP, C-PAC), please fill out the following information:
   * Pipeline Name: fMRIPrep
   * Who is responsible for running preprocessing pipelines/audits on this data?
   - Kahini Mehta
   * Where are you running these pipelines? CUBIC? PMACS? Somewhere else?
   - CUBIC
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
- Kahini Mehta, GRMPY project
   * Link to project page(s) here: [https://pennlinc.github.io/grmpyproject/](https://pennlinc.github.io/grmpyproject/)
* For each post-processing analysis that has been run on this data, fill out the following
   * Who performed the analysis?
   - Kahini Mehta
   * Where it was performed (CUBIC, PMACS, somewhere else)?
   - CUBIC
   * GitHub Link(s) to result(s)
   * Did you use pennlinckit?  
      * https://github.com/ennLINC/PennLINC-Kit/tree/main/pennlinckit  
