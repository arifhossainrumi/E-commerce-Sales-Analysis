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
sales_by_month = data.groupby('Order Month')['Sales'].sum().reset_index()
fig = px.line(sales_by_month, x='Order Month', y='Sales', title='Monthly Sales Analysis')
fig.show()
```

#### 🖼️ Visualization:
![Monthly Sales Analysis](images/monthly_sales.png)

#### 📊 Insights:
- Sales peak in March, September, and November.
- There is a mid-year slump in April–July.
- **Action:** Plan promotions during peak months.

### 2️⃣ Sales by Category
#### 📜 Code:
```python
sales_by_category = data.groupby('Category')['Sales'].sum().reset_index()
fig = px.pie(sales_by_category, values='Sales', names='Category', title='Sales by Category')
fig.show()
```

#### 🖼️ Visualization:
![Sales by Category](images/sales_by_category.png)

#### 📊 Insights:
- Technology leads sales (36.4%), followed by Furniture and Office Supplies.
- **Action:** Focus marketing on high-selling categories.

### 3️⃣ Sales by Sub-Category
#### 📜 Code:
```python
sales_by_subcategory = data.groupby('Sub-Category')['Sales'].sum().reset_index()
fig = px.bar(sales_by_subcategory, x='Sub-Category', y='Sales', title='Sales by Sub-Category')
fig.show()
```

#### 🖼️ Visualization:
![Sales by Sub-Category](images/sales_by_subcategory.png)

#### 📊 Insights:
- Chairs & Phones have the highest sales.
- Art, Fasteners, and Labels show low demand.

### 4️⃣ Profit Analysis by Category
#### 📜 Code:
```python
profit_by_category = data.groupby('Category')['Profit'].sum().reset_index()
fig = px.pie(profit_by_category, values='Profit', names='Category', title='Profit by Category')
fig.show()
```

#### 🖼️ Visualization:
![Profit by Category](images/profit_by_category.png)

#### 📊 Insights:
- Technology contributes the most profit (50.8%).
- Furniture has the lowest profit margin.

### 5️⃣ Customer Segment Analysis
#### 📜 Code:
```python
sales_profit_by_segment = data.groupby('Segment').agg({'Sales': 'sum', 'Profit': 'sum'}).reset_index()
fig = px.bar(sales_profit_by_segment, x='Segment', y=['Sales', 'Profit'], barmode='group', title='Sales and Profit by Customer Segment')
fig.show()
```

#### 🖼️ Visualization:
![Customer Segment](images/customer_segment.png)

#### 📊 Insights:
- Consumer segment generates the highest sales.
- Corporate customers yield higher profit ratios.

### 6️⃣ Sales Forecasting Using Exponential Smoothing
#### 📜 Code:
```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing
sales_data = data.resample('M', on='Order Date').sum()
model = ExponentialSmoothing(sales_data['Sales'], trend='add', seasonal='add', seasonal_periods=12).fit()
sales_data['Forecast'] = model.predict(start=sales_data.index[0], end=sales_data.index[-1])
fig = px.line(sales_data, x=sales_data.index, y=['Sales', 'Forecast'], title='Sales Forecasting')
fig.show()
```

#### 🖼️ Visualization:
![Sales Forecast](images/sales_forecast.png)

#### 📊 Insights:
- Forecasting aligns with sales trends, showing seasonal patterns.

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
