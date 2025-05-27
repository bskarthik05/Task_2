# Titanic Dataset: Exploratory Data Analysis (EDA)

This repository contains a Python script for performing Exploratory Data Analysis (EDA) on the Titanic dataset. The primary goal of this EDA is to understand the data's underlying structure, identify patterns, detect anomalies, and make initial inferences using statistical summaries and visualizations.

The analysis is conducted using popular Python libraries: Pandas for data manipulation, and Matplotlib, Seaborn, and Plotly for data visualization.

## Dataset

The analysis uses the `Titanic-Dataset.csv` file, which contains information about passengers on the Titanic, including whether they survived, their age, class, fare paid, etc.

## Tasks Performed in the EDA Script

The Python script (`task_2.py`) systematically performs the following EDA tasks:

### 1. Initial Data Inspection & Summary Statistics
   - **Objective:** Get a first look at the data and its basic statistical properties.
   - **Actions:**
     - Load the dataset using Pandas.
     - Display the first few rows of the dataset (`df.head()`).
     - Print concise summary of the DataFrame (`df.info()`), including data types and non-null counts.
     - Generate descriptive statistics for numerical features (`df.describe()`), which includes count, mean, standard deviation, min, max, and quartiles.
     - Generate descriptive statistics for categorical features (`df.describe(include=['object', 'category'])`), showing count, unique values, top value, and frequency of the top value.
     - Check for and sum missing values for each column (`df.isnull().sum()`).
   - **Basic Data Cleaning for Visualization:**
     - Create a copy of the DataFrame (`df_vis`) for visualizations to preserve the original data.
     - Impute missing 'Age' values with the median age.
     - Impute missing 'Embarked' values with the mode (most frequent embarkation point).
     - Create a new binary feature 'HasCabin' (1 if 'Cabin' data exists, 0 otherwise) due to a large number of missing 'Cabin' values.

### 2. Histograms and Boxplots for Numeric Features
   - **Objective:** Understand the distribution of individual numeric features and identify potential outliers.
   - **Actions:**
     - **Histograms:**
       - Generated for key numeric features: 'Age', 'Fare', 'SibSp' (siblings/spouses aboard), 'Parch' (parents/children aboard).
       - Kernel Density Estimate (KDE) is overlaid to better visualize the distribution shape.
     - **Boxplots:**
       - Generated for the same numeric features ('Age', 'Fare', 'SibSp', 'Parch') to show median, quartiles, and potential outliers.
       - Boxplots are also generated to compare the distributions of these numeric features based on the 'Survived' status (0 = No, 1 = Yes). This helps in visually assessing if a feature's distribution differs between survivors and non-survivors.
       - An interactive boxplot using Plotly is created to show 'Age' distribution by 'Pclass' (Passenger Class), further segmented by 'Survived' status.

### 3. Pairplot and Correlation Matrix for Feature Relationships
   - **Objective:** Explore relationships and correlations between different features.
   - **Actions:**
     - **Correlation Matrix & Heatmap:**
       - Calculated for all numerical features (including numerically encoded categorical features like 'Survived' and 'Pclass').
       - Visualized as a heatmap using Seaborn, with correlation coefficients annotated. This helps to quickly identify pairs of features that are linearly related (positively or negatively).
     - **Pairplot:**
       - Generated using Seaborn for a selected subset of features: 'Age', 'Fare', 'Pclass', 'SibSp', 'Parch', and 'Sex' (numerically encoded as 'Sex_numeric').
       - The 'Survived' status is used as the `hue` to color-code the plots, allowing for visual inspection of how relationships between pairs of features differ for survivors versus non-survivors.
       - Diagonal plots show Kernel Density Estimates (KDE) for each feature.
       - Off-diagonal plots are scatter plots showing the relationship between pairs of features.

### 4. Identify Patterns, Trends, or Anomalies
   - **Objective:** Interpret the generated visualizations to find meaningful insights.
   - **Process:** This step involves analyzing the output from the previous steps. The script includes print statements guiding the user on what to look for:
     - **Histograms:** Check for skewness (e.g., 'Fare' is typically right-skewed), modality (e.g., 'Age' might show peaks for children and adults).
     - **Boxplots:** Identify outliers (e.g., very high 'Fare' values), compare medians and IQRs across groups (e.g., 'Age' of survivors vs. non-survivors).
     - **Correlation Matrix:** Note strong positive/negative correlations (e.g., 'Pclass' and 'Fare' are expected to be negatively correlated).
     - **Pairplot:** Look for clusters, separations, or trends in scatter plots when conditioned on 'Survived'. For example, observing if female passengers show higher survival across different ages.

### 5. Basic Feature-Level Inferences from Visuals
   - **Objective:** Draw initial conclusions about individual features and their potential impact or characteristics based on the EDA.
   - **Process:** This involves articulating the observations from the visualizations. The script provides examples of such inferences:
     - "The 'Fare' boxplot shows many high-value outliers, suggesting a few passengers paid significantly more."
     - "The histogram for 'Age' suggests that the majority of passengers were young to middle-aged adults."
     - "The correlation heatmap indicates a negative correlation between 'Pclass' and 'Fare', which is logical."
     - "The pairplot, when 'Survived' is used as hue, might show that for female passengers (Sex_numeric=1), survival rates are higher across different ages compared to male passengers."

## How to Use

1.  Ensure you have Python and the necessary libraries installed: `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly`.
    ```bash
    pip install pandas numpy matplotlib seaborn plotly
    ```
2.  Place the `Titanic-Dataset.csv` file in the same directory as the script or update the path in the script.
3.  Run the Python script (e.g., in a Jupyter Notebook or Google Colab environment).
4.  Observe the printed outputs (summary statistics, correlation matrices) and the generated plots to understand the data.

## Further EDA Possibilities

The script also suggests potential next steps for a more comprehensive EDA:
-   Count plots for categorical features (e.g., 'Sex', 'Embarked', 'Pclass', 'Survived').
-   Bar plots to show relationships between categorical features (e.g., survival rate by 'Pclass' or 'Sex').
-   Facet grids for more complex conditional visualizations.
-   Investigating relationships with 'SibSp' and 'Parch' by potentially creating a 'FamilySize' feature.

This EDA serves as a foundational step before any advanced modeling or hypothesis testing.
