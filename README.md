import pandas as pd
import plotly.express as px
import plotly.graph_objects as go

# 1. Data Loading
# Load your dataset (assuming a CSV format based on the report)
df = pd.read_csv('adidas_sales_data.csv')

# 2. Revenue by Store Type (Bar Chart)
# [cite: 5, 11, 12, 13, 14]
store_revenue = df.groupby('Type')['Total_Revenue'].sum().reset_index()
fig_store = px.bar(store_revenue, x='Type', y='Total_Revenue', title="Revenue by Store Type")

# 3. Category Distribution (Donut Chart)
# [cite: 4, 20, 33, 41]
category_rev = df.groupby('Category')['Total_Revenue'].sum().reset_index()
fig_cat = px.pie(category_rev, values='Total_Revenue', names='Category', hole=0.4, title="Revenue by Category")

# 4. Top 5 Products (Table/Bar)
# [cite: 24, 25, 28, 29, 30, 31, 32]
top_products = df.groupby('Product_Name')['Total_Revenue'].sum().nlargest(5).reset_index()
fig_prod = px.bar(top_products, x='Total_Revenue', y='Product_Name', orientation='h', title="Top 5 Products")

# 5. Monthly Revenue and Profit Trends (Area Chart)
# [cite: 22]
# Assuming a 'Date' column exists in the dataset
trend_data = df.groupby('Date')[['Total_Revenue', 'Total_Profit']].sum().reset_index()
fig_trend = go.Figure()
fig_trend.add_trace(go.Scatter(x=trend_data['Date'], y=trend_data['Total_Revenue'], fill='tozeroy', name='Revenue'))
fig_trend.add_trace(go.Scatter(x=trend_data['Date'], y=trend_data['Total_Profit'], fill='tozeroy', name='Profit'))
fig_trend.update_layout(title="Monthly Revenue and Profit Trends")

# 6. Regional Sales (Data Frame/Table)
# [cite: 27, 37, 39, 42, 44, 46]
region_rev = df.groupby('Region')['Total_Revenue'].sum().reset_index()
print(region_rev)
