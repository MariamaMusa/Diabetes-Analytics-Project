# Diabetes Analytics Project
> This project analyzed healthcare statistics and lifestyle survey information data to identify the socioeconomic, clinical, and behavioral factors most associated with diabetes risk, and built a predictive model to estimate diabetes status from them - equipping governments and NGOs to target screening and interventions where they're needed most, in a country where over 80% of diabetes cases occur and diagnosis often comes too late.

---

## ⚙️ Project Type Flags
- [x] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [x] Data Cleaning / Wrangling
- [ ] Data Pipeline / ETL
- [x] Dashboard / Data Visualization
- [x] Predictive Modelling / Machine Learning
- [ ] Other: ___________
---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Dataset](#6-dataset)
7. [Analysis & Metrics](#7-analysis--metrics)
8. [Key Insights](#8-key-insights)
9. [Recommendations](#9-recommendations)
10. [Assumptions & Limitations](#10-assumptions--limitations)
11. [Future Enhancements](#11-future-enhancements)
12. [Deliverables](#12-deliverables)
13. [Author](#13-author)

---

## 1. Project Overview
**Context:** Diabetes is a rapidly growing global health burden - 589 million adults live with it worldwide (1 in 9), with cases projected to reach 853 million by 2050. Over 81% of those affected live in low- and middle-income countries, where prevalence is rising fastest and nearly half of diagnosed adults aren't on medication. Compounding this, an estimated 43% of cases go undiagnosed. In a country like Ghana, this makes data-driven identification of at-risk populations essential for guiding limited healthcare resources toward the people and interventions that need them most.

**Problem Statement:** Governments and NGOs currently lack a clear, data-backed view of which socioeconomic factors, pre-existing health conditions, and lifestyle behaviours are most associated with diabetes risk in the population they serve - making it difficult to target screening, resource allocation, and health interventions effectively. This project analyzes healthcare and lifestyle survey data to identify these risk patterns, and builds a predictive model that can estimate an individual's diabetes status from selected health and lifestyle characteristics - supporting both population-level planning and individual risk awareness.

**Approach:** After defining stakeholder objectives, I sourced the [CDC Diabetes Health Indicators dataset](https://archive.ics.uci.edu/dataset/891/cdc+diabetes+health+indicators) (BRFSS 2015 survey), deliberately introduced realistic data quality issues to simulate a real-world messy dataset using Claude, then cleaned and prepared it in Python before analyzing and visualizing it in Power BI and building a predictive model in Python.

**Outcome:** A cleaned, analysis-ready dataset, a Power BI dashboard showing which socioeconomic, clinical, and lifestyle factors are most associated with diabetes prevalence across different population segments and a predictive model capable of estimating diabetes status from selected health and lifestyle inputs.

---

## 2. Objectives
- **Primary Objective:** Identify the socioeconomic, clinical, and lifestyle factors most associated with diabetes prevalence, and build a predictive model that estimates diabetes status from selected features.
- **Secondary Objective 1:** Determine whether socioeconomic background (income, education) influences diabetes prevalence, to support equitable healthcare access planning by government.
- **Secondary Objective 2:** Assess whether pre-existing health conditions (e.g., high blood pressure, high cholesterol) increase diabetes risk, so health authorities can prepare targeted care ahead of time.
- **Secondary Objective 3:** Identify which population segments and lifestyle habits should be prioritized in NGO/health interventions, and what those interventions should address.
- **Secondary Objective 4:** Give patients/individuals a way to estimate their own diabetes risk from personal health and lifestyle characteristics, supporting early awareness and self-directed screening.

> 💡 *Every analysis decision in this project traces back to one of these objectives.*

---

## 3. Project Scope & Tools

### Scope

| Dimension | Details |
|-----------|---------|
| **In Scope** | [CDC Diabetes Health Indicators dataset](https://archive.ics.uci.edu/dataset/891/cdc+diabetes+health+indicators) (BRFSS 2015 survey), individual-level self-reported health, lifestyle, and socioeconomic indicators, and diabetes status for U.S. respondents. The dataset was deliberately modified with realistic data quality issues to practice a full data analytics workflow, analyzed and framed around questions relevant to a low- and middle-income country context (e.g., Ghana).|
| **Out of Scope** | Geographic/regional analysis (no location variable in the dataset), trend or time-series analysis, gestational diabetes/pregnancy-related hyperglycemia (no pregnancy variable present). Underlying values (income brackets, prevalence rates, healthcare access patterns) reflect the U.S. context in which the data was originally collected, and are not directly generalizable to Ghana or another lower and middle income countries.|
| **Time Period** | Data reflects a single point-in-time survey (BRFSS 2015) - no time-series component.|
| **Granularity** | Row-level / individual respondent - one row per survey participant. |

### Tools & Technologies

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | CSV files |
| Data Cleaning | Python (pandas) |
| Analysis | Power BI |
| Visualization | Power BI|
| Machine Learning | Python (Scikit-learn) |
| Version Control | Github |
| Documentation | Markdown |
| Other | Streamlit |

---

## 4. Repository Structure

```
[project-root]/
│
├── data/
│   ├── raw/                  # Original, unmodified source data - never edited
│   ├── processed/            # Cleaned and transformed data
│   └── external/             # Reference data, lookup tables, third-party files
│
├── notebooks/                # Jupyter, R Markdown, or Colab notebooks
│
├── scripts/                  # Reusable .py, .R, or .sh processing files
│
├── queries/                  # SQL files (retain this folder for SQL-heavy projects)
│   ├── exploratory/          # Ad-hoc or investigative queries
│   ├── transformations/      # Cleaning and reshaping logic
│   └── final/                # Production-ready or presentation queries
│
├── reports/                  # Final outputs: PDFs, slide decks, Word docs
│
├── visuals/                  # Exported charts, dashboard screenshots, ERD diagrams
│
├── docs/                     # Data dictionaries, schema notes, reference material
│
├── project_metadata.yml      # Machine-readable metadata (optional)
└── README.md                 # You are here
```

---

## 5. Data Workflow

```
[Data Source]
      ↓
[Ingestion / Collection Method]
      ↓
[Cleaning]
      ↓
[Transformation]
      ↓
[Analysis / Modelling]
      ↓
[Output / Visualisation / Reporting]
```

1. **Source:** [CDC Diabetes Health Indicators dataset](https://archive.ics.uci.edu/dataset/891/cdc+diabetes+health+indicators) based on the 2015 BRFSS survey. The dataset was deliberately modified to introduce realistic data quality issues for practice purposes. The new CSV file has 257,485 rows and 23 fields/columns. (Access the modified dataset from the data folder)
2. **Ingestion:** Loaded into Python using pandas
3. **Cleaning:** Removed 3,805 duplicate rows, dropped the unwanted RecordID column, renamed the fields/columns, trimmed extra whitespace from column values, standardized inconsistent categorical values, replaced invalid values, visualized the distribution of BMI, physical health and mental health values using boxplots and histograms to determine the best imputation method to use and replaced  missing values in the caategorical columns, stripped embedded units of measurement from BMI, converted BMI, Mental Health, and Physical Heallth from string to integer type, corrected negative values in BMI, Mental Health, and Physical Health to positive, removed BMI outliers (values below 14 or above 80) and removed rows where Mental Health or Physical Health exceeded the valid 30-day range       
4. **Transformation:** Created a BMI category column from the BMI column. Created DAX measures for the dashboard creation. Encoded categorical values to numerical for machine learning. Dealt with the imbalanced classes. Split the dataset into train and test set and used cross-validation
5. **Analysis:** Exploratory and visual analysis in Power BI (prevalence breakdowns by socioeconomic, clinical, and lifestyle factors), predictive modelling in Python using logistic regression via scikit-learn
6. **Output:** An interactive Power BI dashboard, presentation slides, and a trained predictive model that estimates diabetes status from selected input features.

---

## 6. Dataset

### Field Mapping

| Field Name (this dataset) | Original UCI Field | Data Type | Description | Example Value |
|------------|-----------|-------------|---------------|---------------|
| Diabetes Status | Diabetes_012 | string | Diabetes status of the respondent | No diabetes |
| High BP | HighBP | string | Had high blood pressure | Yes |
| High Cholesterol| HighChol | string | Had high cholesterol | No |
| Cholesterol Checked | CholCheck | string | Had a cholesterol check within the past 5 years | Yes |
| Smoker | Smoker | string | Smoked at least 100 cigarettes in their lifetime | Yes |
| Stroke | Stroke | string | Ever told they had a stroke | Yes |
| Heart Disease/Attack | HeartDiseaseorAttack | string | History of coronary heart disease or myocardial infarction | Yes |
| Physical Activity | PhysActivity | string | Physical activity in past 30 days (excluding job) | No |
| Fruits | Fruits | string | Consumes fruit one or more times per day | Yes |
| Vegetables | Veggies | string | Consumes vegetables one or more times per day | Yes |
| Heavy Drinker | HvyAlcoholConsump | string | Heavy alcohol consumption(more than 14 drinks per week for men and more than 7 drinks per week for women) | No |
| Healthcare Coverage | AnyHealthcare | string | Has any kind of healthcare coverage | Yes |
| No Doctor (Cost) | NoDocbcCost | string | Needed to see a doctor in the past year but couldn't due to cost | No |
| Difficulty Moving | DiffWalk | string | Serious difficulty walking or climbing stairs | No |
| Sex | Sex | string | Sex of respondent | Female |
| General Health | GenHlth | string | Self-rated general health | Good |
| Age | Age | string | Age bracket (13-level categories) | 18 - 24 |
| Education | Education | string | 	Highest level of education completed | Yes |
| Stroke | Stroke | string | Ever told they had a stroke | College graduate (4 years or more) |
| Income | Income | string | Income bracket | $50,000 to less than $75,000 |
| BMI | BMI | integer | Body Mass Index | 27 |
| Mental Health | MentHlth | integer | Number of days of poor mental health in the past 30 days | 3 |
| Physical Health | PhysHlth | integer | Number of days of poor physical health in past the 30 days| 0 |
| BMI Category (derive) | - | string | BMI category derived from the BMI field | Overweight |

> **Row count of the cleaned dataset:** 249669
> 
> **Column count of the cleaned dataset:** 23

---

## 7. Analysis & Metrics
### Analytical Approach

This project combined exploratory and hypothesis-driven analysis with predictive modelling. The exploratory phase examined distributions, missingness, and outliers in BMI, Mental Health, and Physical Health to inform cleaning decisions. The hypothesis-driven phase tested whether diabetes prevalence varies meaningfully by socioeconomic factors (income, education), pre-existing health conditions (high blood pressure, high cholesterol), and lifestyle behaviors (smoking, physical activity, diet), in line with the stakeholder questions defined in Section [1]. A logistic regression model was then built and validated to predict diabetes status from selected features.

### Key Metrics Defined

| Metric | Definition | Why It Matters |
|--------|--------------------------|----------------|
| Diabetes Prevalence Rate | Number of respondents with "Diabetes" divided by total respondents (excluding "Unknown"), calculated overall and by segment (income, education, age, sex) | The core measure used to compare risk across population segments and answer both government and NGO stakeholder questions |
| Comorbidity Count | Number of pre-existing conditions (High BP, High Cholesterol, Heart Disease/Attack, Stroke) a respondent has, from 0 to 4 | Tests whether prior health conditions compound diabetes risk, directly answering the Ministry of Health's question on preparing ahead for at-risk patients |
| Lifestyle Risk Score | Count of unhealthy lifestyle behaviors present (e.g., smoking, physical inactivity, low fruit/vegetable intake, heavy drinking), from 0 to 4 | Identifies whether risk scales with the number of modifiable behaviors, informing which lifestyle factors NGO interventions should prioritize |
| Healthcare Access Gap | Percentage of respondents lacking healthcare coverage or reporting cost as a barrier to seeing a doctor, compared by income bracket | Surfaces whether access barriers — not just prevalence — differ by socioeconomic status, relevant to the government's equitable-access question |

| `[Metric 3]` | [What it measures, in one sentence] | [What decision or question it answers] |

### Methods Used

- Descriptive statistics — distribution, central tendency, and outlier detection (used to inform BMI/Mental Health/Physical Health cleaning decisions)
- Segmentation / group comparison of diabetes prevalence by income, education, age, and sex
- Comorbidity and lifestyle risk scoring — aggregating related binary indicators into composite counts
- Association analysis between categorical risk factors (e.g., High BP, Smoker) and diabetes status
- DAX measures in Power BI for prevalence rates and segment-level KPIs
- Logistic regression (scikit-learn) for predictive modelling, with train/test split and cross-validation
---

## 8. Key Insights

<!--
  Findings + implications. Not just what happened - what it means.

  WHAT GOOD LOOKS LIKE:
  ✅ "Return rates, not sales volume, explain Region A's underperformance.
      Region A's return rate on home goods was 34% - more than double the
      company average. Revenue was not lost at the point of sale; it was
      lost post-sale through refunds. This points to a fulfilment or
      product quality issue specific to that region, not a demand problem."

  WHAT TO AVOID:
  ❌ "Region A had lower revenue than other regions in Q4."
     (That's an observation. It describes what happened.
      An insight says what it means and where to look next.)

  Aim for 3–6 insights. Quality over quantity.
-->

**Insight 1: [Short descriptive headline]**
[What you found + what it suggests. One short paragraph.]

**Insight 2: [Short descriptive headline]**
[What you found + what it suggests.]

**Insight 3: [Short descriptive headline]**
[What you found + what it suggests.]

**Insight 4 (if applicable): [Short descriptive headline]**
[What you found + what it suggests.]

---

## 9. Recommendations

<!--
  Action-oriented. Addressed to a real audience.
  Tied explicitly to the insight that supports each one.

  WHAT GOOD LOOKS LIKE:
  Priority: High
  Recommendation: "Conduct a fulfilment audit for home goods deliveries
                   in Region A - specifically investigating whether returns
                   correlate with a particular warehouse, carrier, or SKU batch."
  Based On: Insight 1 - return rate anomaly in Region A
  Owner: Operations / Supply Chain team

  WHAT TO AVOID:
  ❌ "Improve the return rate."
     (Not actionable. Doesn't say who, how, or where to start.)
  ❌ "Further analysis is needed."
     (This is a placeholder, not a recommendation.)
-->

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | [Specific, actionable step] | [Insight it comes from] | [Who should act] |
| Medium | [Specific, actionable step] | [Insight it comes from] | [Who should act] |
| Low | [Exploratory or longer-term suggestion] | [Insight it comes from] | [Who should act] |

---

## 10. Assumptions & Limitations

<!--
  WHAT GOOD LOOKS LIKE:
  Assumption: "Transaction records were assumed to be complete for all five regions.
               No validation was performed against source system record counts."
  Limitation: "The analysis cannot distinguish between returns initiated by
               the customer vs. returns initiated by the business (e.g., recalls).
               If business-initiated returns are concentrated in Region A, the
               return rate finding may reflect a policy decision, not a quality issue."

  WHAT TO AVOID:
  ❌ Leaving this section blank or writing "None known."
     Every project has limitations. Documenting them is a sign of
     analytical maturity - not a confession of failure.
-->

### Assumptions
- [What did you treat as true without being able to verify?]
- [What simplifications did you make for scope or feasibility?]
- [What domain rules or definitions did you accept as given?]

### Limitations
- [What gaps exist in the data?]
- [What analysis was out of scope but could affect interpretation?]
- [What would a more rigorous version of this project include?]
- [Are there known biases in the data source or collection method?]

> *The goal here is pre-emptive Q&A. What would a thoughtful skeptic push back on? Document the answer here, before they ask.*

---

## 11. Future Enhancements

<!--
  WHAT GOOD LOOKS LIKE:
  ✅ "Automate the monthly data pull from the POS export folder using
      a scheduled Python script, replacing the current manual process."
  ✅ "Expand the return rate analysis to include carrier-level data,
      which was unavailable in this dataset but exists in the logistics system."

  WHAT TO AVOID:
  ❌ "Add a machine learning model."
     (Vague, and disconnected from the actual findings of this project.)
  ❌ Listing aspirational features that don't follow logically from the work.
-->

- [ ] [Enhancement 1 - specific and traceable to a real gap in this project]
- [ ] [Enhancement 2]
- [ ] [Enhancement 3]
- [ ] [Enhancement 4]

---

## 12. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| [Name] | [What it contains] | [`/path/to/file`] |
| [Name] | [What it contains] | [`/path/to/file`] |
| [Name] | [What it contains] | [`/path/to/file`] |

---

## 13. Author

**Mariama Musa**

Data Analyst

- 🔗 https://www.linkedin.com/in/mariama-musa/
- 💼 https://github.com/MariamaMusa
- 📧 musamariama037@gmail.com

---

*Last updated: September, 20226*

