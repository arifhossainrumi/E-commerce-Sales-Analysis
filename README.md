# 📊 E-commerce Sales Analysis

## 📌 Project Overview
This project analyzes an e-commerce sales dataset to extract meaningful business insights. The goal is to leverage Exploratory Data Analysis (EDA) and forecasting techniques to improve decision-making for inventory management, marketing, and operations.

## 📂 Data Source
- The dataset contains transaction details, including:
  - **Order Date, Ship Date, Customer Segment, Sales, Profit, Discount, Shipping Mode**
- Stored in a **CSV file** and analyzed using **Jupyter Notebook**.

## 🛠️ Data Cleaning & Preprocessing
- **Handled missing values** (imputed or removed where necessary)
- **Converted data types** (e.g., Order Date and Ship Date)
- **Removed duplicates**
- **Created calculated columns** (Processing Time, Sales-to-Profit Ratio)
- **Filtered anomalies and outliers**

## 📈 Exploratory Data Analysis (EDA)

### 1️⃣ Monthly Sales Analysis
#### 📜 Code:
```python
import pandas as pd
import plotly.express as px

data = pd.read_csv("dataset.csv")
sales_by_month = data.groupby('Order Month')['Sales'].sum().reset_index()

fig = px.line(sales_by_month, x='Order Month', y='Sales', title='Monthly Sales Analysis')
fig.show()
```

#### 🖼️ Visualization:
![Monthly Sales Analysis](images/monthly_sales.png)
![image](https://github.com/user-attachments/assets/9af9847b-7fab-4e18-8388-d49325bd6489)

#### 📊 Insights:
- Sales fluctuate throughout the year, showing both growth and decline phases.
- There is a significant increase around March, peaking above 200K.
- Sales recover strongly in September, with a sharp rise towards the year’s end.
- **Key Takeaways:**
  - Seasonal trends exist, with notable peaks in March, September, and November.
  - Businesses can leverage high-demand months with promotions and stock planning.

### 2️⃣ Profit Analysis by Category
#### 📜 Code:
```python
profit_by_category = data.groupby('Category')['Profit'].sum().reset_index()
fig = px.pie(profit_by_category, values='Profit', names='Category', title='Profit Analysis by Category')
fig.show()
```

#### 🖼️ Visualization:
![Profit by Category](images/profit_by_category.png)

#### 📊 Insights:
- **Technology** contributes the most to profit (~50.8%).
- **Office Supplies** follows at 42.8%, indicating steady demand.
- **Furniture** lags behind with only 6.4%.
- **Key Takeaways:**
  - Technology and Office Supplies should be prioritized for maximizing profits.
  - Furniture needs further investigation—pricing adjustments or cost reduction might be required.

### 3️⃣ Sales Forecasting Using Exponential Smoothing
#### 📜 Code:
```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing
import matplotlib.pyplot as plt

data['Order Date'] = pd.to_datetime(data['Order Date'])
data.set_index('Order Date', inplace=True)
sales_data = data.resample('M').sum()

model = ExponentialSmoothing(sales_data['Sales'], trend='add', seasonal='add', seasonal_periods=12).fit()
sales_data['Forecast'] = model.predict(start=sales_data.index[0], end=sales_data.index[-1])

plt.figure(figsize=(12, 6))
plt.plot(sales_data.index, sales_data['Sales'], label="Actual Sales", marker='o')
plt.plot(sales_data.index, sales_data['Forecast'], label="Forecasted Sales", linestyle="dashed")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.title("Sales Forecasting using Exponential Smoothing")
plt.legend()
plt.show()
```

#### 🖼️ Visualization:
![Sales Forecast](images/sales_forecast.png)

#### 📊 Insights:
- The forecasted values align with actual sales trends.
- Clear seasonal patterns exist, with peaks and dips at regular intervals.
- **Key Takeaways:**
  - Seasonal forecasting helps in stock optimization and marketing strategy planning.
  - The model needs fine-tuning to improve prediction accuracy.

## ✅ Recommendations
1. **Optimize inventory** based on peak demand months.
2. **Adjust discount strategies** to prevent profit erosion.
3. **Improve order fulfillment** to reduce shipping delays.
4. **Encourage faster shipping modes** to improve customer experience.
5. **Refine forecasting models** for better business predictions.

## 🖥️ Technologies Used
- **Python** (Pandas, NumPy, Matplotlib, Seaborn, Statsmodels, Plotly, Scikit-learn)
- **Jupyter Notebook**
- **Time Series Forecasting (Exponential Smoothing)**

## 📂 Repository Structure
```
📂 E-commerce-Sales-Analysis
│── 📜 README.md  # Project Overview
│── 📜 dataset.csv  # Raw data file
│── 📜 e_commerce_analysis.ipynb  # Jupyter Notebook with full analysis
│── 📂 images/  # Visualizations from EDA
│── 📂 results/  # Processed data and outputs
```

## 📢 How to Use
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/E-commerce-Sales-Analysis.git
   ```
2. Open Jupyter Notebook and run `e_commerce_analysis.ipynb`.
3. Load `dataset.csv` and explore the insights.

## 📧 Contact
For questions or collaborations, feel free to reach out via [GitHub Issues](https://github.com/your-username/E-commerce-Sales-Analysis/issues).

---

🚀 **Happy Analyzing!** 🎯
