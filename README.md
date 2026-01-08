## Table of Contents

- [Tools & Technologies](#tools--technologies)
- [Datasets Used](#datasets-used)
- [Business Questions Addressed](#business-questions-addressed)
- [Key Outcomes](#key-outcomes)
- [Dashboards](#https://github.com/karthic180/analytics-and-reporting/tree/main#-dashboards)
  - [Executive Sales Performance Dashboard](https://github.com/karthic180/analytics-and-reporting/edit/main/README.md#-executive-sales-performance-dashboard)
  - [Customer Profitability & Segmentation Dashboard](https://github.com/karthic180/analytics-and-reporting/edit/main/README.md#-customer-profitability--segmentation-dashboard)
- [DAX Measures & Semantic Layer](#dax-measures--semantic-layer)
  - [Core Measures](#core-measures)
  - [Profitability & Margin Measures](#profitability--margin-measures)
  - [Time Intelligence Measures](#time-intelligence-measures)
  - [Operational & Segmentation Measures](#operational--segmentation-measures)

##  Tools & Technologies

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat\&logo=powerbi\&logoColor=black)
![SQL](https://img.shields.io/badge/SQL%20\(T--SQL\)-4479A1?style=flat\&logo=microsoftsqlserver\&logoColor=white)
![Data Modeling](https://img.shields.io/badge/Data%20Modelling-Star%20Schema-00599C?style=flat)
![GitHub](https://img.shields.io/badge/GitHub-Version%20Control-181717?style=flat\&logo=github)
![Documentation](https://img.shields.io/badge/Documentation-Stakeholder%20Ready-4CAF50?style=flat)

---

##  Datasets Used

![Open Data](https://img.shields.io/badge/Data-Open%20Source-2E7D32?style=flat)
![Kaggle](https://img.shields.io/badge/Source-Kaggle-20BEFF?style=flat\&logo=kaggle\&logoColor=white)

**Primary Dataset**

* **Superstore Sales Dataset (Retail Transactions)**
  Source: Kaggle
  [https://www.kaggle.com/datasets/vivek468/superstore-dataset-final](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

**Dataset Characteristics**

* Transaction-level retail sales data
* Includes sales, profit, discount, quantity, shipping, geography, and product hierarchy
* Widely used for analytics, BI modelling, and profitability analysis
* No customer-identifiable or proprietary data


---

## Business Questions Addressed

* What are the key revenue and profit trends over time?
* Which products, segments, and regions drive sustainable profitability?
* Where are discounts eroding margins?
* Which operational choices (shipping modes, regions) impact profit most?
* Where do revenue and profitability diverge?

---

## Key Outcomes

* Delivered executive-ready dashboards with clear KPIs and drill-down capability
* Designed a logical star-schema semantic model for scalable reporting
* Identified unprofitable product sub-categories despite high sales volume
* Highlighted margin erosion caused by aggressive discounting strategies
* Enabled data-driven conversations around operational efficiency

---

## 📊 Dashboards

---

### 📈 Executive Sales Performance Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=flat)
![KPI](https://img.shields.io/badge/KPIs-Executive%20Level-4CAF50?style=flat)
![Data Model](https://img.shields.io/badge/Data%20Model-Star%20Schema-00599C?style=flat)

 **PDF:**
[View Dashboard](https://github.com/karthic180/analytics-and-reporting/blob/main/Executive%20Sales%20Performance%20Dashboard.pdf)

#### Business Questions Answered

* How is overall sales and profit trending over time?
* Which regions and segments contribute most to revenue?
* Where are top-line and bottom-line performance misaligned?

#### Key Insights

* Revenue growth is not always aligned with profit growth across regions
* Certain regions outperform in volume but underperform in margin
* Segment-level analysis reveals differing profit efficiencies

---

### 📊 Customer Profitability & Segmentation Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Advanced%20Analytics-F2C811?style=flat)
![Profitability](https://img.shields.io/badge/Focus-Profitability-FF6F00?style=flat)
![Segmentation](https://img.shields.io/badge/Analysis-Segmentation-9C27B0?style=flat)

 **PDF:**
[View Dashboard](https://github.com/karthic180/analytics-and-reporting/blob/main/Customer%20Profitability%20Segmentation%20Dash.pdf)

#### Business Questions Answered

* Which customer segments are truly profitable?
* Which product categories and sub-categories generate losses?
* How does discounting impact overall margin?
* Do shipping modes influence profitability?
* Where are geographic margin risks concentrated?

#### Key Insights

* High-discount transactions significantly reduce overall profitability
* Several high-revenue sub-categories operate at negative margins
* Shipping mode selection has a measurable impact on profit
* Certain regions consistently underperform despite strong sales volume

---

##  DAX Measures & Semantic Layer

![DAX](https://img.shields.io/badge/DAX-Semantic%20Model-512BD4?style=flat\&logo=microsoft\&logoColor=white)
![Measures](https://img.shields.io/badge/Measures-Business%20Logic-4CAF50?style=flat)
![Performance](https://img.shields.io/badge/Optimised-Yes-2E7D32?style=flat)



###  Core Measures

```DAX
Total Sales =
SUM ( Fact_Sales[Sales] )

Total Profit =
SUM ( Fact_Sales[Profit] )

Total Quantity =
SUM ( Fact_Sales[Quantity] )

Average Discount =
AVERAGE ( Fact_Sales[Discount] )
```

---

###  Profitability & Margin Measures

```DAX
Profit Margin % =
DIVIDE ( [Total Profit], [Total Sales], 0 )

Discounted Sales =
CALCULATE (
    [Total Sales],
    Fact_Sales[Discount] > 0
)

Non-Discounted Sales =
CALCULATE (
    [Total Sales],
    Fact_Sales[Discount] = 0
)
```

---

###  Time Intelligence Measures

(Using a dedicated Date dimension)

```DAX
Sales YTD =
TOTALYTD (
    [Total Sales],
    Dim_Date[Date]
)

Profit YTD =
TOTALYTD (
    [Total Profit],
    Dim_Date[Date]
)

Sales YoY % =
VAR PrevYearSales =
    CALCULATE (
        [Total Sales],
        SAMEPERIODLASTYEAR ( Dim_Date[Date] )
    )
RETURN
DIVIDE ( [Total Sales] - PrevYearSales, PrevYearSales, 0 )
```

---

###  Operational & Segmentation Measures

```DAX
Average Order Value =
DIVIDE ( [Total Sales], [Total Quantity], 0 )

Profit per Unit =
DIVIDE ( [Total Profit], [Total Quantity], 0 )

High Discount Flag =
IF (
    AVERAGE ( Fact_Sales[Discount] ) > 0.2,
    "High Discount",
    "Standard"
)
```
