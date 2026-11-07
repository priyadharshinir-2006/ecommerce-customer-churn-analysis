# E-commerce Customer Churn Analysis

**Which customers are leaving, when do they leave, and who should the customer care team call first?**

An end-to-end analytics project using **Python, DuckDB (SQL) and Tableau**, from raw data to a published decision dashboard for retention teams.

**[View the live dashboard on Tableau Public]**https://public.tableau.com/app/profile/priyadharshini.r5311/viz/e-commercecustomerchurndashboard/Dashboard1**

![Dashboard preview](dashboard/Dashboard%201.png)

---

## Key Findings 

| Metric | Result |
|---|---|
| Customers analyzed | 3,941 |
| Churned customers | 674 |
| Overall churn rate | **17.1%** |
| Churn in the first 0-1 months | **53.5%** (n=836) |
| Churn at 13+ months | 4.7% (n=1,301) |
| High Risk tier churn | **67.7%** (n=254) |
| Medium Risk tier churn | 22.3% (n=1,913) |
| Low Risk tier churn | 4.2% (n=1,774) |

1. **Churn is an onboarding problem.** More than half of customers in their first 1-2 months churn, versus under 5% after a year.
2. **High Risk is precise but small.** It churns at 67.7% but holds only about 26% of all churners.
3. **Medium Risk holds most of the churn.** About 63% of churned customers (427 of 674) sit in the Medium tier, so a team that only works the High Risk list would miss most of them.

---

## Business Problem

A customer care team cannot contact every customer. This project answers two questions:
- **When** do customers churn?
- **Which segments** should care teams prioritize to reduce churn and increase customer tenure?

---

## Dataset

- **Source:** [E-commerce Customer Churn dataset on Kaggle](https://www.kaggle.com/datasets/samuelsemaya/e-commerce-customer-churn)
- **Dataset size:** 3,941 customer rows, 674 churned
- **Key fields:** Tenure, Complain, Satisfaction Score, Cashback Amount, Preferred Order Category, Day Since Last Order, Warehouse To Home, Number of Device Registered

---

## Approach

1. **Data cleaning (Python, Jupyter):** Imputed missing values in continuous features (`Tenure`, `WarehouseToHome`, `DaySinceLastOrder`) using median imputation to preserve sample size, standardized redundant categories (e.g., merging `"Mobile Phone"` into `"Mobile"`), and dropped unneeded index/ID columns.
2. **Analysis (DuckDB SQL):** Evaluated churn rates by tenure cohorts and risk tiers by executing high-performance SQL queries directly on Pandas DataFrames inside Jupyter.
3. **Risk segmentation (rule-based SQL `CASE` logic):**
   - **High Risk:** complaint + tenure ≤ 6 months + mobile order category
   - **Medium Risk:** complaint **or** tenure ≤ 6 months
   - **Low Risk:** all other customers
4. **Dashboard (Tableau Public):** Built executive KPIs, risk tier distributions, tenure cohort trends, and action-oriented retention recommendations into an interactive dashboard.

---

## Dashboard Design Decisions

The dashboard went through several revisions to make it usable for a non-technical care team:

- **Insight-led headline:** The top line states the main finding, so a reader gets the point in about 10 seconds.
- **Labelled KPIs:** Total Customers, Churned Customers, Churn Rate.
- **Sample size on every bar (n=):** So a reader can judge how reliable each percentage is. For example, 67.7% is based on 254 customers.
- **Tenure grouped into buckets** (0-1, 2-6, 7-12, 13+ months) instead of a noisy line chart. Tiny groups at long tenures had produced misleading 0% values.
- **Zero-based axes:** Bars start at 0% so the gaps between tiers are not exaggerated.
- **Tier definitions and recommendations on the page:** The dashboard says what the tiers mean and what to do next.

---

## Recommendations

1. **Onboarding:** Contact new customers in their first 2 months, when churn is 53%.
2. **Complaints:** Resolve complaints fast. Complaint + short tenure is the High Risk profile.
3. **Targeting:** Work both High and Medium Risk lists, since Medium holds about 63% of churners.

---

### Limitations

- **Rule-based vs. Predictive:** The risk tiers are rule-based heuristic segments, not a statistical predictive model. They rank customers by observed logic rather than individual probabilities.
- **Correlation vs. Causation:** Tiers rely on tenure and complaints; results reflect strong risk associations rather than proven causal mechanisms.
- **Actionability:** The dashboard provides aggregate segment trends; operational teams would require an exported customer ID dispatch list for direct outreach.
- **Imputation assumption:** Missing numerical values (`Tenure`, `WarehouseToHome`, `DaySinceLastOrder`) were filled using column medians to preserve overall sample size.

---

### Next Steps

- Build a predictive machine learning churn model (Logistic Regression / XGBoost) and compare performance against rule-based tiers.
- Add a customer-level at-risk dispatch list for the customer support team.
- Expand churn analysis to include breakdowns by product category complaints and individual satisfaction scores.

---

## How to Run

1.Clone the repository:
   ```bash
   git clone
 https://github.com/priyadharshinir-2006/ecommerce-customer-churn-analysis.git
