# Retail Territory Margin Analysis | SQL

**Tools:** SQL (SQLite) | **Dataset:** 9,995 orders across US states | **Focus:** Territory profitability & margin risk

---

## Business Question

> *Which US territories are most and least profitable — and what is driving the gap?*

---

## Dataset

| Column | Description |
|---|---|
| `Order ID` | Unique order identifier |
| `Sales` | Revenue per order |
| `Profit` | Profit per order |
| `Shipping Cost Per Unit` | Shipping cost |
| `Net_Margin_pct` | Net margin as a percentage |
| `State` | US state |
| `Conversion_Flag` | Whether order converted |

- **9,995 rows** across multiple US states
- Merged from 3 source files

---

## SQL Queries & Findings

### Query 1 — Average margin by state

```sql
SELECT State, 
       ROUND(AVG(Net_Margin_pct), 2) AS avg_margin,
       COUNT("Order ID") AS total_orders
FROM retail
GROUP BY State
ORDER BY avg_margin DESC
```

**Top performing states by margin:**

| State | Avg Margin | Total Orders |
|---|---|---|
| District of Columbia | 42.20% | 10 |
| Iowa | 39.93% | 30 |
| Arkansas | 37.95% | 60 |
| South Dakota | 37.75% | 12 |

**Insight:** Highest margin states are all low volume — suggesting untapped growth potential in profitable markets.

---

### Query 2 — Low margin orders by state (below 10%)

```sql
SELECT State,
       COUNT("Order ID") AS low_margin_orders
FROM retail
WHERE Net_Margin_pct < 10
GROUP BY State
ORDER BY low_margin_orders DESC
```

**Most problematic states:**

| State | Low Margin Orders |
|---|---|
| Texas | 585 |
| California | 378 |
| Pennsylvania | 331 |
| Illinois | 310 |
| Ohio | 257 |

**Insight:** Texas alone accounts for 585 low margin orders — nearly double California. These are high volume states where pricing or shipping costs are severely eroding profitability.

---

### Query 3 — Total sales, profit and margin by state

```sql
SELECT State,
       ROUND(SUM(Sales), 2) AS total_sales,
       ROUND(SUM(Profit), 2) AS total_profit,
       ROUND(AVG(Net_Margin_pct), 2) AS avg_margin
FROM retail
GROUP BY State
ORDER BY total_profit DESC
```

**Top states by revenue:**

| State | Total Sales | Total Profit | Avg Margin |
|---|---|---|---|
| California | $457,687 | $76,381 | 27.83% |
| New York | $310,876 | $74,038 | 29.84% |
| Washington | $138,641 | $33,402 | 27.64% |
| Michigan | $76,269 | $24,463 | 33.34% |
| Indiana | $53,555 | $18,382 | 34.79% |

💡 **Insight:** California and New York generate the most revenue but have the lowest margins among top states. Indiana and Georgia show healthier margin profiles despite lower revenue.

---

### Query 4 — Full territory overview

```sql
SELECT State,
       ROUND(AVG(Net_Margin_pct), 2) AS avg_margin,
       ROUND(SUM(Sales), 2) AS total_sales,
       ROUND(SUM(Profit), 2) AS total_profit,
       COUNT("Order ID") AS total_orders,
       SUM(CASE WHEN Net_Margin_pct < 10 THEN 1 ELSE 0 END) AS low_margin_orders
FROM retail
GROUP BY State
ORDER BY total_sales DESC
LIMIT 10
```

💡 **Insight:** This combined view reveals the full picture — allowing direct comparison of revenue, profitability and margin risk side by side across all territories.

---

## Key Business Insights

1. **Biggest markets = worst margins.** California ($457K revenue) and New York ($310K) both sit below 30% average margin with hundreds of low margin orders. The business appears to be over-discounting to compete in large, saturated markets.

2. **Texas is a triple red flag.** 585 low margin orders, doesn't appear in top revenue states, and isn't a high margin state — high volume, low revenue, low profit.

3. **Mid-size states are the hidden winners.** Indiana (34.79%), Georgia (34.52%) and Michigan (33.34%) show consistently healthy margins with far fewer low margin problem orders — these states represent the most profitable operating model.

4. **Small states show huge margin potential.** District of Columbia (42.2%) and Iowa (39.93%) have very few orders but exceptional margins — targeted expansion here could be high ROI.

---

## Business Recommendation

> The data suggests a **pricing strategy review** is needed for California and Texas specifically. The pattern of high volume + low margin in large states indicates either aggressive discounting, high shipping costs, or both. Replicating the pricing approach used in Indiana and Georgia across larger markets could significantly improve overall profitability.

---

## Files

- `retail_shipping_sample.csv` — merged dataset (9,995 rows)
- `queries.sql` — all SQL queries used in this analysis

---

*Analysis by Monika Kwiatkowska | [LinkedIn](https://www.linkedin.com/in/monikakwiatkowska) | [Portfolio](https://github.com/monikkwiatkowska)*

