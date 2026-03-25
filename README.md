# 📊 Commodity Investment Dashboard (Gold & Silver Analysis) #

## 📌 Overview

This project builds an end-to-end analytical pipeline to evaluate **investment performance of gold and silver**, separating **true asset returns** from **currency (USD/EGP) impact**.

The goal is to help decision-makers answer a critical question:

> **Which commodity is the better investment, considering both return and risk?**

---

## ⚙️ Project Pipeline

### 1. Data Collection 

A Python script (`scrape_data.py`) is used to collect historical data:

* Gold prices (USD per ounce)
* Silver prices (USD per ounce)
* USD to EGP exchange rates

#### Key Responsibilities:

* Scrape financial data from online sources
* Clean and normalize datasets
* Export structured data (CSV/Excel)

#### Technologies:

* Python
* Pandas
* Requests / BeautifulSoup (or Selenium if used)

---

### 2. Data Modeling (Power BI)

Data is imported into Power BI and structured using a **star schema**:

### Tables:

* `Dim_Date` → Central date table
* `gold_prices` → Gold price (USD)
* `silver_prices` → Silver price (USD)
* `USD_EGP Historical Data` → Exchange rate

### Relationships:

* All fact tables connect to `Dim_Date`
* No direct relationship between commodities and FX (handled via DAX)

---

## 🧠 Core Calculations (DAX)

### 1. Price Conversion (USD → EGP)

Gold and silver prices are converted dynamically:

```
Gold Price EGP =
SUMX(
    gold_prices,
    gold_prices[price] *
    CALCULATE(
        MAX('USD_EGP Historical Data'[Price]),
        TREATAS(
            VALUES(gold_prices[date]),
            'USD_EGP Historical Data'[Date]
        )
    )
)
```

---

### 2. Total Return %

```
Total Return % =
(End Price - Start Price) / Start Price
```

Calculated dynamically based on slicer-selected date range.

---

### 3. Currency Impact

```
Currency Impact % =
Return (EGP) - Return (USD)
```

This separates:

* Real asset performance
* Currency-driven gains

---

### 4. Volatility (Risk Measurement)

```
Volatility =
STDEVX.P(
    VALUES(Date),
    Daily Returns
)
```

Used to measure investment risk.

---

### 5. Risk-Adjusted Return

```
Risk Adjusted Return =
Return % / Volatility
```

Used to compare assets fairly.

---

## 📊 Dashboard Pages

### 🔹 Overview Page

Provides a high-level comparison:

* Gold Total Return %
* Silver Total Return %
* Best Performer
* Best Risk-Adjusted Asset
![App Demo](images/demo.gif)
Charts:

* Normalized Performance (Base = 100)
* Gold vs Silver price trends

---

### 🟡 Gold Analysis Page

Focus: Gold investment performance

KPIs:

* Total Return (USD)
* Total Return (EGP)
* Currency Impact %
* Volatility

Charts:

* Gold price (USD)
* Gold price (EGP)
* USD/EGP exchange rate
* Combined USD vs EGP comparison
![App Demo](images/demo.gif)
---

### ⚪ Silver Analysis Page

Same structure as gold for direct comparison.
![App Demo](images/demo.gif)
---

## 🎯 Key Insights Delivered

This dashboard enables users to:

* Distinguish between **real commodity growth** and **currency-driven gains**
* Compare **gold vs silver performance**
* Evaluate **risk vs return**
* Identify the **better investment option**

---

## 🚀 Tools & Technologies

* Python (Data Scraping & Processing)
* Power BI (Data Modeling & Visualization)
* DAX (Advanced Calculations)
* Excel (Optional preprocessing)

---

## 📈 Business Value

This project demonstrates:

* End-to-end data pipeline design
* Financial analytics (returns, volatility, risk-adjusted metrics)
* Real-world investment decision modeling
* Advanced Power BI and DAX skills

---

## 📎 Future Improvements

* Add more commodities (oil, platinum, etc.)
* Integrate real-time APIs
* Include predictive modeling (ML)
* Portfolio optimization features

---

## 👤 Author

Hassan Yasser
Data Analyst / Analytical Engineer
