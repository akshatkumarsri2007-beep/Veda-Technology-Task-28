# Veda-Technology-Task-28
# Customer Repeat Purchase Analysis


> **Task 28 | Data Analytics Track | Veda Technology Internship**
> Measuring repeat purchase behaviour and identifying repeat-customer segments in the Online Retail II dataset.

---

---

## Overview

Acquiring a new customer costs far more than retaining an existing one, so understanding **who comes back and how much they are worth** is a core business question. This project analyses transaction data from an online retailer to:

- calculate the **repeat purchase rate**,
- split customers into **loyalty segments**,
- compare the **average order value (AOV)** of first-time and repeat orders,
- turn the findings into **actionable retention recommendations**.

## Objectives and Deliverables

| Deliverable | Description |
|---|---|
| **Repeat rate** | Share of customers who placed 2 or more orders |
| **Segment table** | Customers grouped by order frequency with customers, AOV and revenue share |
| **Insights** | Written findings and recommendations for the business |

**Definition used:** a *repeat customer* is a customer with **2 or more unique invoices**.

## Dataset

**Online Retail II** (UCI Machine Learning Repository): transactions of a UK-based online gift-ware retailer between December 2009 and December 2011.

| Column | Description |
|---|---|
| `Invoice` | Invoice number (starts with `C` for cancellations) |
| `StockCode` | Product code |
| `Description` | Product name |
| `Quantity` | Units per transaction |
| `InvoiceDate` | Date and time of the invoice |
| `Price` | Unit price (GBP) |
| `Customer ID` | Unique customer identifier |
| `Country` | Customer's country |

> **Note:** The file `online_retail_II.csv` in this repository is a **sample dataset with the same schema** as the original, included so the notebook runs out of the box. To reproduce the analysis on the full real data, download Online Retail II from [UCI](https://archive.ics.uci.edu/) or Kaggle and replace the file. Results will differ from the sample numbers shown below.

## Methodology

1. **Load** the data with pandas and parse `InvoiceDate`.
2. **Clean**
   - drop rows with missing `Customer ID`,
   - drop cancellations (`Invoice` starting with `C`),
   - drop rows with non-positive `Quantity` or `Price`,
   - create `Revenue = Quantity x Price`.
3. **Build an order-level table** (one row per invoice) and number each customer's orders by date.
4. **Build a customer-level table** with order count, total spend and AOV, then flag repeat customers.
5. **Segment customers** by number of orders:

   | Segment | Orders |
   |---|---|
   | One-time | 1 |
   | Occasional | 2 to 3 |
   | Regular | 4 to 6 |
   | Loyal | 7 or more |

6. **Compare AOV** between first-time orders and repeat orders.
7. **Measure the time** between a customer's first and second order.

## Key Results

> Results below are from the **sample dataset** (1,500 customers). Replace with your own output if you run the analysis on the full data.

| Metric | Value |
|---|---|
| Customers analysed | 1,500 |
| Repeat customers | 781 |
| **Repeat rate** | **52.07%** |
| Avg. days between 1st and 2nd order | ~45 days |
| First-time order AOV | 77.98 |
| Repeat order AOV | 77.59 |

**Segment table**

| Segment | % of customers | % of revenue |
|---|---|---|
| One-time | 47.9% | 18.2% |
| Occasional (2-3) | 29.3% | 26.5% |
| Regular (4-6) | 15.1% | 27.3% |
| Loyal (7+) | 7.7% | 28.0% |

## Key Insights and Recommendations

**Insights**
- Roughly half of customers buy only once, which is the biggest retention gap.
- Regular and Loyal customers (4+ orders) are about 23% of the base but generate over 55% of revenue.
- AOV is nearly the same for first-time and repeat orders, so loyalty is driven by **purchase frequency, not basket size**.

**Recommendations**
- Send a personalised follow-up offer within about 30 to 40 days of the first purchase.
- Launch a loyalty or VIP programme for Regular and Loyal customers.
- Test bundles, free-shipping thresholds and cross-selling to lift basket size.
- Track repeat rate and time-to-second-order as monthly retention KPIs.

> **Conclusion:** A large share of customers never return, while a small loyal core drives a disproportionate share of revenue. Converting one-time buyers with a timely follow-up offer and rewarding the Regular and Loyal segments is the most effective way to improve retention.
