# Ecommerce Recommendation System with Apache Spark

A big data analysis and recommendation system for ecommerce data using Apache Spark and Python. Performs exploratory data analysis, builds collaborative filtering recommendations, and analyses purchasing trends.

**Dataset:** Online Retail II (UCI) — 1M+ transactions, 5,878 customers, 4,631 products across 41 countries (Dec 2009 – Dec 2011)

---

## Quick Start

### Prerequisites
- Python 3.8+
- Java JDK 11+
- Apache Hadoop (HDFS running on `localhost:8020`)
- Apache Spark 3.4+
- 8 GB RAM, 10 GB disk space

### Setup (Windows)

```powershell
# Clone and navigate
git clone https://github.com/Malinda1/ecommerce-recommendation-spark.git
cd ecommerce-recommendation-spark

# Create and activate virtual environment
python -m venv venv
.\venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt

# Start Jupyter
jupyter lab
```

### Setup (macOS / Linux)

```bash
git clone https://github.com/Malinda1/ecommerce-recommendation-spark.git
cd ecommerce-recommendation-spark

python3 -m venv venv
source venv/bin/activate

pip install -r requirements.txt
jupyter lab
```

---

## Notebooks

> **Run order is important — always run 01 first.**

| # | Notebook | Author | Purpose | Key Output | Runtime |
|---|----------|--------|---------|------------|---------|
| 01 | `01_data_cleaning.ipynb` | Pasindu | Load raw CSV → HDFS → EDA → Clean → Save Parquet to HDFS | 779K cleaned records | 3–5 min |
| 02 | `02_visualisation.ipynb` | Thaweesha | Load from HDFS → 7 EDA charts → Save PNGs + CSVs | 7 charts + 7 CSV files | 2–3 min |
| 03 | `03_frequently_bought.ipynb` | Ishara | Spark SQL self-join → product pair co-occurrence analysis | Top 100 pairs with lift/support/confidence | 4–6 min |
| 04 | `04_recommendations_system.ipynb` | Kevin | Item-based collaborative filtering recommendation engine | Recommendation chart + CSV | 3–5 min |
| 05 | `05_purchasing_trends.ipynb` | Adeesha | Monthly/quarterly trends, AOV, country products, retention | 5 trend charts + 5 CSV files | 2–4 min |

**Run order:** `01 → 02 → 03 → 04 → 05`  
Notebooks 02–05 are independent of each other and can run in any order **after** 01 completes.

---

## Project Structure

```
ecommerce-recommendation-spark/
├── README.md
├── requirements.txt
├── data/
│   └── raw/
│       └── online_retail_II.csv          # Raw dataset (1,067,371 records)
├── notebooks/
│   ├── 01_data_cleaning.ipynb            # Pasindu
│   ├── 02_visualisation.ipynb            # Thaweesha
│   ├── 03_frequently_bought.ipynb        # Ishara
│   ├── 04_recommendations_system.ipynb   # Kevin
│   ├── 05_purchasing_trends.ipynb        # Adeesha
│   └── output/
│       ├── cleaned_data/
│       │   ├── retail_cleaned_full.csv
│       │   └── schema.json
│       ├── eda/
│       │   ├── eda_null_values.png
│       │   └── eda_distributions.png
│       ├── visualisations/
│       │   ├── chart1_top10_countries.png
│       │   ├── chart2_monthly_revenue.png
│       │   ├── chart3_top10_products.png
│       │   ├── chart4_orders_by_day.png
│       │   ├── chart5_order_distribution.png
│       │   ├── chart6_top_customers.png
│       │   ├── chart7_heatmap.png
│       │   └── *.csv
│       ├── frequent_pairs/
│       │   ├── chart_frequent_pairs.png
│       │   ├── chart_pair_distribution.png
│       │   ├── top100_product_pairs.csv
│       │   └── top100_pairs_with_metrics.csv
│       ├── recommendations/
│       │   ├── chart_recommendations.png
│       │   └── recommendations_top5_products.csv
│       └── trends/
│           ├── chart_monthly_trends.png
│           ├── chart_quarterly.png
│           ├── chart_avg_order_value.png
│           ├── chart_top5_by_country.png
│           ├── chart_customer_retention.png
│           └── *.csv
└── report/
    └── Group_Report.docx
```

---

## HDFS Data Layout

All notebooks read and write to the following HDFS paths:

```
hdfs://localhost:8020/
└── retail/
    ├── raw/
    │   └── online_retail_II.csv          ← uploaded by Notebook 01
    ├── cleaned/                           ← written by Notebook 01, read by 02–05
    └── output/
        ├── frequent_pairs/               ← Notebook 03
        ├── recommendations/              ← Notebook 04
        └── trends/
            ├── monthly/                  ← Notebook 05
            └── quarterly/               ← Notebook 05
```

---

## Key Insights

| Finding | Detail |
|---------|--------|
| **UK dominates** | 83% of total revenue (£14.5M) from domestic customers |
| **Seasonality** | Clear November peak each year driven by Christmas gift purchasing |
| **Weekday-only** | Near-zero orders on weekends — confirms B2B wholesale model |
| **Top product pairs** | Red + White Heart T-Light Holder bought together 1,153 times |
| **Loyalty value** | Customers with 6+ orders spend 5–10× more than one-time buyers |
| **International** | Netherlands, EIRE, Germany are top international markets |

---

## Output Files by Notebook

### Notebook 01 — Data Cleaning (Pasindu)
- `output/eda/eda_null_values.png` — missing value bar chart
- `output/eda/eda_distributions.png` — Quantity + Price distributions
- `output/cleaned_data/retail_cleaned_full.csv` — cleaned dataset
- `output/cleaned_data/schema.json` — column schema

### Notebook 02 — Visualisation (Adeesha & Thaweesha)
- 7 chart PNGs: countries, monthly trend, products, day-of-week, order distribution, top customers, heatmap
- 6 CSV files: dataset summary, monthly revenue, top products/countries/customers, orders by day

### Notebook 03 — Frequently Bought Together (Ishara)
- `output/frequent_pairs/chart_frequent_pairs.png` — top 10 pairs bar chart
- `output/frequent_pairs/chart_pair_distribution.png` — co-occurrence distribution
- `output/frequent_pairs/top100_product_pairs.csv` — raw pair data
- `output/frequent_pairs/top100_pairs_with_metrics.csv` — support, confidence, lift

### Notebook 04 — Recommendations (Kevin)
- `output/recommendations/chart_recommendations.png` — 3-panel recommendation chart
- `output/recommendations/recommendations_top5_products.csv` — recommendation results

### Notebook 05 — Purchasing Trends (Adeesha)
- `output/trends/chart_monthly_trends.png` — monthly revenue + orders (dual axis)
- `output/trends/chart_quarterly.png` — quarterly revenue grouped by year
- `output/trends/chart_avg_order_value.png` — average order value over time
- `output/trends/chart_top5_by_country.png` — top products per country (5 panels)
- `output/trends/chart_customer_retention.png` — loyalty tier analysis (2 panels)
- 5 CSV files with corresponding data

---

## Troubleshooting

**"JAVA_HOME is not set"**
```powershell
# Windows
$env:JAVA_HOME = "C:\Program Files\Java\jdk-17.0.1"
java -version
```
```bash
# macOS/Linux
export JAVA_HOME=$(/usr/libexec/java_home)
```

**"PySpark module not found"**
```bash
pip install --upgrade pyspark
```

**HDFS not running**
```bash
start-dfs.sh          # macOS/Linux
# or check Hadoop is started before running Notebook 01
hdfs dfs -ls /        # verify HDFS is accessible
```

**"Jupyter kernel timeout" / Out of memory**
```python
# Increase memory in any notebook's SparkSession config
spark = SparkSession.builder \
    .config("spark.driver.memory", "6g") \
    .config("spark.executor.memory", "6g") \
    .getOrCreate()
```

**Notebook 02–05 fails to load data**  
Make sure Notebook 01 has been run successfully first — it writes the cleaned Parquet to HDFS that all other notebooks depend on.

---

## Team

| Name | Role | Notebook |
|------|------|----------|
| Pasindu | Data Cleaning & Preprocessing | 01 |
| Thaweesha | Visualisation | 02 |
| Ishara | Frequently Bought Together Analysis | 03 |
| Kevin | Recommendation System | 04 |
| Adeesha | Trend Analysis | 05 |

---

## License
Educational project — NSBM Big Data Course

## References
- [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
- [UCI Online Retail II Dataset](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- [PySpark API Reference](https://spark.apache.org/docs/latest/api/python/)
- [Hadoop HDFS Guide](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html)

**Repository:** https://github.com/Malinda1/ecommerce-recommendation-spark
