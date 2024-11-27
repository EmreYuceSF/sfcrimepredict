


![San Francisco Crime Scene](DALL·E_2024-11-26_San_Francisco_Prison_Bars.webp)

# San Francisco Crime Prediction System

Living in San Francisco for the past seven years, I’ve witnessed fluctuating crime rates reported in the news. The city's sense of safety has varied, with some periods feeling safer and others feeling noticeably more dangerous. This growing concern has prompted many, including myself, to wonder if San Francisco is becoming increasingly unsafe.

In this project, I aim to:

- Explore the trends in San Francisco crime rates.
- Develop a predictive model for specific crime types by location.
- Analyze the hourly distribution of crimes.

I hope this project provides both valuable insights and a new perspective on the city’s safety.

---

## 1. Data Sources

### **Crime Data**
I obtained crime data from **DataSF**, a platform that provides open data for San Francisco. This dataset includes incident reports filed since January 1, 2018, either by officers or self-reported through SFPD’s online reporting system. Reports are categorized as:

- **Initial Reports**: The first report filed for an incident.
- **Coplogic Reports**: Reports submitted by the public via the online system.
- **Vehicle Reports**: Incidents related to stolen or recovered vehicles.

> **Disclaimer**: The San Francisco Police Department (SFPD) does not guarantee the accuracy or completeness of the data, as it is subject to updates and changes.

Data is added after being reviewed by supervising officers. Incident reports can be removed for compliance with court orders or administrative purposes. [More details here](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-2018-to-Present/wg3w-h783/about_data).

### **Weather Data**
To analyze the impact of weather on crime, I acquired daily weather data from NOAA (National Centers for Environmental Information), a trusted and reliable government source.

### **Other Considered Data**
Initially, I explored using daily passenger data from San Francisco International Airport, but it was only available in monthly aggregates. As it didn’t suit the daily prediction needs, I excluded it.

---

## 2. Objective

My goal was to create a system that allows users to select specific neighborhoods and time frames to predict the likelihood of crimes. Ultimately, the model focuses on the top five most common crimes in San Francisco, as these have the greatest impact on daily life.

---

## 3. Data Cleaning

- **Weather Data**: The dataset was relatively clean, though a few outliers (e.g., extreme rainy days) were verified through news reports and found to be valid. I removed unnecessary columns for prediction and analysis.
- **Crime Data**: Missing values were present, but not in significant proportions. Instead of removing incomplete rows or columns, I used context-based imputation techniques, including AI-assisted filling of missing categories based on crime descriptions.

---

## 4. Exploratory Data Analysis (EDA)

![San Francisco Crime Trends](Screenshot_2024-11-26_at_2.01.15_PM.png)

Key findings from the EDA:
- **Larceny Theft (From Vehicle)**: The most common crime across many neighborhoods.
- Other crimes, such as **Motor Vehicle Theft**, **Drug Violations**, and **Vandalism**, are more prevalent in specific neighborhoods.

[Link to EDA Notebook](#)

---

## 5. Algorithms & Machine Learning

I conducted the analysis and built machine learning models using Python. After testing multiple models, I selected the best-performing algorithm based on R² and error metrics like MSE and MAE.

### **Data Preparation**
1. One-hot encoded categorical variables (e.g., crime categories).
2. Binned weather data into categories (e.g., "low," "medium," "high" precipitation).
3. Engineered new features, such as:
   - Custom neighborhood clusters using the KMeans algorithm.
   - Lag features for crime data (e.g., data from the previous day and seven days earlier).

### **Model Comparisons**

| Model                     | MSE   | MAE   | R²   |
|---------------------------|-------|-------|-------|
| Linear Regression         | 4.44  | 1.35  | 0.562 |
| Random Forest Regressor   | 4.50  | 1.35  | 0.556 |
| Neural Network            | 4.26  | 1.29  | 0.580 |
| XGBoost Regressor         | 4.15  | 1.27  | **0.591** |

### **Selected Model: XGBoost**
XGBoost outperformed other models, achieving the highest R² score and the lowest errors.

> **About XGBoost**: XGBoost (Extreme Gradient Boosting) is an ensemble learning algorithm that builds decision trees in a sequential manner. It uses gradient boosting to optimize predictions, making it highly efficient for structured data.

---

## 6. Predictions

The final model successfully generates daily crime predictions, which, while not perfect, provide promising results for such a complex and unpredictable human-driven phenomenon.

![Prediction Visualization](#)

[Link to Full Analysis and Code](https://colab.research.google.com/drive/1dSOnkDZ7m-OWLpnWYC_msWGhMiuH3cis#scrollTo=gLck1iqYxwEg)

---



