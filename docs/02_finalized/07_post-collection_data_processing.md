# Guidance Note on Post-Collection Data Processing

## Introduction

Post-collection data processing refers to the set of activities undertaken to review, integrate, harmonize, clean, and validate collected microdata for errors, consistency, and completeness, turning it into well-structured datasets ready for analysis. Effective processing is essential for ensuring the data are usable, reproducible, and adequately documented for dissemination and archiving. Even with rigorous planning and well-defined protocols to minimize measurement errors, the volume and complexity of surveys, the interdependencies across datasets, and potential bugs in data-entry software resulting from imperfect testing or insufficient monitoring may still introduce human error and other inaccuracies.

This guide does not address field-level data quality monitoring. Instead, it presents best practices for post-collection raw data processing, emphasizing reproducible workflows implemented with statistical software such as Stata, SPSS, or R as well as version control platforms such as GitHub for managing and tracking processing code.

Specifically, it describes the following phases of data processing:

* **Post-collection data quality assessment** includes a comprehensive review of all variables and datasets to ensure data completeness, accuracy, consistency, and validity.
* **Data editing** is the process of preparing the data for analysis or dissemination
* **Statistical treatment of the data** is a part of the process aimed at increasing the usability of the data. It may include missing data imputation and outlier detection and replacement.
* **Anonymization** (also referred to as de-identification) is a process to remove or mask personally identifiable information (PII).

The main concept and definitions applicable to the data quality process are:

* **Completeness** refers to the extent to which all required data is present, recorded, and available in the dataset. This implies that all sections and variables that are supposed to be collected are present; no value is missing where data is expected; there are no gaps in target population coverage.
* **Accuracy** refers to how close results are to the true values of the population being measured. In the context of data processing, accuracy refers to potential errors introduced in the data collection process that can eventually be corrected. These include data entry and coding issues that may lead to misreported and illogical values.
* **Consistency** refers to the degree to which the data is logically coherent and does not contradict itself both within and across related datasets. As an example, an unemployed person receiving a salary in a labor force survey is an inconsistent record.
* **Validity** refers to the extent to which data measures what is intended to measure. In this context, values should fall within expected ranges or categories.
* **Outlier** is a data point that differs significantly from the response values of the rest of the observations in a dataset. An outlier value is unusually high or low compared to what is normal or typical, but it is not necessarily an error.
* **Unique identifier** refers to a specific variable or combination of variables that distinctly identifies each record within the dataset. This identifier ensures that every observation, such as a household, individual, or item, can be distinguished from all others, preventing duplication and supporting accurate data management.
* **Personally Identifiable Information (PII)** refers to any data that can be used to identify an individual. This may include details such as full name, address, date of birth, national identification number, driver's license number, passport information, phone numbers, email addresses, and other unique identifiers.
* **Metadata** are data and other documentation that define and describe data. For survey microdata, metadata provide structured information about the survey, its methodology, variables, data-collection and processing procedures, and other information needed to understand and use the data correctly.

## Guidelines

### Post-collection data quality assessment

Post-collection data quality assessment is the systematic evaluation of all datasets and variables after data collection to identify areas of improvement in the usability of the data and to detect issues that possibly compromise the quality of the data.

#### Data quality check list

Below is the list of typical checks that an analyst should perform to assess whether the data is ready for dissemination or analysis or needs further processing.

##### Completeness

1. **The final dataset must include all variables designated for dissemination, and these variables should be arranged so they are easily identifiable and correspond directly to the questionnaire.**
2. **The dataset must contain one record for each unique observation.** The dataset must contain one record for each unique observation: This means that every entry in the dataset should represent a distinct observation, without any duplication. In the context of household surveys, for example, each household or individual should be recorded only once according to the survey's design. The total number of records should directly correspond to the number of valid observations collected during the survey, whether that is households, individuals, or items as specified by the section of the questionnaire. Ensuring a single record per unique observation helps maintain data integrity and prevents analytical errors that could arise from duplicated entries, which can occur due to miscoding of identifiers or multiple exports from data collection applications.
3. **There should not be missing values in variables where a value is expected.**

##### Consistency

1. **Consistency between questionnaire and dataset structures.** The dataset should be structured in a way that is easiest for users to use. Normally, if the dataset resembles the questionnaire that accompanies the dataset, it would be easier to follow and use for analysis. This is especially the case when the questionnaire is long and there are many variables. The dataset could be organized following the sections in the questionnaire.
2. **Consistency in names:**

* Variables should be named, coded, and labeled as in the questionnaire, and response codes should be labeled as in the questionnaire. The same principle applies to the sections and the names of the datasets.
* Names of unique identifiers should be consistent in all sections to easily merge across.

1. **Consistency across values.** Responses recorded in different questions that are related to each other could be checked to see if they are internally consistent. For example, when soliciting information about a 5-year-old, the response to the highest level of education completed cannot be university.

##### Validity

* 1. **Navigation paths should be respected.** This means that during data collection, the flow of questions outlined in the questionnaire must be followed precisely. For example, if a respondent answers "No" to a question about owning a mobile phone, all subsequent questions about mobile phone usage should be automatically skipped. If those skip patterns are not correctly programmed or followed, a respondent may be asked and answer questions that are irrelevant to their situation, producing data that is logically inconsistent with their prior responses. In practice, this ensures that respondents are only asked relevant questions based on their previous answers, and no required questions are skipped or asked out of order. When navigation paths are not respected, it can lead to incomplete or inconsistent data, as responses may be missing due to incorrect question routing or skipped logic in the data entry process.
  2. **Out-of-range values.** Questions with numeric responses could be checked for out-of-range values. For these questions, reasonable minimum and maximum values can be predetermined. Examples include a 13th month of the year in a Gregorian calendar or a 6 recorded where the answer options are 1 through 4.

##### Accuracy

In addition to checks for consistency and validity, accuracy checks include:

1. **Outlier detection.** See details in the next section.
2. **Prior to analysis, the data could be cross-referenced against external resources.** The data could be compared against external data such as administrative records and data from previous or different surveys conducted in the same country/area.

#### Missing values and outlier detection

Missing values and outliers are data conditions that may affect the overall quality and interpretability of the dataset, although they are not necessarily indicative of errors. During the data quality assessment process, it is essential to determine appropriate procedures for identifying, evaluating, and addressing these conditions.

##### Missing values

**Missingness** in survey data occurs when required responses, variables, or records are not collected or recorded, leading to incomplete information. We refer to *item nonresponse* when the missing value is limited to particular items; and to *unit nonresponse* if the respondent (e.g. household) is not found or refuses to participate and data is missing for the whole interview. Missing values result when a question was asked, but no response was recorded, or a question that should have been asked was not asked. Missing values are different from zero (0) and should not be interpreted the same in data review. Zero is a defined value/quantity, while missing values are the absence of a value or quantity.

When assessing missing values, several questions should be asked. These include: Is this due to a wrong navigation path? Is a variable missing in the data entry program? Is the information saved somewhere else under a different variable name? This would help to identify the causes of the missing values and determine potential solutions, if any.

#### Outlier detection

An outlier is a value that appears inconsistent with the rest of a variable's distribution. Identifying such values is an essential component of data quality assessment. Several approaches are available, ranging from visual inspection to statistically defined thresholds.

The simplest methods rely on the judgement of the data analyst, who inspects tables, charts, or summary statistics to understand the distribution of a variable. Based on knowledge of the context and the data-generating process, the analyst decides which values are implausibly high or low. This step is often used as an initial screening tool.

Other approaches use statistical criteria to identify values that deviate markedly from the rest of the distribution. Common methods include the following:

**Tail-Region Thresholds** This method flags observations in the extreme tails of the distribution, typically those below the 1st (or 5th) percentile and above the 95th (or 99th) percentile. These thresholds are simple to compute and widely used in preliminary data cleaning.

**Z-Score Method** The z-score measures the distance of a value from the mean in units of standard deviation. Values beyond &plusmn;3 standard deviations are commonly treated as potential outliers. Under a normal distribution, such values occur in approximately 0.3 per cent of cases. This method is effective when the distribution is roughly symmetric and free of extreme values.

**Modified Z-Score Method** Because means and standard deviations can be distorted by outliers, a more robust alternative uses the median and the Median Absolute Deviation (MAD). A value is typically classified as an outlier if its modified z-score exceeds &plusmn;3.5. A scaling constant (0.6745) is applied to ensure comparability with the standard z-score under normality.

**Box-Plot Rule** This rule is based on the interquartile range (IQR), defined as the difference between the third quartile (Q3) and the first quartile (Q1). Observations falling below *Q1 &minus; 1.5 &times; IQR* or above *Q3 &plus; 1.5 &times; IQR* are considered potential outliers. A stricter threshold uses 3 &times; IQR. This method is robust to extreme values and does not require the assumption of normality.

Several of the statistical methods described above assume an approximately normal distribution. Many survey variables, particularly income or welfare indicators, are often skewed. In such cases, applying a transformation before outlier detection may improve performance. The natural logarithm is a simple and commonly used transformation to reduce skewness[^1].

[^1]: For further guidance on variable normalization and additional outlier detection methods relevant to welfare analysis, see [On the Construction of a Consumption Aggregate for Inequality and Poverty Analysis](https://documents.worldbank.org/en/publication/documents-reports/documentdetail/099225003092220001)

When conducting outlier detection, the analyst should observe several methodological considerations to ensure the validity and interpretability of the results.

Outlier detection should be undertaken at the item level, as different goods possess inherently distinct value ranges. For example, the purchase price of a house is not comparable to that of a car. Consequently, extreme purchase values for housing should be evaluated only within the distribution of house prices, and not against the values of other items. This practice ensures that potential outliers are assessed relative to an appropriate and internally consistent reference group.

Some variables may exhibit greater homogeneity when evaluated at an appropriate geographical level. For instance, price levels may differ substantially between urban and rural areas yet remain relatively similar within specific regions. Recognizing such geographical variation is important for outlier detection, as assessing observations within more comparable groups reduces the likelihood of misclassifying legitimate differences as anomalies. Evaluating potential outliers against a contextually appropriate reference population thereby enhances both the accuracy and the interpretability of the analysis.

Outlier detection should not be carried out when the number of observations for the variable of interest falls below a minimum acceptable threshold. Reliable identification of outliers requires sufficient data to establish a meaningful distribution against which atypical values can be evaluated. When the sample is too small, measures of central tendency and dispersion, such as the mean, median, standard deviation, or interquartile range, become unstable and highly sensitive to individual observations. The minimum number of observations required should, however, be determined in relation to the level of disaggregation at which the analysis is performed (e.g., by item, geographical area, or other relevant classifications). Setting the threshold too high may inadvertently exclude groups or categories with limited observations, whereas setting it too low may lead to unreliable identification of outliers. A balanced requirement is therefore necessary to ensure both adequate coverage and analytical validity.

It is generally advisable to employ ratio-based or other relative measures for outlier detection rather than relying solely on absolute values. For example, when both values and quantities are recorded, assessing unit prices, defined as the ratio of value to quantity, is typically more informative than evaluating each variable independently. Relative measures capture the intrinsic relationship between the underlying variables and thereby support a more accurate and meaningful identification of extreme observations.

### Data editing

The data editing process should not *change* the content or meaning of the data but is limited to generate a polished data set consistent with the questionnaire that the final user can easily use. During data editing, corrections to the data should be performed only when absolutely necessary and should be restricted to cases where logical inconsistencies or errors are clearly identified. All data editing should be documented, reproducible and reversable. During data editing, any anomaly that cannot be corrected should be documented.

This section describes the most common data editing that the analyst may have to complete during this data processing phase.

#### Alignment with questionnaire

Different data entry programs may export the dataset in their own specific structure. For example, Survey Solutions[^2] exports one dataset per reporting level (i.e. one dataset for all the individual level data from different sections, one for household level, etc.).

[^2]: Survey Solutions is a free, cloud-based software platform developed by the World Bank to facilitate the design, management, and implementation of survey data collection. For more details, see https://mysurvey.solutions/en/ .

It is important to ensure that the dataset aligns with the questionnaire that would be accompanying the dataset. This means that the dataset structure matches the questionnaire section and its format, the question numbering and formats match, the questions and their corresponding variables are in the same order, and the response options match.

#### Uniqueness of observations and identifiers

**Duplicates in the dataset.** If any duplicates are found in the dataset (e.g. all the information of a household is present in the dataset twice) and have been confirmed that they are indeed duplicates, the duplicated observations should be removed.

**Uniqueness of section identifiers**. Each file must have identification variables that uniquely identify each observation. The variable or a combination of variables that constitute the unique identifiers differ, depending on the unit of reporting. For example, in a household survey, for observations reported at a household level, the identification variable is the household ID. For observations reported at an individual level, the unique identifier is a combination of the household ID plus the Person ID, which uniquely identifies the household member within the household. For observations reported at other levels such as plot for farm households, enterprises, food consumption items, they will need the household ID and an additional identifier such as Plot ID, Enterprise ID or Item ID.

#### Variable Names & Labels

For many data entry programs, the exported dataset include variable names, variable labels and response (value) labels. If the data entry program is properly programmed and tested, the exported dataset should include correct labels. However, if the data entry program is not programmed or tested sufficiently, variable names and labels could be missing, truncated, or inconsistent with the questions.

**Variable names.** Variable names should be unique within the survey[^3]. They should be simple, short, consistent, and intuitive, following the accompanying questionnaire if possible. Variable names should use only alphanumeric characters. The use of underscores, spaces, or other punctuation marks in variable names should be avoided, as statistical packages handle such characters differently, which can create problems during dissemination in multiple formats and reduce interoperability across platforms. The most efficient system is to name variables using the section and question numbers.

[^3]: Some data entry software such as Survey Solutions will display an error message if the variable names are not unique in the programmed questionnaire.

**Variable labels.** A good method for labeling variables is to use the entire question as the label. If questions are too long, the question should be summarized without changing its meaning.

**Response (value) labels.** For coded response variables, all values should also be labeled. If the labels are not present, coded response labels should be taken verbatim from the questionnaire.

**System variables and flags.** System-generated variables and processing flags that are not required for understanding or analyzing the data should be removed from the disseminated dataset before release.

**'Other, specify'.** 'Other, specify' variables are open-ended questions that follow closed categorical questions, allowing interviewers to record respondents' answers when those answers do not fit any of the predefined categories. For the follow-up question to the coded response 'Other, specify', the responses should be checked to see if they match one of the coded responses.

When respondents are allowed to provide answers that are not included in the predefined response options, the response option include an 'Other (specify)' category where these additional responses are recorded. It is important to review these specified responses to determine if any of them correspond to existing coded response options; if so, they should be recoded accordingly to maintain consistency within the dataset.

#### Incorrect Navigation Path

All edits made to address errors resulting from an incorrectly programmed navigation path must be consistent with other responses in the dataset. When correcting such errors, any invalid responses that should not have been recorded should be reverted to blank values. These adjustments must be verified by cross-checking other responses provided by the same individual or household to ensure accuracy.

#### Incorrect/Inconsistent values

**Out-of-range values.** When a variable appears to have an error with out-of-range values, a few options for resolution are as follows:

* **Re-code it as missing** or re-code it to a specific value assigned for invalid values. For example, values such as 99999999 can be assigned for "missing" and 77777777 for "not applicable".
* **Leave it as it is:** If what is correct cannot be determined through cross-validation, leave it to the data user to decide how to treat it.
* **Drop the variable**: This should only be done in extreme cases when the data quality is severely error-prone across most or all of the responses. When a variable is dropped, this decision must be documented in the dataset metadata, including the reason for dropping it, in keeping with the principle of transparency.

**Internal inconsistencies.** If any reasonable assumption can be made, internal inconsistencies can be corrected. To make any reasonable assumptions, responses to other questions that are related should be taken into consideration and be consistent. All changes should then be documented and reversible.

Any incorrect or inconsistent value that cannot uniquely solved through reasonable assumption should be documented.

### Statistical treatment of the data

The extent of data manipulation in data processing depends on the purpose of the work. If the goal of data processing is dissemination, it is good practice to leave any statistical treatment to the final users. However, during the data quality assessment phase, it is important to identify missing values and outliers, as they may, although not necessarily, indicate errors.

**Missing values**

If an error is identified during fieldwork, it may be corrected at that stage. However, when the cause of a missing value becomes apparent only after field activities have concluded, the resulting gap must generally be accepted as a limitation of the data. Such cases should be clearly documented for the benefit of data users, unless additional information is available that permits a valid reconstruction of the missing value (for example, age at the time of the interview may be derived from the date of birth and the interview date).

Prior to analysis, the imputation of missing values may be incorporated into the data processing workflow. Imputation replaces missing observations with estimated values to mitigate potential biases in downstream analyses, such as poverty or welfare estimations. Several imputation techniques may be employed, including:

* **Multiple Imputation (MI):**
  Recommended for complex or analytically central variables, such as consumption or expenditure aggregates. MI generates multiple completed datasets to account for the uncertainty associated with missingness. Software packages such as *Stata* (e.g., the *mi* suite of commands) implement this method.
* **Hot-Deck Imputation:**
  Suitable for categorical or discrete variables (e.g., educational attainment). Missing observations are assigned values from "donor" cases that closely resemble them based on relevant characteristics such as geographic area or age group.
* **Regression-Based Imputation:**
  Appropriate for continuous variables (e.g., wages). Missing values are predicted using statistical models, typically ordinary least squares or logistic regression, based on other observed characteristics.
* **Mean or Median Substitution:**
  A simple approach that may be acceptable when the proportion of missing values is small (e.g., below 5 percent). Substitution should be performed within analytically meaningful groups, such as urban and rural strata, to preserve distributional characteristics.

**Outliers**

Outliers are not necessarily indicative of errors, as they may legitimately reflect the circumstances of observational units that differ substantially from the average. Nevertheless, it is good practice to flag and report such values. Outliers should be reviewed, where appropriate, in consultation with subject-matter experts. If an outlier is conclusively determined to represent an error, the value may be replaced with blank values. During or prior to analysis, such missing values may then be imputed using the methods outlined above.

### Anonymization

Data anonymization is the process of modifying microdata to substantially reduce the risk of identification of survey respondents while preserving the dataset's analytical value. It does not guarantee that identification is impossible, but rather makes it very difficult or reduces the probability of identification to an acceptably low level. It ensures that no individual, household, establishment, or geographic unit can be identified, either directly through explicit personal identifiers or indirectly via combinations of quasi-identifying variables. In survey operations, anonymization is typically applied before dissemination to ensure privacy of the respondents.

The need for data anonymization stems from its role in providing ethical and legal safeguards, including the protection of respondent privacy and confidentiality, adherence to commitments made during informed consent, and compliance with national data-protection laws and international guidelines such as the UN Fundamental Principles of Official Statistics[^4] and the World Bank Data Quality Policy. By minimizing disclosure risks, especially when microdata is shared with external users, anonymization also enables safe data dissemination, fostering greater research collaboration without compromising participant trust.

[^4]: https://unstats.un.org/unsd/dnss/gp/fundprinciples.aspx

Survey data anonymization is generally implemented in two stages: an initial pre-analysis phase and a final pre-publication phase. The initial stage occurs early in data processing. It focuses on identifying and removing direct personal identifiers, such as names, phone numbers, addresses, fieldworker names and IDs, email addresses, and other explicit PII. The second stage takes place after data processing is complete and addresses the risk of re-identification from indirect identifiers through advanced techniques, including encoding or masking variables, aggregating categories, applying top- or bottom-coding to extreme values, geographic masking via offsetting or removal, and eliminating rare combinations that could uniquely pinpoint respondents For detailed operational guidance on statistical disclosure control for microdata, analysts are encouraged to consult Benschop and Welch (n.d.), a guide developed by the Development Data Group (DECDG).

### Reproducible Workflows and Version Control

A core requirement of post-collection data processing is that all steps be fully reproducible and traceable. This means that every transformation applied to the raw data, including cleaning decisions, recoding, imputation, and the dropping of variables, must be captured in documented processing scripts (e.g., Stata do-files, R scripts, or Python notebooks). These scripts should be organized, commented, and stored systematically so that another analyst can replicate the entire processing workflow from the raw data to the final dissemination-ready dataset.

Version control platforms such as GitHub should be used to manage processing code, track changes over time, and maintain an audit trail. This enables teams to identify when and why a particular decision was made. Log files generated during processing runs should also be retained as part of the audit trail.

Processing code and associated logs should be stored in a designated repository and linked to the dataset documentation.

### Secure Handling of Raw and Intermediate Data

While anonymization protects data before dissemination, the handling of identifiable raw and intermediate datasets during the processing phase also requires careful attention. The following principles should be observed:

* Raw data containing PII must be stored in secure, access-controlled environments. Access should be limited to authorized team members only, using role-based permissions.
* Intermediate datasets produced during processing (e.g., partially cleaned datasets that still contain PII) should be subject to the same access controls as the raw data and should not be shared externally.
* Clear retention policies should be established for non-anonymized intermediate datasets, specifying how long they are retained and when they should be securely deleted.
* When datasets need to be transferred between team members or institutions, secure transfer protocols must be used. Sending identifiable data via unencrypted email attachments is not acceptable.
* A data risk assessment should be conducted at the start of the processing phase to identify and mitigate potential risks to confidentiality.

### Communicating and Escalating Data Quality Issues

Post-collection data processing may reveal significant quality issues that cannot be addressed through editing alone. These issues should be communicated clearly and in a timely manner. The guidance below applies:

* When a material data quality issue is identified (e.g., a systematic error affecting a key variable, a large and unexplained proportion of missing values, or evidence of enumerator fraud), it should be escalated promptly to the survey task team leader and, where appropriate, to the data steward or relevant counterpart at the national statistics office.
* A brief written record of the issue, its likely cause, the scope of affected records, and the resolution taken (or the reason it could not be resolved) should be maintained and shared with relevant stakeholders.
* Any quality issues that could affect the interpretation of the final dataset should be disclosed in the dataset documentation and accompanying technical notes, so that data users are adequately informed.

### Coherence, Comparability, and International Classifications

Beyond ensuring internal consistency within a dataset, survey data processing should promote coherence with recognized international standards and longitudinal comparability where applicable.

* When variables relate to internationally standardized concepts (e.g., industry, occupation), coding should follow established classification systems such as ISIC (International Standard Industrial Classification) or ISCO (International Standard Classification of Occupations). Deviations from these standards should be documented and justified.
* For panel surveys or surveys that are part of a series, analysts should document any changes in questionnaire design, coding, or processing procedures that may affect comparability over time. Where possible harmonization procedures should be applied to maintain longitudinal consistency.

### Metadata Standards and Deposit

Variable naming and labeling, as described in Section 2.2, are necessary but not sufficient for adequate documentation. Standardized metadata files must also be produced and deposited in centralized catalogues.

* Metadata should be produced following recognized standards, such as the Data Documentation Initiative (DDI) standard or IHSN templates. DDI allows for the documentation of data processing steps and cleaning decisions alongside variable-level documentation, making it particularly well suited for survey microdata.
* Metadata files should document the survey instrument, the sample design, processing decisions, and any known data quality issues.
* Completed metadata files must be deposited in the designated centralized catalogue in accordance with institutional requirements. Metadata deposit is not optional and should be treated as a mandatory step in the dissemination workflow.

### Access, Dissemination, and Archiving

Preparing a cleaned dataset is not the final step in the data processing workflow. Analysts are responsible for ensuring that datasets and their associated metadata are properly archived and disseminated in accordance with institutional policies.

* Cleaned datasets and their metadata must be deposited in the designated institutional repository or data archive. Dataset deposit should be completed within the timeframe specified by the relevant data management policy.
* Before dissemination, access categories must be specified (e.g., open access, licensed access, restricted access), taking into account the sensitivity of the data and any legal or ethical constraints identified during the anonymization phase.
* Licensing terms governing the use of the dataset must be clearly stated in the dataset documentation.
* Analysts should familiarize themselves with the Institution's archiving responsibilities and follow any additional procedures specified by the relevant data management unit.

### Interoperability and Responsible Use of Automated Tools

As automated and AI-driven tools become more common in data processing workflows, survey teams should be aware of both their potential and their limitations.

* Datasets should be structured to maximize interoperability across statistical platforms. This includes using standard file formats (e.g., CSV, Stata .dta), adhering to alphanumeric variable naming conventions (see Section 2.2), and producing DDI-compliant metadata.
* When automated tools (e.g., machine learning algorithms for anomaly detection or AI-assisted coding) are used in the processing workflow, they should be evaluated carefully before adoption. Analysts should understand what the tool does, on what basis it makes decisions, and what its known limitations are.
* Decisions made by automated tools should be reviewed by a qualified analyst before being applied to the data. Automated outputs should not be accepted uncritically.

The use of any automated tool in the processing workflow should be documented in the processing scripts and metadata.

## References

* Benschop, T. and Welch, M. (n.d.) Statistical Disclosure Control for Microdata: A Practice Guide. DECDG, World Bank. <https://sdcpractice.readthedocs.io/en/latest/>
* Food and Agriculture Organization of the United Nations (FAO), FAO Data and Statistical Standard Series --- Data editing and validation of input data, 2019

<https://openknowledge.fao.org/server/api/core/bitstreams/6b13757e-d7d0-48ec-aa8c-1923f35eeb7a/content> )

* Food and Agriculture Organization of the United Nations (FAO), FAO Data and Statistical Standard Series --- Imputation

<https://openknowledge.fao.org/server/api/core/bitstreams/519783f5-8328-4c72-9380-a7b7c57c1a95/content>

* Food and Agriculture Organization of the United Nations (FAO), FAO Data and Statistical Standard Series --- Data aggregation, 2019

<https://openknowledge.fao.org/server/api/core/bitstreams/9965d142-f4da-40d8-bc3e-e45d417a91cc/content>

* Innovation for Poverty Action (IPA), data cleaning Note December 5, 2025: <https://data.poverty-action.org/data-cleaning/>
* International Household Survey Network (IHSN) Generic Statistical Business Process Model (GSBPM v4.0): Guidelines on survey implementation, <https://www.ihsn.org/implementing-surveys>
* Demographic and Health Surveys Methodology (DHS): Standard recode manual for DHS-7. <https://dhsprogram.com/pubs/pdf/DHSG4/Recode7_DHS_10Sep2018_DHSG4.pdf>
* Demographic and Health Surveys Methodology (DHS): Survey organization manual. <https://dhsprogram.com/pubs/pdf/DHSG4/Recode7_DHS_10Sep2018_DHSG4.pdf>
* MICS Processing the Data (MICS3 Chapter 7): <https://mics.unicef.org/sites/mics/files/MICS3_Chapter_7___Processing_the_Data_060219.pdf>
* United Nations Statistics Division: Handbook of Surveys on Individuals and Households Foundations and Emerging Approaches (Draft): <https://unstats.un.org/UNSDWebsite/statcom/session_56/documents/BG-3p-Handbook_of_Surveys_on_Individuals_and_Households-E.pdf>
* The World Bank DIME: Development Research in Practice The DIME Analytics Data Handbook, 2021: Chapter 5 Cleaning and processing research data. <https://worldbank.github.io/dime-data-handbook/processing.html>
* United Nations Economic Commission for Europe (UNECE). (2009). *Statistical Metadata in a Corporate Context: A Guide for Managers*. Common Metadata Framework, Part A. United Nations. https://unece.org/fileadmin/DAM/stats/publications/CMF\_PartA.pdf
* International Household Survey Network (IHSN). (n.d.). *Metadata Standards and Models*. https://www.ihsn.org/documentation-standards
* International Household Survey Network (IHSN). (n.d.). *Microdata Documentation*. https://www.ihsn.org/documentation

1. For further guidance on variable normalization and additional outlier detection methods relevant to welfare analysis, see [On the Construction of a Consumption Aggregate for Inequality and Poverty Analysis](https://documents.worldbank.org/en/publication/documents-reports/documentdetail/099225003092220001) [?](#footnote-ref-1)
2. Survey Solutions is a free, cloud-based software platform developed by the World Bank to facilitate the design, management, and implementation of survey data collection. For more details, see https://mysurvey.solutions/en/ . [?](#footnote-ref-2)
3. Some data entry software such as Survey Solutions will display an error message if the variable names are not unique in the programmed questionnaire. [?](#footnote-ref-3)
4. https://unstats.un.org/unsd/dnss/gp/fundprinciples.aspx [?](#footnote-ref-4)
