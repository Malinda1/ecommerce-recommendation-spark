# Ecommerce Recommendation System with Apache Spark

A big data analysis and recommendation system for ecommerce data using Apache Spark and Python. Performs exploratory data analysis, builds collaborative filtering recommendations, and analyzes purchasing trends.

**Dataset:** Online Retail II (UCI) - 1M+ transactions, 4,300+ customers, 4,600+ products across 37 countries (Dec 2009 - Dec 2011)

---

## Quick Start

### Prerequisites
- Python 3.8+
- Java JDK 11+
- Apache Spark 3.4+ (optional, for notebook 03)
- 8GB RAM, 10GB disk space

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

---

## Notebooks

| Notebook | Purpose | Key Output | Runtime |
|----------|---------|-----------|---------|
| **01_data_cleaning.ipynb** | Load raw CSV, clean & validate, create features | 779K cleaned records | 2-5 min |
| **02_visualisation.ipynb** | EDA with 7 charts (revenue, trends, products) | 7 PNG charts + 5 CSV files | 1-2 min |
| **03_frequently_bought.ipynb** | Market basket analysis - product co-purchase pairs | Top 100 pairs with metrics | 3-5 min |
| **04_recommendations_and_trend.ipynb** | Recommendations engine + trend analysis | 7 charts + 8 CSV metrics | 3-5 min |

**Run order:** 01 → 02 → 03 → 04

---

## Project Structure

```
ecommerce-recommendation-spark/
├── README.md                         # This file
├── requirements.txt                  # Python dependencies
├── data/raw/
│   └── online_retail_II.csv         # Raw data (1.067M records)
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_visualisation.ipynb
│   ├── 03_frequently_bought.ipynb
│   ├── 04_recommendations_and_trend.ipynb
│   └── output/                       # Generated outputs
│       ├── cleaned_data/
│       ├── visualisations/
│       ├── frequent_pairs/
│       ├── recommendations/
│       └── trends/
└── report/
    └── Group_Report.docx
```

---

## Key Insights

- **UK dominates:** 83% of total revenue (£9.2M)
- **Seasonality:** November peak driven by Christmas shopping
- **Customer concentration:** Top 10% of customers drive majority revenue
- **Market basket:** Products frequently bought together have strong co-purchase patterns
- **Loyalty:** Customers with 6+ orders spend 5-10x more than one-time buyers

---

## Output Files Summary

### Notebook 02 - Visualisation
- **Charts:** Top countries, monthly trends, best products, day-of-week patterns, order distribution, top customers, revenue heatmap
- **Data:** Dataset summary, monthly breakdown, customer/product lists

### Notebook 03 - Frequently Bought
- **Charts:** Top product pairs, pair frequency distribution
- **Data:** Top 100 pairs with lift/support/confidence metrics

### Notebook 04 - Recommendations & Trends
- **Charts:** Recommendations, monthly/quarterly trends, AOV, top products by country, customer retention
- **Data:** 8 CSV files with trends and metrics

---

## Troubleshooting

**"JAVA_HOME is not set"**
```powershell
$env:JAVA_HOME = "C:\Program Files\Java\jdk-17.0.1"
java -version  # Verify
```

**"PySpark module not found"**
```powershell
pip install --upgrade pyspark
```

**"Jupyter kernel timeout"**
- Increase Spark memory in notebook:
```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.config("spark.driver.memory", "4g").getOrCreate()
```

---

## Authors
- **Data Cleaning:** Team
- **Visualisation:** Adeesha & Thaweesha
- **Recommendations:** Kevin
- **Documentation:** Team

---

## License
Educational project (NSBM Big Data Course)

## References
- [Apache Spark](https://spark.apache.org/docs/latest/)
- [UCI Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail)
- [PySpark API](https://spark.apache.org/docs/latest/api/python/)

**Repository:** https://github.com/Malinda1/ecommerce-recommendation-spark
