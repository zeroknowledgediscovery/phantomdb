This readme file was generated on [2024-05-01] by Ishanu Chattopadhyay

# GENERAL INFORMATION

Title of Dataset: phantomDB

## Abstract
We are sharing diagnostic history of 2,000,000 phantom patients (1M phantoms generated from a national model, and 1M generated from Chicagoland African Americans treated at the University of Chicago Medical Center), comprising time-stamped diagnostic and procedural codes, along with the generative model and software (python package https://pypi.org/project/teomim), all with a permissive license. We also share the generative algorithm and results that demonstrate via critical stress-test comparisons that it is difficult to differentiate between the training database and generated phantom patients. The research community will now have access to a high quality EHR database, validated to closely replicate real data without licensing constraints. The generative AI models for the national cohort and the African-American cohort are also included.

+ Author/Principal Investigator Information
+ Name: Ishanu Chattopadhyay
+ ORCID: https://orcid.org/0000-0001-8339-8162
+ Institution Affliation: University of Chicago
+ Email: zeroknowledgediscovery@gmail.com

## Date of data collection

NA (data is generated from digital twin)

## Geographic location of data collection

Data represents output of digital twin which is 1) trained on a national database (Truven Marketscan), and 2) trained on diagnostic history of patients treated in the University of Chicago between years 2012 and 2021.

## Information about funding sources that supported the collection of the data

NA

## ABSTRACT
Thus, the PREPARE Challenge envisions significant progress in the field of AD/ADRD research with its core objective being to revolutionize early detection methods by leveraging machine learning (ML) and artificial intelligence (AI). This can substantially improve patient outcomes because early detection has been demonstrated to improve disease management by allowing for more effective treatment and planning, and providing a chance for patients to participate in emerging clinical trials. Also of crucial importance, this challenge aims to eliminate biases in current datasets and clinical procedures, seeking novel datasets that could facilitate AI and ML in predicting AD/ADRD earlier than current clinical practice. The key issue that our submission aims to address is the barrier to progress arising from the reliance of AI algorithms on extensive training datasets. The strict regulatory environment in the context of healthcare hinders development, as necessary datasets can be difficult to access and utilize legally and ethically. This present data submission from our team proposes a novel approach towards alleviating these challenges. Our solution is to leverage the power of generative AI to produce data that would be indistinguishable from real patient populations, but belong to no actual human, freeing such data from regulatory control, and proprietary restrictions. Our submission comprises a large number (2M) of “phantom” patients with high quality timestamped diagnostic medical history, over a continuous time-span of 15 years, from age 60 to 75 of the phantom patients.

## BACKGROUND

The PREPARE Challenge aims to revolutionize the early prediction of Alzheimer’s Disease and Alzheimer’s Disease Related Dementias (AD/ADRD). It seeks innovative datasets that can empower machine learning (ML) and artificial intelligence (AI) methodologies to predict AD/ADRD earlier than current clinical practices, with key emphasis on overcoming biases in existing datasets and clinical practices. AI algorithms are typically data hungry, requiring large datasets to train and validate upon. This results in a bottleneck since clinical databases are seldom open-sourced, partly due to privacy laws such as the Health Insurance Portability and Accountability Act (HIPAA) considerations in the US, and often due to the commercial and profit incentives of data warehouses which often have vast amounts of relevant data, but are unwilling to allow open source access. Without open source access, profit motives stifle scientific progress. For example, the Marketscan Database of commercial insurance claims, that houses Electronic Healthcare Records (EHR) with emphasis on diagnostic and procedural records for over 100 Million US patients, costs upward of 100K USD per year to access, putting it squarely out of reach of a large section of the research community. The key issue that our submission aims to address is the barrier to progress arising from the reliance of AI algorithms on extensive training datasets.

Our current and ongoing work is developing a novel generative AI framework that can produce medical histories reflecting realistic deep and often uncharted comorbidity constraints and relationships learned from an actual database of >20K 60-75 year old patients eventually diagnosed with AD/ADRD. Our generative AI uses a novel approach to learn and characterize cross-dependencies between time-stamped diagnostic and procedural codes in individual patient histories, to identify a 774,627 parameter model. This model, the “phantom-net”, can replicate perturbed variations of medical histories from scratch, that are no longer proprietary data, but replicate delicate cross-talk across the entire human disease-spectrum for AD/ADRD patients.

We are sharing diagnostic history of 2,000,000 phantom patients (1M phantoms generated from a national model, and 1M generated from Chicagoland African Americans treated at the University of Chicago Medical Center (UCM)), comprising time-stamped diagnostic and procedural codes, along with the generative model and software (python package teomim on PyPi), all with a permissive license. The package also comprises the generative algorithm and results that demonstrate via critical stress-test comparisons that it is exceedingly difficult to differentiate between the training database and generated phantom patients, or between validation held-back patient samples and the phantom patients. The research community will now have access to a high quality EHR database, validated to closely replicate real data without licensing constraints.

## METHODS 

We have developed a novel generative AI framework capable of producing medical histories that reflect the complex and often unexplored comorbidity constraints and relationships learned from a database of 21,734 patients aged 60-75 (and 187 African-American patients treated at UCM), who are diagnosed with AD/ADRD as evidenced by their EHR record at some point. This generative AI, termed ”phantom-net ”, utilizes a 774,627 parameter model to learn and characterize cross-dependencies between time-stamped diagnostic codes in individual patient histories. This model can replicate perturbed variations of medical histories that are no longer proprietary data but simulate the intricate interactions across the human disease spectrum for AD/ADRD patients.  Thus, the data, while being statistically indistinguishable from real patients, does not correspond to any actual human subject. Hence, no de-identification is required.

### Description of methods used for collection/generation of data: 

We describe the details of phantom-net construction and inference briefly. The phantom-net is a generative model that aims to capture the cross-dependencies between the occurrences of any of the 816 ICD10 prefixes in an individual’s medical history. Internally, for the purpose of training, the medical history of individual patients from proprietary databases is represented in a tabular format, with columns corresponding to (ICDCODE_AGEi), and rows corresponding to individual patients. To make sure we can accommodate maximum details of patient diagnostic history without loss, we encode columns with three-letter prefixes of ICD10 codes, and the remaining suffix for individual patients is actually entered as table entries. The AGE suffix in the column specification designates the age (in six month increments, first half denoted by a suffix 0, and second half of the age-year indicated by a 1, see Eq. (1)) at which the ICD10 prefix was encountered in the patient history. An example excerpt of the patient data encoding from this scheme can be described as follows:
Suppose patient_A has codes G72.9 and G24.5 at ages 61 years 3 months and 62 years 5 months and patient_B has codes G81.9 at age 62 years 7 months, then a portion of the encoding dataframe will look like:

<div style="overflow-x:auto;">
  <table>
    <tr>
      <th></th>
      <th>...</th>
      <th>G72_61_1</th>
      <th>G72_61_2</th>
      <th>G24_62_1</th>
      <th>G24_62_2</th>
      <th>G81_62_1</th>
      <th>G81_62_2</th>
      <th>...</th>
    </tr>
    <tr>
      <th>patient_A</th>
      <td>...</td>
      <td>9</td>
      <td>x</td>
      <td>5</td>
      <td>x</td>
      <td>x</td>
      <td>x</td>
      <td>...</td>
    </tr>
    <tr>
      <th>patient_B</th>
      <td>...</td>
      <td>x</td>
      <td>x</td>
      <td>x</td>
      <td>x</td>
      <td>x</td>
      <td>9</td>
      <td>...</td>
    </tr>
  </table>
</div>


The phantom-net then infers a generative model to capture the cross-dependencies of a priori unspecified complexity between the different columns of the tabular representation of the diagnostic code-histories of a patient database (in this case proprietary databases from MarketScan and UCM), all satisfying some phenotype of interest (which in this case is the presence of one or more codes for AD/ADRD). A successful inference will capture known and uncharted co-morbidities, and replicate any longitudinal effects that might exist. This inference is carried out using our quasinet python package, which infers a digital twin in the general scenario of a large number of sparsely observed categorical variables with a priori unknown cross-talk (making it applicable to the scenario at hand).

This digital twin inference algorithm has been published in the context of modeling the microbial ecosystem in the context of infant gut microbiome:

*Sizemore, Nicholas, Kaitlyn Oliphant, Ruolin Zheng, Camilia R. Martin, Erika C. Claud, and Ishanu Chattopadhyay. "A digital twin of the infant microbiome to predict neurodevelopmental deficits." Science Advances 10, no. 15 (2024): eadj0400. https://www.science.org/doi/10.1126/sciadv.adj0400*

### Methods for processing the data

The data in the phantomDB is generated from the inferred digital twin via sampling non-trivial perturbations of real patients, such that the generated data has very low correlation with that from real patients, while capturing the subtle statistical structures underlying realistic medical history. The phantom-net allows us to rigorously compute bounds on the probability of a perturbation of

 a medical history producing a “valid” phantom-patient, namely capturing the idea that random occurrences of diagnostic codes are not realistic, and deep long-range constraints exist that shape medical history over time. With an exponentially exploding number of possibilities in which a medical history over a large set of items can vary, it is computationally intractable to directly model all possible variations or their inter-related emergence rules; nevertheless, we can constrain the possibilities using the patterns distilled by the phantom-net, and approximately sample from the full conditional distributions. In particular, starting from a known sample, we may iteratively update its indices by sampling the corresponding conditional distribution in the phantom-net, thus generating data for the "phantom patients".

### Instrument- or software-specific information needed to interpret the data:

Data is shared on Zenodo (https://doi.org/10.5281/zenodo.10598052)
More phantom patient data, beyond what is shared, may be generated using the teomim package.

https://pypi.org/project/teomim/

#### Installation: 

```
pip install teomim
```
Natively runs in a X64 Linux system. For other systems, the underlying quasinet package needs to be patched.

#### for windows
```
from quasinet.osfix import osfix
osfix('win')
```
#### for mac x86_64 (macbook pro)
```
from quasinet.osfix import osfix
osfix('macx86')
```
#### mac arm (macbook air)
```
from quasinet.osfix import osfix
osfix('macarm')
```

Contact ishanu.chattopadhyay@gmail.com for quasinet import issues

## Environmental/experimental conditions: 

Digital twin is inferred from medical data of patients in medical encounters including inpatient and outpatient.

## Describe any quality-assurance procedures performed on the data:

We have shown by a sequence of evaluation measures that the phantoms are not recognizable from human patients, either by a general classifier, code distribution, or disambiguation from control patients who don't have AD/ADRD diagnosis. It is also shown that PhantomDB has non-trivial correlation structure, is not correlated with the proprietary training patients, and replicates prevalences of top AD/ADRD comorbidities.

# DATA DESCRIPTION

Data is provided in .json format, and consists of a list of dictionaries, each representing medical records of a single patient.

| Key         | Type                       | Description                                                                         |
|-------------|----------------------------|-------------------------------------------------------------------------------------|
| patient_id  | String                     | Unique identifier for each patient.                                                 |
| race        | String or null             | Indicates the race of the patient. This field may be null if the information is not available. |
| seeded      | Boolean                    | Indicates whether the patient's data has been seeded on the Training Dataset (true) or generated from an empty record (false). |
| DX_record   | Array of Objects           | An array containing diagnosis records for the patient.                              |

## Each object in DX_record array has the following properties:

| Key   | Type      | Description                                          |
|-------|-----------|------------------------------------------------------|
| date  | String    | Date of the diagnosis. Format: "YYYY-MM-DD".         |
| code  | String    | ICD-10 diagnosis code recorded on the given date.    |

# File List

The data is distributed as a compressed JSON object, which encodes time-stamped diagnostic codes for 2M phantom patients. The race of the patients is specified as a key in the JSON object. All patients are assumed to begin being observed at age 60. Full description of the format is given in the accompanying data dictionary (`data dictionary.pdf`), and schema files (`schema.json`). Additionally, all ICD10 prefixes that are used in the model are enumerated in the accompanying file `USED ICD CODES.xlsx`. These metadata files are also included in the Zenodo object version 1.1 ([https://doi.org/10.5281/zenodo.10601248](https://doi.org/10.5281/zenodo.10601248)). To be more specific:

| File Description                                | File Link                                                                                                                   |
|-------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Compressed PhantomDB database                   | [phantomDB.tgz](https://zenodo.org/records/10598052/files/phantomDB.tgz?download=1)                                         |
| Phantom-net model for national cohort           | [national.pkl.gz](https://zenodo.org/records/10598052/files/national.pkl.gz?download=1)                                     |
| Phantom-net model for African-American cohort   | [chicago AA.pkl.gz](https://zenodo.org/records/10598052/files/chicago%20AA.pkl.gz?download=1)                               |
| Data dictionary                                 | [data dictionary.pdf](https://zenodo.org/records/10601248/files/data%20dictionary.pdf?download=1)                           |
| Schema file                                     | [schema.json](https://zenodo.org/records/10601248/files/schema.json?download=1)                                             |

# ETHICS

+ The data is not from real patients, hence no regulatory approval is required.
+ The Marketscan data used for training (not shared) is accessed under Data Use Agreement, and the generation of the PhantomDB does not violate the terms of this license. In particular, no part of the proprietary data is shared, and the proprietary data cannot be re-created from what is shared.
+ The UCM data used for training (also not shared) is regulated by U Chicago Data warehouse

# ACCESS
[Detail access policies, licensing information, and any required training for dataset use.]

Licenses/restrictions placed on the data: 

The data is distributed under Creative Commons Attribution 4.0 International, which allows re-distribution and re-use of a licensed work on the condition that the creator is appropriately credited. The phantom patients have no identifiable information, and have very low or no correlation with training dataset, and thus cannot be re-identified with the training database.

# Links to publications that cite or use the data

Will be added when available

# Recommended citation for this dataset

Chattopadhyay, Ishanu. “Phantomdb”. Zenodo, January 31, 2024. https://doi.org/10.5281/zenodo.10601248

# DISCOVERY
+ https://zenodo.org/doi/10.5281/zenodo.10598051
+ https://pypi.org/project/quasinet/
+ https://pypi.org/project/teomim/

## VERSIONS for Data

v1 Jan 31, 2024

# Data Summary

- **Number of variables:** 816 x 30 = 24,480
- **Number of cases/rows/samples:** 2,000,000

## Variable List

### Variables

The dataset includes 816 ICD10 code prefixes, each with an age stamp. Variables are of the form `ICDPREFIX_AGE`.

### Example

| Variable      | Description                                                     | Unit     | Value Labels             |
|---------------|-----------------------------------------------------------------|----------|--------------------------|
| G72_61_1      | ICD10 prefix G72, age bracket between 61 and 61.5 years         | N/A      | Values complete the ICD10 code (e.g., "9" indicates G72.9) |

Each variable represents a specific ICD10 code prefix with an associated age bracket, where the age bracket is denoted in the variable name.

### Format

- `ICDPREFIX`: The prefix of the ICD10 code.
- `AGE`: The age bracket (e.g., `61_1` indicates ages between 61 and 61.5 years).

### Example Variable

- `G72_61_1`
  - **Description:** ICD10 prefix G72, age bracket between 61 and 61.5 years.
  - **Value:** Completes the ICD10 code, e.g., "9" would indicate a code of G72.9.

## Missing data codes

Each sample (phantom-patient) is simulated to have many missing data columns to match realistic histories (automatically replicated by teomim)
