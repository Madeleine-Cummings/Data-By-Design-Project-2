# DS 4320 Project 2: Predicting Readmission Risk in Diabetic Patients

## Executive Summary 

---

### Name: Madeleine Cummings

### NetID: Uwg9at

### DOI: 

### Press Release- [Read the press release](press_release/press_release.md)

### Pipeline- 

### Liscense- 

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







