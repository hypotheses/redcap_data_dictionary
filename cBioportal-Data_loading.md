# cBioPortal Data Loading Guide

## Loading Data Overview

- ทุกๅ data file ต้องมี meta file [cBioportal Document](https://docs.cbioportal.org/5.1-data-loading/data-loading#preparing-study-data)
- เช็ค format ของแต่ละไฟล์ [File Format Page](https://docs.cbioportal.org/5.1-data-loading/data-loading/file-formats)
- `meta` file is needed for each data file. Must begins or ends with `meta[/|.]*.txt` or `.meta.txt`
- `data file` can be named anything, but needs to be referenced within the `meta-file`

## Files Needed

1. [**cancer study**](#cancer_study) - **Mandatory** `meta_study.txt` 
2. [**clinical data**](#clinical_data) - **Mandatory** `meta_clinical.txt` comes with `data_clinical.txt`
3. **Semi-mandatory** `meta_cancer_type.txt` comes with `cancer_type.txt`

## Cancer Study
Only need `meta_study.txt` no data file needed.

### fields in meta_study.txt 

1. **type_of_cancer** : same abbreviation set in `meta_cancer_type.txt`
2. **cancer_study_identifier** : unique string
3. **name** : Long Study Name
4. **Description** : Study description
5. _Optional_ **citation** : e.g. "TCGA, Nature 2012"
6. _Optional_ **pmid** : Pubmed ID
7. **short_name** : for showing on webpage e.g. "BRCA (Jones)"
8. _Optional_ **groups** : the user groups that is allowed access. -- check [User Authorization Page](https://docs.cbioportal.org/2.2-authorization-and-authentication/user-authorization)
9. _Optional_ **add_global_case_list** : to allow access to all samples set this value to 'true'
10. _Optional_ **tags_file** : See [Study Tags](https://docs.cbioportal.org/5.1-data-loading/data-loading/file-formats#study-tags-file)
11. **reference_genome** : {hg19, hg38}

### example of meta_study.txt

```
type_of_cancer: brca
cancer_study_identifier: brca_joneslab_2013
name: Breast Cancer (Jones Lab 2013)
short_name: BRCA (Jones)
description: Comprehensive profiling of 103 breast cancer samples. Generated by the Jones Lab 2013.
add_global_case_list: true
```

## Clinical data
Divided into 1) sample 2) patient
- **sample file** is required.

### fields in meta_clinical.txt
1. **cancer_study_identifier** : same as what's in `meta_study.txt`
2. **genetic_alteration_type** : CLINICAL
3. **datatype** : PATIENT_ATTRIBUTES or SAMPLE_ATTRIBUTES
4. **data_filename** : name of the data file

### example of meta_clinical_sample.txt

```
cancer_study_identifier: brca_tcga_pub
genetic_alteration_type: CLINICAL
datatype: SAMPLE_ATTRIBUTES
data_filename: data_clinical_sample.txt
```

### example of meta_clinical_patient.txt

```
cancer_study_identifier: brca_tcga_pub
genetic_alteration_type: CLINICAL
datatype: PATIENT_ATTRIBUTES
data_filename: data_clinical_patient.txt
```

### fields in data_clinical.txt

- the attributes defined in the sample file belongs to the sample. 
- the attributes defined in the patient file belongs to the patient.
- **header rows** there are four header rows. Each row starts with a `#` symbol.
  1. the attribute name -- tab separated (can contain space)
  2. the attribute description -- tab separated (can contain space)
  3. the attribute datatype: three types {STRING, NUMBER, BOOLEAN}
  4. the attribute priority: the higher number display first in the chart. 
  5. the attribute name for the database: should be in capital
  6. the first row of the data
- **data field**: the only required colume/field is the PATIENT_ID

#### Preset priority  
  **attribute**: **preset priority**
    CANCER_TYPE: 3000
    CANCER_TYPE_DETAILED: 2000
    Overall survival plot: 400
    Disease free survival plot: 300
    Mutation count vs CNA Scatter Plot: 200
    Mutated genes table: 90
    CNA genes Table: 80
    study_id: 70
    number of samples per patient: 40
    Mutation data pie chart: 30
    CNA bar chart: 20
    gender: 9
    sex: 9
    age: 8

### examples of data_clinical_patient.txt
```
#Patient Identifier<TAB>Overall Survival Status<TAB>Overall Survival (Months)<TAB>Disease Free Status<TAB>Disease Free (Months)<TAB>...
#Patient identifier<TAB>Overall survival status<TAB>Overall survival in months since diagnosis<TAB>Disease free status<TAB>Disease free in months since treatment<TAB>...
#STRING<TAB>STRING<TAB>NUMBER<TAB>STRING<TAB>NUMBER<TAB>...
#1<TAB>1<TAB>1<TAB>1<TAB>1<TAB>
PATIENT_ID<TAB>OS_STATUS<TAB>OS_MONTHS<TAB>DFS_STATUS<TAB>DFS_MONTHS<TAB>...
  ```
1. PATIENT_ID - unique patient ID allows only numbers, letters, points, underscores and hyphens.
2. OS_STATUS: overall survival status
  - Possible values: 1:DECEASED, 0:LIVING
3. OS_MONTHS: numeric overall survival in months since initial diagnosis
4. DFS_STATUS: Disease free status since initial treatment
  - Possible values: 0:DiseaseFree, 1:Recurred/Progressed
5. DFS_MONTHS: numeric disease free months since initial treatment  

**--Additional fields--**
6. PATIENT_DISPLAY_NAME: Patient display name (string)
7. GENDER or SEX: Gender or sex of the patient (string)
8. AGE: Age at which the condition or disease was first diagnosed, in years (number)
9. TUMOR_SITE

**--Custom attributes--** [See this link](https://docs.cbioportal.org/5.1-data-loading/data-loading/file-formats#custom-columns-in-clinical-data)

### Example clinical_data_sample.txt
- two required columns: PATIENT_ID and SAMPLE_ID
- one patient can have multiple biopsied samples with different genomic profiels
1. PATIENT_ID (**required**)
2. SAMPLE_ID (**required**)

Adding info to the pan-cancer summary statistics tab 
3. CANCER_TYPE -- [see example](https://www.cbioportal.org/patient?studyId=lgg_ucsf_2014&caseId=P04) 
4. CANCER_TYPE_DETAIL

Adding info to the patient view
5. SAMPLE_DISPLAY_NAME
6. SAMPLE_CLASS
7. METASTATIC_SITE or PRIMARY_SITE : This will overide TUMOR_SITE in patient_data

Adding info to the [timeline visualization](https://docs.cbioportal.org/5.1-data-loading/data-loading/file-formats#timeline-data) 
8. OTHER_SAMPLE_ID : SAMPLE_ID could be different for each timeline
9. SAMPLE_TYPE, TUMOR_TISSUE_SITE or TUMOR_TYPE -- different icon for different status
    - If set to recurrence, recurred, progression or progressed: orange
    - If set to metastatic or metastasis: red
    - If set to primary or otherwise: black

### Adding custom attributes
- follow the header instruction

## Cancer type 

### fields in meta_cancer_type.txt
1. genetic_alteration_type: CANCER_TYPE
2. datatype: CANCER_TYPE
3. data_filename: 

### example of meta_cancer_type.txt

```
genetic_alteration_type: CANCER_TYPE
datatype: CANCER_TYPE
data_filename: cancer_type.txt
```
### example cancer_type.txt
List of columns 
1. **type_of_cancer** - abbreviation of the cancer type
2. **name** - longer name for the abbreviation in (1)
3. **clinical_trial_keywords** - A comma separated list of keywords used to identify this study, e.g., "breast,breast invasive".
4. **dedicated_color** - check cancer ribbon color
5. **parent_type_of_cancer** - The type_of_cancer field of the cancer type of which this is a subtype, e.g., "Breast". :information_source: : you can set parent to tissue, which is the reserved word to place the given cancer type at "root" level in the "studies oncotree" that will be generated in the homepage (aka query page) of the portal. 

#### Example of cancer_type.txt
```
brca<TAB>Breast Invasive Carcinoma<TAB>breast,breast invasive<TAB>HotPink<TAB>Breast
```

## Data Importing Steps