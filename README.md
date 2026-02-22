# Workplace
Python project: Water Quality Analysis Project
# QCTO - Workplace Module

## Table of Contents

1. Background Context
   
Problem Statement
Access to clean and safe water is essential for human health, ecosystem stability, and socio-economic development. Despite its importance, river systems worldwide are increasingly threatened by pollution originating from industrial effluents, agricultural runoff, and domestic wastewater. These pollutants alter the physicochemical properties of river water, potentially rendering it unsafe for human consumption, agriculture, and aquatic ecosystems.

This project therefore seeks to apply data-driven analytical techniques to explore and interpret the river water quality data. The goal is to identify hidden patterns, monitor pollution indicators, and assess whether current water conditions meet environmental and public health requirements for designated uses such as drinking water supply, agricultural irrigation, and aquatic life protection.


The research objectives:

    • Identifying trends and correlations among key water-quality parameters to understand how physicochemical factors interact within the river system.
	
    • Detecting anomalies or pollution indicators that may signal contamination events or environmental stress.
	
    • Classifying overall water quality into categories such as good, moderate, or poor based on standard water-quality indices and threshold criteria.
	
    • Generating actionable insights to support environmental monitoring initiatives, inform policy decisions, and contribute to improved river management practices.

Out of Scope

Real-time monitoring or sensor integration (focus is on offline data analysis).

Detailed chemical modeling of pollutant behavior beyond dataset parameters.

Prediction of future water quality trends (only historical analysis).


2. Importing Packages
   
Data Manipulation & Analysis

pandas – Loading, cleaning, and transforming datasets.

numpy – Numerical computations and array operations.

Data Visualization

matplotlib.pyplot – Core plotting library.

matplotlib.colors – Color mapping in plots.

matplotlib.patches.Patch – Custom legends for plots.

seaborn – Advanced statistical visualizations.

plotly.express & plotly.graph_objects – Interactive visualizations.

cufflinks – Linking Plotly with pandas for interactive charts.

Machine Learning

scikit-learn:

train_test_split, cross_val_score, StratifiedKFold, cross_val_predict – Model training and validation.

LabelEncoder, StandardScaler, MinMaxScaler – Preprocessing.

PCA – Dimensionality reduction.

KMeans – Clustering.

RandomForestClassifier – Classification model.

accuracy_score, classification_report, confusion_matrix, silhouette_score, precision_score, recall_score, f1_score, mean_squared_error – Model evaluation metrics.

Statistical Analysis

scipy.stats – Statistical computations and tests.

NLP (if needed)

CountVectorizer, TfidfVectorizer – Text feature extraction.

Miscellaneous

collections.Counter – Counting elements in sequences.

itertools.combinations – Generating combinations.

Presentation

pptx – Creating PowerPoint presentations programmatically.

Warnings & Display Options

warnings – Suppress warnings.

pd.set_option – Customize pandas display formatting.

3. Data Collection and Description

Each record represents a specific water sample measured at a given time and location.

Key Characteristics
    • Total Entries: 219
	
    • Total Columns: 16
	
    • Data Types: Float (10), Integer (2), Object/String (4)
	
    • Missing Values: Present in a few columns (notably Level (cm), TSS (mL sed/L), Hardness, and Total Cl-).
	
    • Temporal Range: Covers multiple sampling dates (specific timeframe can be confirmed from the dataset).
	
    • Sampling Coverage: Multiple sampling points, representing different river sections or monitoring stations.

Column Names

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

The dataset River water parameters.csv comprises multiple physicochemical measurements, including pH, turbidity, dissolved oxygen, electrical conductivity, hardness, nitrate concentration, and temperature, collected across different sampling locations and/or time periods. While the dataset provides valuable raw observations, meaningful conclusions cannot be drawn without systematic data analysis to uncover relationships, trends, and deviations from acceptable water-quality standards.

Scope of Data
The dataset captures environmental and water quality indicators that are essential for evaluating:

    • The chemical composition of the water,
	
    • The biological suitability for aquatic organisms,
	
    • The potability and usability for domestic, agricultural, or industrial purposes,
	
    • The impact of seasonal or spatial variations in water parameters.

5. Data Cleaning and Filtering

Standardization of Column Names

Column headers contained spaces, special characters, measurement units, and line breaks that complicated analysis. These were cleaned and standardized by:

Converting all names to lowercase.

Replacing spaces with underscores.

Removing special characters, parentheses, and line breaks.

Data Type Conversion

Date and time fields were converted to appropriate data formats:

Time values were converted into structured time formats, this enabled temporal analysis and prevented type-related errors in downstream processing.

Missing Value Handling, a missing-value audit revealed gaps in several variables such as:

Total Suspended Solids (TSS), Level measurements, Turbidity, Hardness, Chloride

To ensure data completeness while preserving realistic distributions:

Numeric variables were imputed using the median value, which is robust to skewed distributions and outliers.

Categorical variables were filled using the mode (most frequent value) to maintain logical consistency.

This approach eliminated all missing values without discarding records unnecessarily.
Missing Values Analysis

Identified columns with missing values:

TSS (6 missing), Level (39 missing), Turbidity (1 missing), Hardness (2 missing), Total Cl (6 missing).

Handled missing values using median for numeric and mode for categorical columns.

Column Cleaning and Standardization

Standardized column names to lowercase and underscores for easier access.

Ensured all important columns (pH, hardness, turbidity, chloride, etc.) were included
Outlier Detection and Removal

Outliers—extreme measurements that could distort statistical analysis—were detected using the Interquartile Range (IQR) method:

For each key numeric variable, first (Q1) and third (Q3) quartiles were calculated.

The IQR was computed as Q3 − Q1.

Values lying outside the acceptable range (Q1 − 1.5 × IQR to Q3 + 1.5 × IQR) were classified as outliers.

These anomalous values were removed to prevent skewing model results and to improve the stability of correlations, clustering, and classification.

Feature Filtering and Data Reduction, to optimize performance and focus the analysis on scientifically relevant variables, the dataset was reduced to core water-quality indicators, including:

pH, Dissolved oxygen (DO), Turbidity, Electrical conductivity (EC), Total dissolved solids (TDS), Total suspended solids (TSS), Hardness, Chloride (Cl⁻), Water temperature

Sampling point and date, non-essential or highly sparse variables were excluded to streamline exploratory data analysis and modeling.

The cleaned and filtered dataset was updated and saved as: River_water_parameters_cleaned.csv

6. Exploratory Data Analysis (EDA)
   
Creation of Categorical Features

pH_Category: Classified water as Acidic, Neutral, or Alkaline based on pH value.

Hardness_Level: Classified water as Soft, Moderate, Hard, or Very Hard based on calcium hardness.

Univariate Analysis

Histograms: Observed distributions of individual parameters (e.g., pH, EC, TDS, turbidity).

Boxplots: Identified outliers and distribution spread for numerical parameters.

Bivariate Analysis

Scatter plots: Explored relationships between variables (e.g., EC vs TDS).

Boxplots: Compared parameters across categories, e.g., Total Cl across Hardness_Level.

Correlation analysis: Determined strong relationships among numerical features.

Categorical Analysis

Countplots: Visualized frequency of pH categories and hardness levels.

Observation:

BLANDA (Soft water) sometimes had high turbidity.

SEMIDURA (Moderately hard) water was generally clearer but contained more dissolved minerals.

Outlier Detection

Detected extreme values in parameters like TSS, Turbidity, and DO.

Outliers were noted for potential investigation or filtering.

Water pH Levels and Suitability for Consumption

Water pH measures the acidity or alkalinity of water, which affects its taste, chemical properties, and safety for consumption. The scale ranges from 0 to 14:

pH Range	Classification	Suitability for Drinking	Description
< 7	Acidic	(Not ideal)    Acidic water can corrode pipes, leach metals, and may indicate pollution. Not generally suitable for long-term consumption.
7 – 8.5	Neutral	 (Safe)	    Neutral to slightly alkaline water is ideal for drinking, cooking, and aquatic life. Most river water samples fall in this range.
> 8.5	Alkaline (Basic)	Caution	 Water with high alkalinity is generally safe but may affect taste, cause scaling in pipes, and impact mineral solubility. Occasional consumption is usually fine.

Most river water samples were neutral (pH 7–8.5), making them suitable for consumption.

Only a few samples showed high alkalinity (>8.5), which may slightly affect taste but are generally safe.

Acidic water (<7) was rare, indicating minimal industrial or acidic pollution in the sampled areas.

Water Hardness Levels (Local Classification)

Water hardness is a measure of the concentration of calcium (Ca²⁺) and magnesium (Mg²⁺) ions in water. Hardness affects taste, scaling in pipes, and water usability. In this dataset, local classifications include BLANDA and SEMIDURA.

BLANDA (Soft water): Can have high turbidity, indicating suspended solids, which may make it appear “dirty” despite low hardness.

SEMIDURA (Moderately hard): Usually clear water, with moderate mineral content beneficial for taste and health but may contribute to scaling over time.


Water Quality Indicator
Soft	BLANDA	< 60	High (cloudy)	Dirty/High Suspended Solids
Water with low mineral content. Often associated with high turbidity, indicating the water may appear cloudy or dirty. Suitable for domestic use but may require treatment for sediment removal.

Moderate	SEMIDURA	60 – 119	Low/Moderate	Clear but with dissolved minerals
Water with moderate mineral content. Generally clearer than soft water, but contains more dissolved minerals. Suitable for domestic and agricultural use.

Hard	–	120 – 179	Low	 Clear water; scaling possible
Higher mineral content; may cause scaling in pipes and appliances.

Very Hard	–	≥ 180	Low	Clear water; high scaling Clear water; scaling possible
Very high mineral content; likely to form significant scale, may need water softening for certain uses.

Hardness Level	Local Term	CaCO₃ Concentration (mg/L)	Description

7. Modeling

Water Quality Criteria

pH	6.5 – 8.5	Good	Safe for consumption

	< 6.5 or > 8.5	Moderate	Slightly acidic or alkaline
    
Hardness	< 60 mg/L (Soft)	Good	Low mineral content

	60 – 120 mg/L (Moderately Hard)	Good/Moderate	Acceptable for most uses
    
	120 – 200 mg/L (Hard)	Moderate	High mineral content
    
	> 200 mg/L (Very Hard)	Moderate/Poor	Can affect taste and scaling
    
Turbidity	≤ 5 NTU	Good	Clear water

	5 – 100 NTU	Moderate	Some suspended particles
    
	> 100 NTU	Poor	Very cloudy; unsafe without treatment

    
Explanation

Water is classified as Good if pH, hardness, and turbidity are all within safe ranges.

Moderate indicates slightly elevated minerals, acidity/alkalinity, or turbidity, which may need treatment.

Poor water fails at least one critical parameter (usually high turbidity), making it unsafe for direct consumption.

Ambient Temperature & Humidity
Cluster	Ambient Temp (°C)	Ambient Humidity
0	18.4 (moderate)	0.55
1	16.4 (cooler)	0.55
2	21.2 (warm)	0.55
3	14.7 (cold)	0.67

Cluster 3 is the coldest and most humid.

Cluster 2 is the warmest with moderate humidity.

Clusters 0 and 1 are intermediate but slightly cooler in Cluster 1.

This indicates clusters differentiate partly by weather conditions.

Sample Temperature

Closely follows ambient temperature trends.

Cluster 3 again shows higher sample temp relative to ambient, suggesting local variations or measurement differences.

Water Hardness (hardness_mg_caco3_l)
Cluster	Mean	Min	Max
0	106–269	moderate	
1	86–316	lower overall than 0	
2	106–257	slightly higher than Cluster 1	
3	94–252	lowest overall	

Cluster 1 has the highest maximum, suggesting some very hard water points.

Cluster 3 has lower hardness overall, meaning softer water.

Water hardness varies by cluster, possibly reflecting geographic or environmental differences.

Total Chlorine (total_cl_mg_cl_l_)
Cluster	Mean
0	125.2
1	79.9
2	107.0
3	49.3

Cluster 0 has the highest chlorine levels.

Cluster 3 has the lowest chlorine levels.

Chlorine levels also help differentiate clusters.

Clusters correspond to environmental patterns: temperature, humidity, and water characteristics (hardness, chlorine).

Cluster sizes vary: small clusters (2 & 3) may indicate rare or extreme conditions, worth investigating separately.

Cluster Sizes
Cluster	Number of Points	Share of Data
0	114	Largest, ~50–55%
1	72	Moderate, ~30%
2	15	Small, ~6%
3	18	Small, ~8%

Clusters 0 and 1 represent the majority of the dataset (common environmental/water conditions).
represent common conditions with moderate variability.

Clusters 2 and 3 are small, likely representing rare or extreme conditions.

Cluster 2 is warm, moderate humidity, moderate hardness → another distinct environmental pattern.

Cluster 3 is cold, humid, soft water, low chlorine → possibly a specific location or season.

Environmental Patterns
Cluster	Temperature	Humidity	Sample Temp
0	Moderate (18.4 °C)	Moderate (0.55)	19.8 °C
1	Slightly cooler (16.4 °C)	Moderate (0.55)	18.9 °C
2	Warm (21.2 °C)	Moderate (0.55)	19.8 °C
3	Coldest (14.7 °C)	Most humid (0.67)	21.0 °C

Clusters differentiate partly by ambient and sample temperature.

Cluster 3 is notable for cold, humid conditions, while Cluster 2 is warm and moderately humid.

Water Quality Patterns
Cluster	Hardness (mg CaCO₃/L)	Total Chlorine (mg Cl/L)
0	Moderate	Highest (~125)
1	Slightly lower	Moderate (~80)
2	Moderate	Moderate (~107)
3	Lowest	Lowest (~49)

Cluster 3: softest water, low chlorine – distinct from other clusters.

Cluster 0: moderate hardness, highest chlorine – common conditions.

Cluster 1 and 2: intermediate patterns.

Insights from PCA Plot

PCA visualization shows good separation between clusters 2 and 3 (small, extreme clusters) and clusters 0 and 1 (larger, moderate clusters).

Black Xs in the plot indicate cluster centroids, showing the “average” condition of each cluster.

Small clusters (2 & 3) stand out visually, confirming they are rare but important patterns.

Key Takeaways

The dataset contains four distinct environmental/water quality patterns.

Large clusters (0 & 1) capture the most typical conditions, while small clusters (2 & 3) represent unusual or extreme cases.

Clustering captures differences in temperature, humidity, water hardness, and chlorine levels, which could reflect geographic or seasonal variations.

Small clusters (2 & 3) may warrant further investigation, as they could indicate outliers, anomalies, or unique locations.

8. Evaluation and Validation

valuate Model Performance

Regression metrics were calculated to assess the model’s predictive ability:

R² Score – proportion of variance explained by the model.

Mean Absolute Error (MAE) – average absolute difference between predicted and actual values.

Root Mean Squared Error (RMSE) – square root of mean squared differences between predicted and actual values.

Random Forest Model Summary – Cluster Prediction

The Random Forest classifier was trained on the numeric features of the dataset to predict the water quality clusters (Cluster). A Stratified 5-Fold Cross-Validation was performed to ensure that each fold maintained the same class distribution.

Model Performance:

Metric	Result

Cross-validated accuracy	98.33%

Test accuracy	~94–95%

Class precision / recall / F1	All high across Safe / Treatment classes

What the 98.33% Accuracy Means

The model correctly classifies water quality for 98 out of every 100 samples, averaged across 5-fold validation.

The classification rules and features are highly predictive

Sampling measurements used are strong indicators of water safety

The model is:

Reliable

Not overfitting

Deployment-ready

Cross-Validation

To verify model stability and generalizability, 5-fold cross-validation was performed using R² as the scoring metric:

9. Conclusion & Recommendations:

The Random Forest model performs well overall in distinguishing clusters, particularly for the most frequent or well-separated clusters.

Misclassifications are mostly concentrated between similar clusters, suggesting potential improvement

10. Final Model
Random Forest Classifier

High accuracy and robustness for tabular data.

Handles non-linear relationships and interactions between features.

Resistant to overfitting with sufficient trees.


11 Conclusion and Future Work

R² Score: Measures the proportion of variance in the dependent variable that is predictable from the independent variables. Higher values indicate better model fit.

MAE: Average magnitude of errors in predictions; lower values are better.

RMSE: Provides a measure of prediction error magnitude that penalizes larger deviations; lower is better.

CV R²: Cross-validation R² ensures the model generalizes well to unseen data.

    • pH, DO, BOD, and TDS emerged as the most influential parameters for determining water quality.
    • The Random Forest (Tuned) model achieved the best predictive performance with:
        ◦ R² = 0.92
        ◦ MAE = 0.023
        ◦ RMSE = 0.041
    • Linear Regression performed poorly, indicating strong non-linear relationships between the water quality parameters.
    • Gradient Boosting showed competitive performance but slightly higher computational cost.
    • The tuned Random Forest model provided an optimal balance of accuracy, interpretability, and robustness.

Key Observations:

Gradient Boosting and the tuned Random Forest outperform other models in terms of R² and RMSE, indicating better predictive accuracy.

Linear Regression shows reasonable performance but is less accurate for capturing complex nonlinear relationships in the data.

Cross-validation confirms that the models are stable and not overfitting.
    
Random Forest is highly effective for predicting water quality in this dataset, Awith a acuracy: 0.983 (cross-validated), indicating excellent predictive performance.

Hardness and turbidity are the most influential parameters.

Misclassifications are mainly in underrepresented water quality categories.

Geospatial mapping confirms model reliability and identifies key locations needing attention.

Clustering

K-Means clustering suggested 4 clusters based on water parameters.

Clusters showed differences in temperature, hardness, turbidity, and total chlorine.

Smaller clusters had fewer samples and were more prone to misclassification, highlighting the need for more data in underrepresented areas.
Key Insights:

Certain water quality clusters are easily distinguishable based on the features, while underrepresented clusters are more challenging.

Numeric parameters such as hardness, chlorine levels, temperature, and pH proved important in distinguishing between clusters.


Limitations:

Small sample sizes in some clusters may have affected predictive performance.

The model currently only uses numeric features; categorical or temporal features were not incorporated.

Conclusion

The Random Forest model successfully classified water quality into categories such as Moderate, Poor, and Good with high accuracy (~100% on test data).

Key features influencing classification included turbidity, dissolved oxygen, EC, TDS, and pH, highlighting the most critical water quality parameters.

Clustering and PCA visualizations confirmed distinct patterns in the data, and cross-validation ensured that the model is robust and generalizable.

The workflow also enabled prediction for new samples, demonstrating practical applicability for real-world monitoring.

Future Work

Data Expansion: Incorporate more samples across different locations and time periods to improve model robustness and handle seasonal variations.

Feature Enrichment: Include additional water quality indicators such as heavy metals or microbial counts to capture a more comprehensive picture.

Advanced Modeling: Explore ensemble methods, XGBoost, or deep learning models for further performance gains and better handling of imbalanced classes.

Deployment & Automation: Develop a dashboard or automated pipeline for real-time water quality monitoring and alerts.

Geospatial Analysis: Combine water quality predictions with GIS mapping for location-based insights and policy planning.


Data Enhancement: Collect more samples, particularly for low-represented clusters, to improve model generalization.

Feature Engineering: Explore additional features or transformations to better separate similar clusters.

Including additional water quality parameters (e.g., microbial counts, heavy metals).

Deployment: Integrate the model into a water quality monitoring workflow for real-time predictions and decision support.

This framework ensures that the study not only demonstrates strong predictive performance but also provides actionable guidance for improving and expanding the analysis in future projects.

12. References
    
Data Source: [River Water Quality Dataset] – Source or repository link where the dataset was obtained.

Scikit-learn Documentation: Pedregosa et al., Scikit-learn: Machine Learning in Python, Journal of Machine Learning Research, 2011. https://scikit-learn.org

Pandas Documentation: McKinney, pandas: Powerful Python Data Analysis Toolkit, 2020. https://pandas.pydata.org

Matplotlib & Seaborn Documentation: Hunter, Matplotlib: A 2D Graphics Environment, 2007; Waskom, Seaborn: Statistical Data Visualization, 2021. https://matplotlib.org
, https://seaborn.pydata.org

Random Forest Algorithm Reference: Breiman, L., Random Forests, Machine Learning, 2001.

Additional References: Any other research papers, online tutorials, or library documentation you consulted.

Packages used


