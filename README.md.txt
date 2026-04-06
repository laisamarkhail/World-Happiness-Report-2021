# 🌍 World Happiness Report 2021 — Data Analysis

This project analyzes the **World Happiness Report 2021** dataset to explore relationships between happiness scores and key socio-economic indicators such as GDP per capita, life expectancy, social support, freedom, generosity, and corruption perception.

It includes data loading, cleaning, visualization, and exploratory data analysis steps implemented in Python.

---

## 🚀 How to Run

### 1️⃣ Install dependencies

pip install pandas numpy matplotlib seaborn gdown


### 2️⃣ Run the analysis script

python analysis.py


Or open it in **Google Colab**:
👉 [Open in Colab](https://colab.research.google.com/)

---

## 📂 Load & Basics

```python
import gdown

# Replace the ID by yours (everything from /d to /view)
file_id = '1qKLrT6b94vRv3Yug8Fdol1aWYRfok3US'
url = f'https://drive.google.com/uc?id={file_id}'

# Downloading
gdown.download(url, 'fb.csv', quiet=False)

# Read the CSV file
import pandas as pd
df = pd.read_csv('fb.csv')
df.head()
```

---

## 🧹 Step 2 – Exploration, Cleaning & Preprocessing

### 🔍 I. First Checks

```python
# Data types and non-null counts
df.info()

# Missing values
missing_percentage = (df.isnull().sum() / len(df)) * 100
print(missing_percentage)

# Check for duplicate rows
print(df.duplicated().sum())
```

### 📊 II. Data Visualization

```python
%matplotlib inline
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
import pandas as pd

# Rename columns for easier access
df = df.rename(columns={
    "Country name": "Country",
    "Regional indicator": "Region",
    "Ladder score": "Happiness Score",
    "Logged GDP per capita": "GDP per capita",
    "Healthy life expectancy": "Life Expectancy",
    "Social support": "Social Support",
    "Freedom to make life choices": "Freedom",
    "Generosity": "Generosity",
    "Perceptions of corruption": "Corruption"
})

# Drop missing rows
df = df.dropna()
```

#### 🔸 Correlation Heatmap

```python
plt.figure(figsize=(10,6))
sns.heatmap(df[["Happiness Score","GDP per capita","Life Expectancy",
                "Social Support","Freedom","Generosity","Corruption"]].corr(),
            annot=True, cmap="Blues", fmt=".2f")
plt.title("Correlation between Happiness and Other Factors")
plt.show()
```

#### 🔸 GDP vs Happiness

```python
plt.figure(figsize=(8,6))
sns.scatterplot(x="GDP per capita", y="Happiness Score", hue="Region", data=df, alpha=0.8)
plt.title("GDP per Capita vs Happiness Score")
plt.show()
```

#### 🔸 Top 10 Lowest Happiest Countries (2021)

```python
top10 = df.nsmallest(10, "Happiness Score")
plt.figure(figsize=(10,6))
sns.barplot(x="Happiness Score", y="Country", data=top10, palette="viridis")
plt.title("Top 10 Lowest Happiest Countries (2021)")
plt.xlabel("Happiness Score")
plt.ylabel("Country")
plt.show()
```

#### 🔸 Top 10 Happiest Countries (2021)

```python
top10 = df.nlargest(10, "Happiness Score")
plt.figure(figsize=(10,6))
sns.barplot(x="Happiness Score", y="Country", data=top10, palette="viridis")
plt.title("Top 10 Happiest Countries (2021)")
plt.xlabel("Happiness Score")
plt.ylabel("Country")
plt.show()
```

#### 🔸 Distribution of Happiness Scores (2021)

```python
plt.figure(figsize=(10, 6))
sns.histplot(df["Happiness Score"], bins=20, kde=True, color="blue")
plt.title("Distribution of Happiness Scores (2021)", fontsize=14)
plt.xlabel("Happiness Score", fontsize=12)
plt.ylabel("Number of Countries", fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```

---

## 📊 Results Summary

* Strong positive correlation between **GDP per capita** and **Happiness Score**.
* **Social Support** and **Freedom** also show positive relationships with happiness.
* Higher perceived **corruption** tends to reduce happiness levels.
* Most countries’ happiness scores are between 5 and 6.

---

## 🙌 Acknowledgements

* **Dataset:** [World Happiness Report 2021](https://worldhappiness.report/)
* **Libraries:** pandas, seaborn, matplotlib, numpy, gdown
## 📊 Dashboard Preview
[![Dashboard Preview](./assets/dashboard-preview.png)](https://lookerstudio.google.com/reporting/42352692-bf50-4117-8e6d-496d9ca43e06)

## 👤 Authors

**Lais, Aga, Bahador**
