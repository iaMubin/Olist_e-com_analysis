# Olist E-Commerce Business Analysis

| Field | Value |
|---|---|
| **Author** | Mubin |
| **Domain** | E-commerce / Data Science |
| **Python** | 3.13.5 |
| **Data Source** | [Olist Brazilian E-Commerce (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) |

**Tools:** Python · Pandas · NumPy · Seaborn · Matplotlib · Folium

---

## Project Objective

Analyze the Olist E-commerce dataset to derive **actionable business insights**, focusing on:

1. **Logistics Performance** — Identifying delays and shipping issues.
2. **Customer Segmentation** — Finding high-value customers using RFM.
3. **Sales Trends** — Understanding seasonality and peak hours.
4. **Product Quality** — Spotting low-rated categories and improvement opportunities.

---

## Table of Contents

1. [Environment Setup & Data Loading](#1-environment-setup--data-loading)
2. [Dataset Overview & Data Quality](#2-dataset-overview--data-quality)
3. [Sales Trend & Temporal Analysis](#3-sales-trend--temporal-analysis)
4. [Delivery Performance & Logistics](#4-delivery-performance--logistics-analysis)
5. [Customer Segmentation (RFM)](#5-customer-segmentation-rfm-analysis)
6. [Product Quality Analysis](#6-product-quality-analysis)
7. [Payment Behaviour Analysis](#7-payment-behaviour-analysis)
8. [Seller Analysis](#8-seller-analysis)
9. [Regional & Geospatial Analysis](#9-regional-analysis-revenue-volume--freight-costs)
10. [Conclusions & Strategic Recommendations](#final-executive-verdict)

---

## 1. Environment Setup & Data Loading

- Import core libraries (pandas, numpy, matplotlib, seaborn, folium).
- Set global constants (e.g. `RANDOM_STATE`, `DATA_PATH`).
- Configure display and plotting defaults.
- Load and validate all Olist E-commerce CSV datasets.

**Reproducibility:** Place the Olist CSVs in the `data/` directory and install dependencies:

```bash
pip install -r requirements-olist.txt
```

### Datasets Used

| File | Description |
|---|---|
| `olist_orders_dataset.csv` | Order-level data (status, timestamps) |
| `olist_order_items_dataset.csv` | Line-item details (price, freight, seller) |
| `olist_customers_dataset.csv` | Customer location and IDs |
| `olist_products_dataset.csv` | Product attributes |
| `olist_order_payments_dataset.csv` | Payment method and installments |
| `olist_order_reviews_dataset.csv` | Customer review scores and comments |
| `olist_sellers_dataset.csv` | Seller location data |
| `olist_geolocation_dataset.csv` | Lat/lng by zip code prefix |
| `product_category_name_translation.csv` | Portuguese → English category names |

---

## 2. Dataset Overview & Data Quality

Schema inspection, dtypes, non-null counts, and missing-value analysis for each table. Order status distribution is summarized to understand the business mix.

---

## 3. Sales Trend & Temporal Analysis

### Monthly Sales Trend & Seasonality

Revenue is resampled monthly to identify growth patterns and seasonality. Data from the initial launch phase (2016) and incomplete September 2018 records are excluded for accuracy.

### Sales Heatmap

A heatmap of orders by **day of week × hour of day** pinpoints when customers are most active, informing marketing and staffing decisions.

---

## 4. Delivery Performance & Logistics Analysis

### On-Time Delivery Rate

A pie chart compares orders delivered on time vs. late (actual vs. estimated delivery date).

### Average Delivery Time by State

Bar chart ranking Brazilian states by mean delivery days, revealing regional logistics gaps.

### Late Delivery Rate by State

Percentage of late deliveries per state — a failure-analysis metric that surfaces high-risk regions.

### Worst Performing Sellers

Sellers who consistently miss shipping deadlines are identified by comparing `order_approved_at` to `order_delivered_carrier_date`.

### Impact of Late Delivery on Customer Satisfaction

Average review scores for on-time vs. late orders quantify the reputational cost of logistics failures.

### Sentiment Analysis Validation

NLP-based polarity scoring (TextBlob) on review comments confirms the negative sentiment associated with late deliveries.

---

## 5. Customer Segmentation (RFM Analysis)

Customers are segmented by **Recency**, **Frequency**, and **Monetary** value:

| Segment | RFM Score |
|---|---|
| Champions (VIP) | ≥ 12 |
| Loyal Customers | ≥ 10 |
| Needs Attention | ≥ 6 |
| At Risk | < 6 |

A treemap visualizes the distribution across segments.

---

## 6. Product Quality Analysis

Review scores are merged with product category translations to rank the **lowest-rated categories**, highlighting quality-control priorities.

---

## 7. Payment Behaviour Analysis

### Preferred Payment Methods

- **Credit Card** dominates at ~74%.
- **Boleto** accounts for ~19%, reflecting Brazil's cash-based digital payment culture.

### Average Order Value (AOV)

Order value distributions and AOV comparisons across payment types and installment vs. single-payment orders.

### Credit Card Installment Distribution

Focused analysis of installment plan preferences among credit-card users.

---

## 8. Seller Analysis

### Top Sellers

Top 10 sellers by order count and by total revenue.

### Seller Concentration

~20% of sellers generate ~80% of total revenue — a classic Pareto distribution that signals business-concentration risk.

---

## 9. Regional Analysis: Revenue, Volume & Freight Costs

1. **Total Revenue by State** — Identifies the most profitable regions.
2. **Sales Volume by State** — Measures customer demand density.
3. **Average Freight Cost by State** — Evaluates shipping affordability.
4. **Geospatial Customer Density** — Scatterplot and interactive Folium heatmap of customer locations across Brazil.
5. **Customers-per-Seller Ratio** — Highlights supply-gap opportunities for new seller recruitment.

---

## Final Executive Verdict

### Elevator Pitch

> Olist demonstrates strong market demand but is constrained by operational inefficiencies. Sustainable profitability will not come from further user acquisition alone, but from resolving logistics failures in remote regions and improving retention of high-value customers.

### Strategic Action Plan

| Pillar | Problem | Action |
|---|---|---|
| **Optimize Operational Resilience** | Regional logistic bottlenecks and quality failures drive customer attrition. | Enforce a "Three-Strike Policy" for underperforming sellers; renegotiate SLAs in high-latency zones. |
| **Focus on High-Value Customers** | ~96% of customers make only a single purchase. | Shift spend from mass acquisition to retention campaigns targeting high-RFM segments during peak hours. |
| **Expand Selectively** | Some regions have high demand but insufficient local sellers. | Recruit local sellers in states with elevated Customers-per-Seller ratios. |

**Conclusion:** Long-term profitability depends on operational discipline — address logistics failures, retain high-value customers, and expand only where supply and demand are structurally aligned.

---

## Repository Structure

```
├── Olist_Ecommerce_Analysis.ipynb   # Main analysis notebook
├── Olist_Ecommerce_Analysis.pdf     # PDF export of the notebook
├── requirements-olist.txt           # Python dependencies
├── data/                            # Raw Olist CSV datasets
├── analytical_data/                 # Exported summary tables (Excel)
├── all_PLOTS/                       # Saved plot images & PDF
└── Olist_Ecommerce_Analysis_files/  # Notebook-embedded plot images
```

## Getting Started

```bash
# Clone the repository
git clone https://github.com/iaMubin/Olist_e-com_analysis.git
cd Olist_e-com_analysis

# Install dependencies
pip install -r requirements-olist.txt

# Open the notebook
jupyter notebook Olist_Ecommerce_Analysis.ipynb
```
