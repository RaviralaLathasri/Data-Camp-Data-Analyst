# Data-Camp-Data-Analyst

> This Repository demonstrates end-to-end data analysis skills across SQL, Python, and business storytelling.

---

## 🏆 Certifications Earned

<table>
<tr>
<td align="center" width="50%">

### 🎓 Associate Data Analyst
**FoodYum Grocery — SQL Analysis**  
*Validated SQL data cleaning, aggregation & filtering*

</td>
<td align="center" width="50%">

### 🎓 Professional Data Analyst
**Fit.ly Tech — Churn Analysis**  
*End-to-end Python analysis, KPIs & executive presentation*

</td>
</tr>
</table>

---

## 📁 Repository Structure

```
Data-Camp-Data-Analyst/
│
├── 📂 Certificates/
│   ├── Data Analyst Associate.jpg
│   └── Data Analyst Professional.jpg
│
├── 📂 Dataset/
│   ├── da_fitly_account_info.csv
│   ├── da_fitly_customer_support.csv
│   └── da_fitly_user_activity.csv
│
├── 📓 Associate-Data Analyst.ipynb       ← SQL tasks for FoodYum
├── 📓 Advance-Data Analyst.ipynb         ← Python churn analysis for Fit.ly
├── 📊 Fitly_Churn_Analysis_Presentation.pptx
├── 📄 Practical--Exam.pdf
└── 📖 README.md
```

---

## 📌 Project 1 — Associate Data Analyst
### FoodYum Grocery Store: SQL Product Analysis

**Context:** FoodYum is a US-based grocery chain that wants to ensure it stocks products across a range of price points for all customers. As food costs rise, data quality and accurate reporting are critical.

### 🎯 Business Questions Answered

| Task | Question | Output |
|------|----------|--------|
| Task 1 | How many products are missing a `year_added` value? | `missing_year` — single count |
| Task 2 | Clean all columns to match business data standards | `clean_data` — 1,700 validated rows |
| Task 3 | What is the min and max price per product type? | `min_max_product` — 5 product categories |
| Task 4 | Which Meat & Dairy products sell more than 10 units/month? | `average_price_product` — 698 rows |

### 🔍 Key Findings
- **170 products** were missing `year_added` — all from a known 2022 system bug; filled with `2022`
- **Meat** has the highest price range ($11.48 – $16.98), making it the premium category
- **Produce** spans the widest affordable range ($3.46 – $8.78), serving budget-conscious shoppers
- **698 Meat & Dairy products** actively selling more than 10 units/month — a strong core inventory

### 🧱 Challenges & How I Solved Them

**Challenge 1 — Non-standard missing values**  
Missing data wasn't always `NULL`. Some fields contained dashes (`-`) or empty strings that standard `IS NULL` checks missed.  
✅ *Solution:* Used `COALESCE()` combined with `NULLIF()` and `REPLACE()` to catch all representations of missing data in a single expression.

**Challenge 2 — Numeric data stored as text with units**  
The `weight` column contained values like `"500.94 grams"` — impossible to use in calculations as-is.  
✅ *Solution:* Applied `REGEXP_REPLACE(weight, '[^\d.]', '', 'g')` to strip all non-numeric characters, then `CAST()` to convert to `DECIMAL(10,2)`.

**Challenge 3 — Median imputation in SQL**  
Replacing nulls with the median (not the mean) requires a more advanced SQL approach than a simple `AVG()`.  
✅ *Solution:* Used `PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ...)` as a subquery inside `COALESCE()` to compute and apply the median dynamically.

**Challenge 4 — Automarker validation**  
All output DataFrames had to have exact column names, types, and variable names to pass automated grading.  
✅ *Solution:* Ran the provided validation script after every query, cross-checking column names and formats before final submission.

### 🛠 SQL Techniques Used
`COALESCE` · `NULLIF` · `REPLACE` · `REGEXP_REPLACE` · `CAST` · `PERCENTILE_DISC` · `GROUP BY` · `MIN / MAX` · `WHERE IN` · `UPPER`

---

## 📌 Project 2 — Professional Data Analyst (Practical Exam)
### Fit.ly Tech: Subscriber Churn Analysis

**Context:** Fit.ly Tech is a subscription-based fitness app experiencing rising churn over two consecutive quarters. With customer acquisition costs increasing, leadership needed a clear picture of *why* users were leaving and *what to do about it* — backed by data.

> *"Retaining customers is absolutely critical for us right now — our cost of acquiring new users is rising, and every customer who leaves puts more pressure on Marketing and Product."*  
> — Head of Analytics, Fit.ly Tech

### 📦 Data Sources

| Dataset | Rows | Description |
|---------|------|-------------|
| `da_fitly_account_info.csv` | 400 | Subscriber plan, churn status, location |
| `da_fitly_customer_support.csv` | 918 | Support tickets, channels, resolution times |
| `da_fitly_user_activity.csv` | 445 | In-app events (workouts, videos, articles) |

### 🔍 Key Findings

| Finding | Metric | Impact |
|---------|--------|--------|
| **Overall churn rate** | 28.5% (114/400 users) | 🔴 Urgent |
| **Engagement gap** | Churned users: 0.36 avg activities vs 1.41 for active | 74% fewer |
| **Support gap** | Churned users waited 17.9h vs 6.0h for active users | 3× longer |
| **Free plan churn** | 41% vs 22% for Pro plan | Highest-risk segment |

### 📊 Deliverables

- **Written Report** — Full data validation, EDA with 5 charts, KPI definitions, recommendations
- **Jupyter Notebook** — Reproducible Python analysis with embedded visualisations
- **Executive Presentation** — 10-slide PowerPoint for senior leadership (non-technical audience)
- **Presenter Script** — Word-for-word 10-minute delivery script with Q&A preparation

### 💡 Recommendations Delivered

| Priority | Action | Target |
|----------|--------|--------|
| 🔴 HIGH | Re-engagement campaigns for 0-activity users | Double avg activities |
| 🔴 HIGH | Support SLA: resolve tickets in < 6 hours | Cut resolution time by 40% |
| 🔴 HIGH | Free → Paid conversion drive with upgrade incentives | Reduce Free churn to <30% |
| 🟡 MED | Early-warning churn dashboard | Weekly at-risk alerts |
| 🟡 MED | Structured onboarding for new users | Improve 30-day retention |

### 🧱 Challenges & How I Solved Them

**Challenge 1 — Churn column with implicit nulls**  
The `churn_status` column only labelled churned users as `"Y"`. Non-churned rows were left blank — not `False` or `"N"`. A naive analysis would have counted 286 NaN rows as missing data and excluded them.  
✅ *Solution:* Investigated the data structure, confirmed with context that blanks = active subscribers, and filled with `"N"` using `.fillna('N')`. Documented the decision transparently in the report.

**Challenge 2 — Three messy datasets from different teams**  
Each dataset used different conventions: timestamps stored as strings, channel values represented as `"-"`, inconsistent capitalisation in `stock_location`.  
✅ *Solution:* Built a systematic column-by-column validation framework, applied `pd.to_datetime()`, `.replace()`, and `.str.upper()` cleanly, and documented every fix in the written report.

**Challenge 3 — Sparse activity data**  
Only 245 of 400 subscribers had any activity records. Simply merging datasets would silently drop 155 users with no events, distorting the engagement analysis.  
✅ *Solution:* Used a `left join` (via `merge(..., how='left')`) from the account table to the activity data, then filled missing activity counts with `0` — preserving all users in the analysis.

**Challenge 4 — Communicating findings to a non-technical audience**  
Leadership needed insights they could act on, not statistical outputs. Presenting correlation coefficients or raw tables would not land.  
✅ *Solution:* Reframed every finding as a business implication. "Churned users average 0.36 activities" became "Users who barely log in are 74% less active — and far more likely to cancel." Built an executive presentation with stat call-outs, bar charts, and a KPI dashboard with clear targets.

**Challenge 5 — Defining a meaningful KPI**  
The brief asked for a business metric that leadership could monitor. Simply reporting churn rate wasn't enough — it needed context, a formula, a baseline, and a target.  
✅ *Solution:* Defined `Monthly Churn Rate = (Churned Users / Total Subscribers) × 100` as the primary KPI (baseline: 28.5%, target: <20%), supported by three leading indicators — engagement score, resolution time, and Free plan churn rate.

### 🛠 Python Stack
`pandas` · `numpy` · `matplotlib` · `seaborn` · `datetime` · `jupyter`

---

## 📈 Skills Demonstrated Across Both Projects

| Skill | Associate | Professional |
|-------|-----------|--------------|
| Data validation & cleaning | ✅ SQL | ✅ Python |
| Missing value imputation | ✅ COALESCE / median | ✅ fillna / left join |
| Exploratory data analysis | ✅ Aggregation queries | ✅ Multi-variable charts |
| Business metric definition | — | ✅ KPI dashboard |
| Stakeholder communication | — | ✅ Executive PPT + script |
| Recommendations | — | ✅ 5 prioritised actions |

---

## 🚀 How to Run the Notebooks

```bash
# Clone the repository
git clone https://github.com/yourusername/Data-Camp-Data-Analyst.git
cd Data-Camp-Data-Analyst

# Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Launch
jupyter notebook
```

## 🤝 Connect

If you're a recruiter, hiring manager, or fellow analyst — feel free to reach out!

[![LinkedIn](https://linkedin.com/in/lathasri-ravirala-06b606309)
[![Mail](lathasriravirala2003@gmail.com)

---


