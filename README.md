# 🛒 Walmart Retail Analytics Dashboard — Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-00B894?style=for-the-badge)

A comprehensive 6-page interactive retail analytics dashboard built in Power BI, analyzing Walmart sales, inventory, forecasting, customer behavior, and promotion effectiveness.

---

## 📊 Dashboard Pages

| Page | Title | Key Visual |
|------|-------|-----------|
| 1 | ⚡ Executive Overview | KPI Cards, Revenue Trend, Payment Donut |
| 2 | 🔬 Sales Deep Dive | Matrix Heatmap, Scatter Plot, Combo Chart |
| 3 | 📦 Inventory & Supply Chain | Traffic Light Table, Lead Time Chart |
| 4 | 🎯 Forecast vs Actual | MAPE Accuracy, Diverging Matrix |
| 5 | 👥 Customer Insights | Age Histogram, Loyalty Scatter |
| 6 | 🎁 Promotions Analysis | 100% Stacked Bar, Promo Lift Cards |

---

## 🔍 Key Insights

### 🚨 Critical Findings
- **51.86% Stockout Rate** — over half of all transactions experienced stockouts
- **54.02% Forecast Accuracy** — well below the 70% industry benchmark
- **All products at CRITICAL stock status** across all 5 store locations

### 💰 Revenue
- Total Revenue: **$15M** | Transactions: **5K** | Avg Order Value: **$3.05K**
- Electronics ($7.9M) slightly outperforms Appliances ($7.3M)
- Promotions generate **11.96% revenue lift**

### 👥 Customers
- **50-64 age group** drives the most transactions
- **Platinum members** generate highest revenue ($4.0M)
- Payment methods evenly split (~25% each)

---

## 🛠 Technical Details

### DAX Measures Created
```dax
-- Revenue Measures
Total Revenue = SUMX('Walmart_Orders', 'Walmart_Orders'[quantity_sold] * 'Walmart_Orders'[unit_price])
Revenue With Promo = CALCULATE([Total Revenue], 'Walmart_Orders'[promotion_applied] = TRUE())
Promo Lift % = DIVIDE([Revenue With Promo] - [Revenue Without Promo], [Revenue Without Promo])

-- Forecast Measures  
Forecast Accuracy = 1 - DIVIDE(SUMX('Walmart_Orders', ABS('Walmart_Orders'[actual_demand] - 'Walmart_Orders'[forecasted_demand])), SUM('Walmart_Orders'[actual_demand]))
Variance % = DIVIDE([Forecast Variance], SUM('Walmart_Orders'[forecasted_demand]))

-- Inventory Measures
Stockout Rate = DIVIDE(COUNTROWS(FILTER('Walmart_Orders', 'Walmart_Orders'[stockout_indicator] = TRUE())), COUNTROWS('Walmart_Orders'))
Critical Reorder Qty = CALCULATE(SUM('Walmart_Orders'[reorder_quantity]), 'Walmart_Orders'[Stock Status] = "🔴 Critical")
```

### Calculated Columns
```dax
Stock Status = IF('Walmart_Orders'[inventory_level] < 'Walmart_Orders'[reorder_point], "🔴 Critical", IF('Walmart_Orders'[inventory_level] < 'Walmart_Orders'[reorder_point] * 1.2, "🟡 Warning", "🟢 Safe"))

Age Group = SWITCH(TRUE(), 'Walmart_Orders'[customer_age] < 25, "18-24", 'Walmart_Orders'[customer_age] < 35, "25-34", 'Walmart_Orders'[customer_age] < 50, "35-49", 'Walmart_Orders'[customer_age] < 65, "50-64", "65+")

Supplier Group = IF('Walmart_Orders'[supplier_lead_time] > 7, "Slow Supplier", "Fast Supplier")
```

---

## 📁 Repository Structure

```
walmart-powerbi-dashboard/
│
├── 📊 Walmart_Dashboard.pbix       # Main Power BI file
├── 📄 Walmart_Orders.csv           # Raw dataset
├── 📸 screenshots/
│   ├── page1_executive_overview.png
│   ├── page2_sales_deep_dive.png
│   ├── page3_inventory.png
│   ├── page4_forecast.png
│   ├── page5_customers.png
│   └── page6_promotions.png
├── 📝 DAX_Measures.md              # All DAX formulas documented
└── 📖 README.md
```

---

## 🚀 How to Use

1. Clone this repository
```bash
git clone https://github.com/YOUR_USERNAME/walmart-powerbi-dashboard.git
```

2. Open `Walmart_Dashboard.pbix` in Power BI Desktop
3. If data doesn't load: Home → Transform Data → update file path to your CSV location
4. Explore all 6 pages using the page tabs at the bottom

---

## 📋 Dataset Columns

| Column | Description |
|--------|-------------|
| transaction_id | Unique transaction identifier |
| customer_id | Customer identifier |
| product_name | Product sold |
| category | Electronics or Appliances |
| quantity_sold | Units sold per transaction |
| unit_price | Price per unit |
| transaction_date | Date of transaction |
| store_location | One of 5 US cities |
| inventory_level | Current stock level |
| reorder_point | Minimum stock threshold |
| supplier_lead_time | Days for supplier to deliver |
| customer_age | Customer age |
| customer_gender | Customer gender |
| customer_income | Annual income |
| customer_loyalty_level | Bronze/Silver/Gold/Platinum |
| payment_method | Payment type used |
| promotion_applied | Whether promotion was used |
| promotion_type | BOGO/Percentage Discount/None |
| weather_conditions | Weather on transaction day |
| holiday_indicator | Whether transaction was on holiday |
| stockout_indicator | Whether item was out of stock |
| forecasted_demand | Predicted demand |
| actual_demand | Real demand |

---

## 👤 Author

**[Omar Moussa]**
- LinkedIn: [www.linkedin.com/in/omar-moussa-a9121523b]
- GitHub: [(https://github.com/omarmoussa724)]

---

## ⭐ If you found this useful, please star the repository!
