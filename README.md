# DS 4320 Project 2: Predicting Readmission Risk in Diabetic Patients

### Executive Summary

This project investigates whether medication complexity can help identify diabetic patients at higher risk of hospital readmission within 30 days. Using patient data, medication complexity was measured through the number of medications and frequency of changes, revealing that patients with more complex treatment plans tend to have higher readmission rates, particularly at moderate levels of complexity. However, prior hospitalizations were found to be a stronger predictor, suggesting that medication complexity reflects underlying patient severity rather than directly causing readmission. Overall, the results show that medication complexity can serve as a useful signal for identifying high-risk patients when combined with clinical history, helping providers target additional support before discharge.

---

### Name: Madeleine Cummings

### NetID: Uwg9at

### DOI: 

### Press Release- [Read the press release](press_release/press_release.md)

### Pipeline- [View Pipeline Notebook](Pipeline/PipelineProject2.ipynb)  
### Pipeline (Markdown)- [View Markdown Version](Pipeline/PipelineProject2.md)

### Liscense- [MIT License](LICENSE.md)

-- 

## Problem Definition 

** General problem **
Predicting hospital readmission risk.

** Refined problem **

Can treatment complexity, measured by the number of active medications and dosage adjustments, predict 30-day readmission risk in diabetic patients?

### Rationale for refinement 

Hospital readmissions are costly and often preventable, making them a key focus for improving healthcare quality and efficiency. Diabetic patients often have complex healthcare plans that involve medling with many medications and dosages, which can put them at higher health instability. Understanding how treatment complexity relates to readmission risk can help healthcare professionals make better decisions about discharge planning, follow-up care, and medication management. This project aims to help support better patient outcomes and reduce unnecessary hospital returns for patients undergoing complex treatments for their diabetes.

### Motivation 

Predicting hospital readmission risk is broad and includes a lot of potential features to include. To make the analysis more focused and managable this project is refined to specifically look at diabetic patients and their treatment complexity, specifically regarding their number of active medications and dosage adjustments. I chose to focus in on diabetes as it is a chronic condition that requires ongoing medication management and frequent adjustments. Understanding what adjustments may put patients at a greater risk of readmission is important for determining what medication changes should be made, and can help make a complex process a bit simpler. As well, diabetic patients often see doctors and possibly end up in the hospital meaning that readmission rates are a meaningful subject to study. For a patient that already has to spend lots of time and money on medications, appointments and possibile hospital visits, reducing the number of readmissions saves them time, money and allows them to have a better quality of life. Another refinement made was to focus on medication related features within this population. These features are interpretable and readily available at the time that a patient is admited to a hospital the first time. As well, since the condition requires ongoing medical managment, thse features are an important driver of readmission risk.

###  A Perspcription for Readmission? What Your Meds Say About Your Risk: [Read the press release](press_release/press_release.md)

---

## Domain Exposition 

### Terminology 

| Term | Definition | Relevance to Project |
|------|-----------|--------------------|
| Readmission | A patient returning to the hospital after being discharged | Primary outcome being analyzed |
| 30-day Readmission | Readmission within 30 days of discharge | Standard healthcare quality metric |
| Diabetes Mellitus | A chronic condition affecting blood sugar regulation | Focus population of the dataset |
| Blood Glucose | The amount of sugar in the blood | Indicator of diabetes control |
| A1C Test (`A1Cresult`) | Measures average blood sugar over 2–3 months | Reflects long-term diabetes management |
| Serum Glucose (`max_glu_serum`) | Blood sugar level at a specific time | Indicates immediate condition severity |
| Insulin | Hormone used to control blood sugar levels | Key treatment for diabetes patients |
| Oral Diabetes Medications | Drugs like metformin or glipizide used to manage diabetes | Represents treatment approach |
| Medication Regimen | The combination of medications prescribed to a patient | Reflects treatment complexity |
| Dosage Adjustment | Increase or decrease in medication levels | Indicates changes in patient condition |
| Polypharmacy | Use of multiple medications by a patient | Associated with higher health risk |
| Length of Stay | Number of days a patient remains hospitalized | Indicator of illness severity |
| Inpatient Care | Treatment requiring hospital admission | Reflects serious medical conditions |
| Emergency Care | Treatment provided in the emergency department | Indicates acute health issues |
| Outpatient Care | Medical care without hospital admission | Reflects ongoing management |
| Comorbidity | Presence of multiple medical conditions | Increases risk of complications |
| Discharge Planning | Process of preparing a patient to leave the hospital | Impacts likelihood of readmission |
| Healthcare Utilization | Use of medical services over time | Helps measure patient risk patterns |
| Chronic Disease Management | Ongoing care for long-term conditions like diabetes | Central to reducing readmissions |

### About the Domain 

This project is situated within the domain of healthcare analytics, specifically focusing on hospital readmissions and chronic disease management in diabetic patients. Healthcare analytics involves using data to improve patient outcomes, reduce costs, and support clinical decision-making. Hospital readmission rates are a key quality metric, as frequent readmissions can indicate gaps in treatment, discharge planning, or ongoing care. Diabetes is a chronic condition that requires continuous monitoring and medication management, often involving multiple drugs and dosage adjustments. As a result, treatment complexity becomes an important factor in understanding patient outcomes. By analyzing how medication patterns relate to readmission risk, this project contributes to the broader goal of improving care quality and reducing unnecessary hospitalizations.

### Background reading

[View Background Reading Folder](https://myuva-my.sharepoint.com/:f:/g/personal/uwg9at_virginia_edu/IgAuzZE157GqRY36Z87neRDIAfIyIUHWZVocm0oyDOOD-SE?e=AZUj7X) 

#### Table for background reading

| Title | Description | Link |
|------|------------|------|
| Predicting and Preventing Acute Care Re-Utilization by Patients with Diabetes | Explores causes of readmissions in diabetic patients and discusses predictive models and prevention strategies | https://myuva-my.sharepoint.com/:b:/g/personal/uwg9at_virginia_edu/IQANipWdDzhVRZCUttXthxJIAe0Koskecy9EaAgL-4of_EM?e=RZ7GNx  |
| Reducing Hospital Readmissions | Provides an overview of why readmissions occur, their impact on healthcare systems, and strategies to reduce them | https://myuva-my.sharepoint.com/:b:/g/personal/uwg9at_virginia_edu/IQAP1L8OgFdxSohOQ70xVKNcAXjFkAZpLul2pyq_W50-aJc?e=jIh7yn |
| Polypharmacy Linked to Higher Risk of Hospital Readmission | Examines how taking multiple medications increases the likelihood of hospital readmission | https://myuva-my.sharepoint.com/:b:/g/personal/uwg9at_virginia_edu/IQAJz9CYMo5tQro414FhW_UiAX2ALroeSWekO8MQsF5OkqY?e=LjLNGi |
| Clinical Risk Factors and Social Needs of 30-Day Readmission Among Patients with Diabetes | Identifies key clinical and social factors associated with readmission in diabetic patients | https://myuva-my.sharepoint.com/:b:/g/personal/uwg9at_virginia_edu/IQA23xRg_ZLbQJnrWLhk5YymATA8RhQv2UyuzujQSPJCrXI?e=j7t55h |
| Adverse Childhood Experiences: Assessing the Impact on Health | Discusses how long-term health conditions and social factors impact healthcare outcomes | https://myuva-my.sharepoint.com/:b:/g/personal/uwg9at_virginia_edu/IQCmFOj9aqPpRbaW5kBRiZKLAdRQp_DywXLZo0sSvmA4X8I?e=T7wjug |

--- 

## Data Creation 

### Provenance 

The dataset being used is from a publically available source with hospital records for diabetic patients. It has over 100,000 patients and contians a large range of information including demographic data, hospital utalization, whether they were readmitted etc.

In order to use the data, the data was downloaded as a compressed file and extracted for analysis. In order to process the data for later use, missing values were standardized, duplicate records were removed and categorical variables were cleaned to ensrue conssitency. Other features were engineered to support the research question such as including the number of active medicaitons, a medication change indicator and a combined treatment complexity score. To improve storage efficiency, categorical medication variabels were encoded into binary indicators.

After preprocessing the data, the data was ingested into mongodb atlas. Each row was then transformed into a document and dstored within a collection allowing for flexible schma and efficient querying. Due to storage constraints, a representative sample of the data was used to ensure scalability. All analysis is performed by querying this mongo db collection rather than accesssing the raw csv file.

### Code Table 

| Step                                       | Description                                                                                                                                                                                                                                                                                          | Code Snippet                                                                                                                                                                                                                                                                               | Link                 |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| Data Extraction & Load                     | Extracts the compressed dataset and loads hospital encounter records for diabetic patients into a DataFrame. Each row represents a patient encounter containing medication usage, clinical variables, and readmission outcomes.                                                                      | `python\nwith zipfile.ZipFile(zip_path, 'r') as zip_ref:\n    zip_ref.extractall(extract_path)\n\ndf = pd.read_csv(csv_path)\n`                                                                                                                                                            | (https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb) |
| Data Cleaning                              | Cleans the dataset by standardizing missing values (`?` → None), removing duplicate encounters, and converting the readmission variable into a binary outcome where 1 indicates 30-day readmission.                                                                                                  | `python\ndf.replace('?', None, inplace=True)\ndf = df.drop_duplicates()\n\ndf['readmitted'] = df['readmitted'].replace({'>30':0,'NO':0,'<30':1})\n`                                                                                                                                        | https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb             |
| Feature Engineering (Treatment Complexity) | Constructs key variables to measure treatment complexity. Specifically, the number of active medications is calculated across all diabetes medications, a medication change indicator is created, and these are combined into a treatment complexity score used as the primary independent variable. | `python\ndf['num_active_meds'] = df[med_columns].apply(\n    lambda row: sum([1 for val in row if val != 'No']), axis=1\n)\n\ndf['med_change_flag'] = df['change'].apply(lambda x: 1 if x == 'Ch' else 0)\n\ndf['treatment_complexity'] = df['num_active_meds'] + df['med_change_flag']\n` | https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb            |
| Medication Encoding                        | Converts individual medication variables (e.g., insulin, metformin, glipizide) from categorical dosage/status values into binary indicators (active vs. not active). This preserves whether a medication is being used while reducing storage requirements and simplifying analysis.                 | `python\nfor col in med_columns:\n    df[col] = df[col].apply(lambda x: 0 if x == 'No' else 1)\n`                                                                                                                                                                                          | https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb            |
| Feature Selection                          | Retains only variables relevant to the research question, including treatment variables (medications and complexity), outcome (readmission), and control variables (demographics and clinical severity), while removing identifiers and high-cardinality fields.                                     | `python\ndf = df[columns_to_keep]\n`                                                                                                                                                                                                                                                       | https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb           |
| Sampling (Atlas Constraint Handling)       | Applies random sampling to create a representative subset of the data that fits within MongoDB Atlas free-tier storage limits while preserving the statistical structure necessary for modeling.                                                                                                     | `python\ndf = df.sample(n=10000, random_state=42)\n`                                                                                                                                                                                                                                       | https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb             |
| MongoDB Atlas Connection                   | Establishes a connection to a MongoDB Atlas cloud cluster and initializes a database and collection for storing patient encounter documents using the document model.                                                                                                                                | `python\nclient = MongoClient(connection_string)\ndb = client['diabetes_db_v2']\ncollection = db['encounters']\n`                                                                                                                                                                          | (https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb)             |
| Data Upload (Document Creation)            | Converts each patient encounter into a JSON document and uploads the processed dataset into MongoDB Atlas, where each document contains treatment variables, clinical context, and readmission outcome.                                                                                              | `python\ncollection.insert_many(df.to_dict('records'))\n`                                                                                                                                                                                                                                  | https://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb             |
| Data Retrieval for Analysis                | Queries MongoDB to retrieve stored documents and converts them back into a DataFrame for modeling and analysis, ensuring MongoDB is the primary data source.                                                                                                                                         | `python\ndata = list(collection.find())\ndf_mongo = pd.DataFrame(data)\n`                                                                                                                                                                                                                  | hhttps://github.com/Madeleine-Cummings/Data-By-Design-Project-2/blob/main/notebooks/Creating_the_data%20(1).ipynb             |

### Rationale 

Several key decisions were made during the data creation process to balance interpretability, feasibility, and alignment with the research question. The most important decision was how to define and construct treatment complexity. Rather than relying solely on the provided num_medications variable, treatment complexity was explicitly engineered using both the number of active diabetes medications and whether a medication change occurred. This approach was chosen to better capture the idea that complexity is not just about how many medications a patient is on, but also whether their treatment is being actively adjusted, which may indicate instability in their condition.

Another decision was made in selecting which variables to retain. Identifiers and high-cardinality variables (such as encounter IDs and diagnosis codes) were removed to reduce noise and storage overhead, while demographic and clinical variables were retained as controls. Although these variables are not the primary focus of the analysis, they are important for accounting for confounding factors such as patient age and baseline health. Excluding them would have simplified the dataset but introduced greater risk of biased results.

Finally, due to MongoDB Atlas storage limitations, a random sample of the dataset was used. This introduces some uncertainty, particularly around rare events or less common medication combinations, which may not be perfectly represented in the sample. However, random sampling was chosen as a reasonable compromise to preserve the overall structure of the data while enabling the use of a cloud-based document database.

### Bias identification 

There are a few ways bias could have been introduced in this dataset and in how the data was processed. First, the data is based on hospital encounters rather than unique patients, so patients who are admitted multiple times appear more than once. This means the dataset may overrepresent individuals with more severe conditions, who are both more likely to have complex medication regimens and to be readmitted. As a result, the relationship between treatment complexity and readmission risk could be overstated.

Another major source of bias comes from how treatment is assigned. Medication complexity is not random: patients who are sicker or have more complications are more likely to be prescribed more medications or have changes to their treatment. This creates an issue where higher treatment complexity may appear to increase readmission risk, when in reality it could just be reflecting underlying severity that is not fully captured in the dataset.

There is also some measurement bias introduced during preprocessing. Medication variables originally included categories like “No,” “Steady,” “Up,” and “Down,” but these were simplified into binary indicators to reduce storage and make analysis easier. While this helps with efficiency, it removes important detail. For example, a medication being increased (“Up”) is treated the same as it simply being present, even though those situations could reflect very different levels of treatment intensity. Because of this, the constructed treatment complexity measure may not fully capture the nuance of dosage adjustments.

Finally, bias may have been introduced through sampling. The dataset was reduced in size to fit MongoDB Atlas storage constraints, and while random sampling was used, it may not perfectly preserve less common patterns, such as rare medication combinations or specific readmission cases. This could slightly affect how representative the final dataset is.

### Bias mitigation 

Several key decisions were made during the data creation process to balance interpretability, feasibility, and alignment with the research question. The most important decision was how to define and construct treatment complexity. Rather than relying solely on the provided num_medications variable, treatment complexity was explicitly engineered using both the number of active diabetes medications and whether a medication change occurred. This approach was chosen to better capture the idea that complexity is not just about how many medications a patient is on, but also whether their treatment is being actively adjusted, which may indicate instability in their condition.

Another decision was made in selecting which variables to retain. Identifiers and high-cardinality variables (such as encounter IDs and diagnosis codes) were removed to reduce noise and storage overhead, while demographic and clinical variables were retained as controls. Although these variables are not the primary focus of the analysis, they are important for accounting for confounding factors such as patient age and baseline health. Excluding them would have simplified the dataset but introduced greater risk of biased results.

Finally, due to MongoDB Atlas storage limitations, a random sample of the dataset was used. This introduces some uncertainty, particularly around rare events or less common medication combinations, which may not be perfectly represented in the sample. However, random sampling was chosen as a reasonable compromise to preserve the overall structure of the data while enabling the use of a cloud-based document database.

--- 

## Metadata

### Implicit Schema 

Each document represents a single hospital encounter for a diabetic patient. The schema is designed to group related variables together logically whil em aintianing flexibility. An implicit schema is used to ensure consistency while still allowing for scalable storage and efficient querying

Each document contains several conceptual groupings of fields. First, treatment-related variables form the core of the document, including individual medication indicators (e.g., insulin, metformin, glipizide), the total number of medications, and engineered features such as num_active_meds, med_change_flag, and treatment_complexity. These variables directly capture the complexity of a patient’s treatment and are central to the research question.

Second, outcome information is stored through the readmitted variable, which is encoded as a binary indicator representing whether the patient was readmitted within 30 days. This serves as the dependent variable for analysis.

Third, control variables are included to account for differences in patient characteristics and health status. These include demographic variables such as age, gender, and race, as well as clinical indicators like number of diagnoses, prior inpatient and emergency visits, and time spent in the hospital. These fields are important for reducing confounding when analyzing the relationship between treatment complexity and readmission.

Finally, laboratory and diagnostic summaries such as A1Cresult and max_glu_serum are included to provide additional clinical context. While not the primary focus, these variables help capture aspects of disease severity that may influence both treatment decisions and outcomes.

To improve storage efficiency and consistency, medication variables are stored as binary indicators (0 = not prescribed, 1 = prescribed), and categorical variables are standardized during preprocessing. All documents follow this same structure, ensuring that queries and aggregation pipelines can be applied consistently across the dataset. At the same time, the document model allows for flexibility if additional fields or derived features are introduced later in the analysis.

### Data Summary 

The MongoDB database contains a single collection of documents representing hospital encounters for diabetic patients. Each document corresponds to one encounter and includes variables related to treatment, outcomes, and patient context. The dataset has been preprocessed to remove irrelevant fields, encode medication variables, and construct a treatment complexity measure aligned with the research question.

| Category             | Description                                                                                                                                |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Database Name        | `diabetes_db_v2`                                                                                                                           |
| Collection Name      | `encounters`                                                                                                                               |
| Unit of Observation  | One hospital encounter                                                                                                                     |
| Number of Documents  | ~10,000 (random sample used due to storage constraints)                                                                                    |
| Document Structure   | Semi-structured JSON documents with consistent fields across records                                                                       |
| Feature Groups       | Treatment variables, outcome variable, control variables, and lab indicators                                                               |
| Treatment Variables  | Includes individual medication indicators and engineered features such as `num_active_meds`, `med_change_flag`, and `treatment_complexity` |
| Outcome Variable     | `readmitted`, a binary indicator of 30-day readmission                                                                                     |
| Control Variables    | Demographic and clinical variables used to account for patient differences (e.g., age, prior visits, diagnoses)                            |
| Data Encoding        | Medication variables stored as binary indicators; categorical variables standardized during preprocessing                                  |
| Data Source of Truth | MongoDB Atlas collection (all analysis performed via queries to this database)                                                             |
### Data Dictionary 

| Name                     | Data Type            | Description                                                                               | Example   |
| ------------------------ | -------------------- | ----------------------------------------------------------------------------------------- | --------- |
| num_medications          | Integer              | Total number of medications prescribed during the encounter                               | 13        |
| change                   | Binary (0/1)         | Indicates whether there was any change in diabetes medication (1 = change, 0 = no change) | 1         |
| diabetesMed              | Binary (0/1)         | Indicates whether the patient was prescribed any diabetes medication                      | 1         |
| metformin                | Binary (0/1)         | Whether metformin was prescribed during the encounter                                     | 1         |
| repaglinide              | Binary (0/1)         | Whether repaglinide was prescribed                                                        | 0         |
| nateglinide              | Binary (0/1)         | Whether nateglinide was prescribed                                                        | 0         |
| chlorpropamide           | Binary (0/1)         | Whether chlorpropamide was prescribed                                                     | 0         |
| glimepiride              | Binary (0/1)         | Whether glimepiride was prescribed                                                        | 1         |
| acetohexamide            | Binary (0/1)         | Whether acetohexamide was prescribed                                                      | 0         |
| glipizide                | Binary (0/1)         | Whether glipizide was prescribed                                                          | 0         |
| glyburide                | Binary (0/1)         | Whether glyburide was prescribed                                                          | 0         |
| tolbutamide              | Binary (0/1)         | Whether tolbutamide was prescribed                                                        | 0         |
| pioglitazone             | Binary (0/1)         | Whether pioglitazone was prescribed                                                       | 0         |
| rosiglitazone            | Binary (0/1)         | Whether rosiglitazone was prescribed                                                      | 0         |
| acarbose                 | Binary (0/1)         | Whether acarbose was prescribed                                                           | 0         |
| miglitol                 | Binary (0/1)         | Whether miglitol was prescribed                                                           | 0         |
| troglitazone             | Binary (0/1)         | Whether troglitazone was prescribed                                                       | 0         |
| tolazamide               | Binary (0/1)         | Whether tolazamide was prescribed                                                         | 0         |
| examide                  | Binary (0/1)         | Whether examide was prescribed                                                            | 0         |
| citoglipton              | Binary (0/1)         | Whether citoglipton was prescribed                                                        | 0         |
| insulin                  | Binary (0/1)         | Whether insulin was prescribed                                                            | 1         |
| glyburide-metformin      | Binary (0/1)         | Whether combination glyburide-metformin was prescribed                                    | 0         |
| glipizide-metformin      | Binary (0/1)         | Whether combination glipizide-metformin was prescribed                                    | 0         |
| glimepiride-pioglitazone | Binary (0/1)         | Whether combination glimepiride-pioglitazone was prescribed                               | 0         |
| metformin-rosiglitazone  | Binary (0/1)         | Whether combination metformin-rosiglitazone was prescribed                                | 0         |
| metformin-pioglitazone   | Binary (0/1)         | Whether combination metformin-pioglitazone was prescribed                                 | 0         |
| num_active_meds          | Integer              | Count of active diabetes medications prescribed (derived from medication indicators)      | 3         |
| med_change_flag          | Binary (0/1)         | Indicates whether any medication adjustment occurred (derived from `change`)              | 1         |
| treatment_complexity     | Integer              | Composite measure of treatment complexity (active meds + change flag)                     | 4         |
| readmitted               | Binary (0/1)         | Indicates 30-day hospital readmission (1 = yes, 0 = no)                                   | 1         |
| age                      | Categorical (binned) | Age group of patient (stored as category ranges)                                          | [60-70)   |
| gender                   | Binary (0/1)         | Patient gender (1 = male, 0 = female)                                                     | 1         |
| race                     | Categorical          | Patient race category                                                                     | Caucasian |
| time_in_hospital         | Integer              | Number of days spent in hospital during encounter                                         | 5         |
| number_diagnoses         | Integer              | Total number of diagnoses recorded                                                        | 9         |
| number_inpatient         | Integer              | Number of prior inpatient visits                                                          | 2         |
| number_emergency         | Integer              | Number of prior emergency visits                                                          | 1         |
| A1Cresult                | Categorical          | Result of A1C test indicating glucose control level                                       | >8        |
| max_glu_serum            | Categorical          | Maximum recorded serum glucose level category                                             | >200      |

### Data Dictionary: Quantification of Uncertainty 

| Feature                     | Mean  | Std Dev | Min | Max | Missing % | Interpretation |
|---------------------------|-------|---------|-----|-----|----------|----------------|
| num_medications            | 16.09 | 8.15    | 1   | 69  | 0.00%    | High variability indicates large differences in medication counts. |
| change                     | —     | —       | —   | —   | 0.00%    | No missing data; binary indicator of medication change. |
| diabetesMed                | —     | —       | —   | —   | 0.00%    | Complete indicator of whether diabetes medication was prescribed. |
| metformin                  | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| repaglinide                | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| nateglinide                | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| chlorpropamide             | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| glimepiride                | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| acetohexamide              | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| glipizide                  | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| glyburide                  | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| tolbutamide                | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| pioglitazone               | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| rosiglitazone              | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| acarbose                   | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| miglitol                   | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| troglitazone               | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| tolazamide                 | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| examide                    | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| citoglipton                | —     | —       | —   | —   | 0.00%    | No missing values; binary medication indicator. |
| insulin                    | —     | —       | —   | —   | 0.00%    | No missing values; key treatment variable. |
| glyburide-metformin        | —     | —       | —   | —   | 0.00%    | No missing values; combination medication indicator. |
| glipizide-metformin        | —     | —       | —   | —   | 0.00%    | No missing values; combination medication indicator. |
| glimepiride-pioglitazone   | —     | —       | —   | —   | 0.00%    | No missing values; combination medication indicator. |
| metformin-rosiglitazone    | —     | —       | —   | —   | 0.00%    | No missing values; combination medication indicator. |
| metformin-pioglitazone     | —     | —       | —   | —   | 0.00%    | No missing values; combination medication indicator. |
| num_active_meds            | 1.19  | 0.92    | 0   | 5   | 0.00%    | Low variability; most patients take few active medications. |
| med_change_flag            | —     | —       | —   | —   | 0.00%    | Derived binary feature capturing treatment adjustments. |
| treatment_complexity       | 1.66  | 1.32    | 0   | 6   | 0.00%    | Captures combined medication burden and changes. |
| readmitted                | —     | —       | —   | —   | 0.00%    | Outcome variable; no missing data. |
| age                        | —     | —       | —   | —   | 0.00%    | Fully observed categorical age groups. |
| gender                     | —     | —       | —   | —   | 0.01%    | Negligible missingness; unlikely to impact results. |
| race                       | —     | —       | —   | —   | 2.30%    | Moderate missingness; may affect subgroup analyses. |
| time_in_hospital           | 4.37  | 2.94    | 1   | 14  | 0.00%    | Moderate variability in hospital stay duration. |
| number_diagnoses           | 7.40  | 1.94    | 1   | 16  | 0.00%    | Reflects variation in patient health complexity. |
| number_inpatient           | 0.64  | 1.25    | 0   | 21  | 0.00%    | Skewed distribution with some high-frequency patients. |
| number_emergency           | 0.20  | 1.07    | 0   | 63  | 0.00%    | Highly skewed with extreme outliers. |
| A1Cresult                  | —     | —       | —   | —   | 83.35%   | Very high missingness; not collected for most patients. |
| max_glu_serum              | —     | —       | —   | —   | 94.75%   | Extremely high missingness; reflects selective testing. |

While numerical features contain no missing values after preprocessing, several categorical variables exhibit substantial missingness. In particular, laboratory-related variables such as A1Cresult (83.35% missing) and max_glu_serum (94.75% missing) are missing for the majority of encounters. This likely reflects the fact that these tests are not administered to all patients, rather than random data loss.

Because the missingness is not random, including these variables without careful handling could introduce bias into the analysis. As a result, these features are either interpreted cautiously or excluded from certain modeling steps. Additionally, the race variable has moderate missingness (2.3%), and gender has negligible missingness (0.01%), which are unlikely to significantly impact results but are still noted for completeness.
