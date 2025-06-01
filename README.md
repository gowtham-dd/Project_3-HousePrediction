


# Individual Household Electric Power Consumption: Data Exploration and Understanding

## 📊 Project Overview

This project involves data exploration and understanding of the **Individual Household Electric Power Consumption** dataset from the UCI Machine Learning Repository. The aim is to clean the data, handle missing values, convert data types, and conduct exploratory data analysis (EDA) to understand consumption patterns and correlations between electrical features over time.

---

## 📦 Dataset Information

- **Source**: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption)
- **Dataset ID**: `235`
- **Total Entries**: `2,075,259` rows and `9` columns
- **Duration**: December 2006 to November 2010

---

## ⚙️ Installation

Install the required package to fetch the dataset:

```bash
pip install ucimlrepo
```

---

## 📥 Data Fetching

Using `ucimlrepo`, the dataset was fetched directly:

```python
from ucimlrepo import fetch_ucirepo
dataset = fetch_ucirepo(id=235)
X = dataset.data.features
```

---

## 🧹 Data Cleaning & Preprocessing

Steps performed:

1. **Missing Values Handling**:  
   - Replaced `?` with NaN and converted columns to numeric.
   - Dropped rows with missing values.

2. **Datetime Creation**:  
   - Merged `Date` and `Time` columns into a single `Datetime` column.
   - Set `Datetime` as the index for time-series analysis.

3. **Dropped Unnecessary Columns**:
   - Removed original `Date` and `Time` columns after conversion.

```python
data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'], format='%d/%m/%Y %H:%M:%S')
data.set_index('Datetime', inplace=True)
data.drop(['Date', 'Time'], axis=1, inplace=True)
```

---

## 📈 Exploratory Data Analysis (EDA)

1. **Basic Summary Stats**:
   - Used `.info()` and `.describe()` to understand distributions.

2. **Missing Values Check**:
   - Verified there were no missing values after cleaning.

3. **Line Plot: Global Active Power Over Time**:
   - Helps identify trends, patterns, or seasonality in power consumption.

```python
import matplotlib.pyplot as plt
plt.figure(figsize=(15, 5))
data['Global_active_power'].plot()
plt.title('Global Active Power Over Time')
plt.ylabel('Kilowatts')
plt.show()
```

4. **Correlation Matrix**:
   - Used `seaborn` heatmap to visualize feature relationships.

```python
import seaborn as sns
plt.figure(figsize=(10, 8))
sns.heatmap(data.corr(), annot=True, fmt=".2f", cmap='coolwarm')
plt.title("Correlation Matrix")
plt.show()
```

---

## 📐 Dataset Statistics

- Final Cleaned Dataset:  
  `2,049,280` rows × `7` columns
- All columns successfully converted to `float64`.
- No null values remaining after cleaning.

---

## 🔍 Observations

- `Global_active_power` shows distinct patterns over time.
- `Global_intensity` correlates positively with `Global_active_power`.
- Sub-meterings are generally sparse but provide granular insight into household energy usage distribution.

---

## ✅ Future Work (Optional)

- Time series modeling (ARIMA, Prophet)
- Anomaly detection
- Seasonal decomposition
- Energy consumption forecasting
- Dashboard or Streamlit app for visualization

---

---

Would you like me to include an optional section on model training or time-series forecasting if you're planning to continue this analysis?
