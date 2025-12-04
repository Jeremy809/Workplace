# Workplace
Python project: Water Quality Analysis Project
# QCTO - Workplace Module

## Table of Contents

1. Background Context
Problem Statement
Access to clean and safe water is essential for human health, ecosystem stability, and socio-economic development. Despite its importance, river systems worldwide are increasingly threatened by pollution originating from industrial effluents, agricultural runoff, and domestic wastewater. These pollutants alter the physicochemical properties of river water, potentially rendering it unsafe for human consumption, agriculture, and aquatic ecosystems.
The dataset River water parameters (1).csv comprises multiple physicochemical measurements, including pH, turbidity, dissolved oxygen, electrical conductivity, hardness, nitrate concentration, and temperature, collected across different sampling locations and/or time periods. While the dataset provides valuable raw observations, meaningful conclusions cannot be drawn without systematic data analysis to uncover relationships, trends, and deviations from acceptable water-quality standards.
This project therefore seeks to apply data-driven analytical techniques to explore and interpret the river water quality data. The goal is to identify hidden patterns, monitor pollution indicators, and assess whether current water conditions meet environmental and public health requirements for designated uses such as drinking water supply, agricultural irrigation, and aquatic life protection.

2. Key Problems to Address
The specific research objectives of this project include:
    • Identifying trends and correlations among key water-quality parameters to understand how physicochemical factors interact within the river system.
    • Detecting anomalies or pollution indicators that may signal contamination events or environmental stress.
    • Classifying overall water quality into categories such as good, moderate, or poor based on standard water-quality indices and threshold criteria.
    • Generating actionable insights to support environmental monitoring initiatives, inform policy decisions, and contribute to improved river management practices.

Out of Scope

Real-time monitoring or sensor integration (focus is on offline data analysis).

Detailed chemical modeling of pollutant behavior beyond dataset parameters.

Prediction of future water quality trends (only historical analysis).


2. Importing Packages
   
pandas / numpy → For data cleaning, manipulation, and numerical operations.

matplotlib / seaborn → For static visualizations.

plotly / cufflinks → For interactive plots.

sklearn → For modeling, feature scaling, evaluation, and clustering.

scipy → For additional statistical tools.

collections / itertools → For handling combinations and counting (useful in Apriori or feature selection tasks).

3. Data Collection and Description<

Dataset Overview

Data type: pandas.DataFrame

Total rows (entries): 219

Total columns (features): 16

#	Column Name	Non-Null Count	Data Type	Description

Date (DD/MM/YYYY)	219	object	Date when the water sample was collected (string format).

Time (24 hrs XX:XX)	219	object	Time of sampling in 24-hour format.

Sampling point	219	object	Location or station where the sample was collected.

Ambient temperature (°C)	219	float64	Air temperature at the sampling site (°C).

Ambient humidity	219	float64	Relative humidity (%) at the time of sampling.

Sample temperature (°C)	219	float64	Temperature of the water sample (°C).

pH	219	float64	Acidity/alkalinity of the water. Ideal range: 6.5–8.5.

EC (µS/cm)	219	int64	Electrical Conductivity, indicates dissolved ions (salinity).

TDS (mg/L)	219	int64	Total Dissolved Solids — measures the combined content of all inorganic and organic substances.

TSS (mL sed/L)	213	float64	Total Suspended Solids — measures particles suspended in water.

DO (mg/L)	219	float64	Dissolved Oxygen — crucial for aquatic life.

Level (cm)	180	float64	Water level at the sampling site. Missing in 39 entries.

Turbidity (NTU)	218	float64	Water clarity — high turbidity indicates cloudiness.

Hardness (mg CaCO3/L)	217	float64	Concentration of calcium and magnesium ions.

Hardness classification	217	object	Categorical label (e.g., “Soft”, “Moderate”, “Hard”).

Total Cl- (mg Cl-/L)	213	float64	Chloride concentration — affects taste and corrosion.



Dataset is mostly complete (over 97% non-null) — good data quality.




4. Loading Data

The dataset was imported into Python using the Pandas library. An initial inspection of the dataset shape and structure was conducted to determine the number of observations, available variables, and data types.

6. Data Cleaning and Filtering

Standardization of Column Names

Column headers contained spaces, special characters, measurement units, and line breaks that complicated analysis. These were cleaned and standardized by:

Converting all names to lowercase.

Replacing spaces with underscores.

Removing special characters, parentheses, and line breaks.

This produced consistent, machine-friendly variable names.

Data Type Conversion

Date and time fields were converted to appropriate data formats:

Time values were converted into structured time formats, this enabled temporal analysis and prevented type-related errors in downstream processing.

Missing Value Handling, a missing-value audit revealed gaps in several variables such as:

Total Suspended Solids (TSS), Level measurements, Turbidity, Hardness, Chloride

To ensure data completeness while preserving realistic distributions:

Numeric variables were imputed using the median value, which is robust to skewed distributions and outliers.

Categorical variables were filled using the mode (most frequent value) to maintain logical consistency.

This approach eliminated all missing values without discarding records unnecessarily.

Outlier Detection and Removal

Outliers—extreme measurements that could distort statistical analysis—were detected using the Interquartile Range (IQR) method:

For each key numeric variable, first (Q1) and third (Q3) quartiles were calculated.

The IQR was computed as Q3 − Q1.

Values lying outside the acceptable range (Q1 − 1.5 × IQR to Q3 + 1.5 × IQR) were classified as outliers.

These anomalous values were removed to prevent skewing model results and to improve the stability of correlations, clustering, and classification.

Feature Filtering and Data Reduction, to optimize performance and focus the analysis on scientifically relevant variables, the dataset was reduced to core water-quality indicators, including:

pH, Dissolved oxygen (DO), Turbidity, Electrical conductivity (EC), Total dissolved solids (TDS), Total suspended solids (TSS), Hardness, Chloride (Cl⁻), Water temperature

Sampling point and date, non-essential or highly sparse variables were excluded to streamline exploratory data analysis and modeling.

The cleaned and filtered dataset was exported as:

8. Exploratory Data Analysis (EDA)

9. Modeling

10. Evaluation and Validation

11. Final Model

12. Conclusion and Future Work

13. References


Packages used


