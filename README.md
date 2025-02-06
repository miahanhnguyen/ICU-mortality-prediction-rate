# ICU-mortality-prediction-rate
Predicting mortality in ICU patients using MIMIC-III data
Project aims and methods:
1. Mortality Prediction in ICU:
To assess the use of machine learning algorithms in predicting mortality based on the first 24 hours of ICU data.

Data Extraction: First 24 hours of ICU admission will be used to assess early indicators of mortality.
Inclusion/Exclusion Criteria: Adult patients (age ≥ 18) will be included. Patients with incomplete data or ICU stays less than 24 hours will be excluded. Using icustay_id as key and icu_expire_flag as the outcome variable to predict because the aim is to predict the mortality probability of this icu stay not this patient. In other words, how likely is this stay being fatal.
EDA: assessing missing data, identifying outliers, and visualising key variables like vital signs, lab results, and demographics.
Analytical Methods: Machine learning models: logistic regression and decision tree. Model performance will be evaluated using accuracy, F1-score and confusion matrix. The best-performing model will be selected based on cross-validation results.
Software: Python (with libraries like scikit-learn, pandas, and matplotlib)
Data dictionary
pt_icu_outcome: Patient outcomes per ICU stay
intime and outtime: ICU entry and exit times.
admittime and dischtime: hospital admission and discharge times.
los: length of stay for the patient for the given ICU stay, which may include one or more ICU units. The length of stay is measured in fractional days.
dod: date of death
ttd: The patients time to death from ICU entry in days.
age_years: the patient’s age at ICU admission. If the patient was over 89 their DOB has been shifted to hide their true age. All these patients have age_years=91.4 (see https://mimic.mit.edu/docs/iii/tables/patients/).
icustay_id should be unique to each row, however there is one patient with errors in their admission/discharge dates (icustay_id = 229922) resulting in duplication.
expire_flag is a binary flag which indicates whether the patient died, i.e. whether DOD is null or not. This value is less relevant to this study as some deaths were recorded many years after ICU admission and can be due to other factors irrelevant to the ICU admission
icu_expire_flag or hospital_expire_flag may be more relevant in this case
vitals_hourly: Bedside measurements
The vitals_hourly table describes commonly measured bedside readings, e.g. heart rate, blood pressure. It is averaged to hourly (MIMIC is not much more frequent). No pre-ICU information is available on bedside, and so the time variable hr begins at 1 for all patients. Be aware that since these patients are in ICU some values (e.g FiO2 or respiratory rate may be “artificial”).

labs_hourly: Lab results
Contains the results of a large number of blood tests. As pre-ICU information on lab values negative values are possible for the time variable hr. The time variable indicates the time the sample was taken, the time at which the test result was available (4-12 hours later) is not available.

gcs_hourly: Glasgow Coma Score
The Glasgow Coma Scale (GCS) is a neurological scale which aims to give a reliable and objective way of recording the state of a person’s consciousness for initial as well as subsequent assessment. A person is assessed against the criteria of the scale, and the resulting points give a person’s score between 3 (indicating deep unconsciousness) and either 14 (original scale) or 15 (more widely used, modified or revised scale).

gcs is the Glasgow Coma Score, with gcsmotor, gcsverbal and gcseyes the motor, verbal and eyes components
endotrachflag: the patient was under mechanical ventilation at the time the score was taken.
output_hourly: Fluid output
The output_hourly table indicates urine output events and amounts (mL).

vasopressors
Prescription of vasopressors indicates cardiac organ failure.

transfers
There are at least 5699 who change location (e.g. ICU) during an ICU stay
