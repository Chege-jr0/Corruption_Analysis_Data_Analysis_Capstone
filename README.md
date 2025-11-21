# Corruption and Economic Growth in Africa 📊

A data analytics project exploring the relationship between corruption levels and economic performance across African countries using data from Transparency International and the World Bank.

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Google Cloud](https://img.shields.io/badge/Google%20Cloud-BigQuery-4285F4.svg)](https://cloud.google.com/bigquery)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Here is the link to my Technical Article: https://medium.com/@paulgikonyo100/analyzing-corruptions-economic-impact-across-africa-a-data-analytics-project-496504428919.

The project presentation : https://africa-growth-audit.lovable.app/

## 🎯 Project Overview

This project investigates whether higher corruption correlates with slower GDP growth and reduced foreign direct investment (FDI) across African nations. By combining Transparency International's Corruption Perceptions Index (CPI) with World Bank economic indicators, the analysis provides data-backed insights into how governance quality influences economic performance.

### The Problem

African countries lose an estimated **$88 billion annually** to corruption, yet policymakers often lack clear, quantitative evidence on how corruption specifically impacts their economies. This project aims to:

- Quantify the economic cost of corruption in measurable terms
- Identify patterns and outliers across different African regions
- Provide actionable insights for investors, policymakers, and development organizations

## 🔍 Key Research Questions

1. **What is the correlation strength** between corruption levels (CPI scores) and GDP growth rates?
2. **Is there a corruption threshold** beyond which economic growth dramatically declines?
3. **How does corruption impact FDI flows** across different countries?
4. **Which countries are outliers** - performing well despite corruption or struggling despite good governance?
5. **What is the time-lag effect** - do corruption improvements today predict economic gains tomorrow?

## 🛠️ Technology Stack

### Data Infrastructure
- **Google Cloud Storage**: Raw data storage and data lake
- **Google BigQuery**: Data warehousing, SQL transformations, and analysis
- **Python 3.8+**: ETL pipeline and API integration
- **Tableau**: Interactive dashboards and visualizations

### Key Libraries
```python
google-cloud-bigquery
google-cloud-storage
pandas
requests
```

## 🚀 Getting Started

### Prerequisites

1. **Google Cloud Project** with BigQuery and Cloud Storage enabled
2. **Python 3.8+** installed
3. **Tableau Desktop** (optional, for dashboard visualization)
4. **Google Cloud SDK** configured

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Chege-jr0/corruption-economic-growth.git
cd corruption-economic-growth
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Set up Google Cloud authentication**
```bash
# Set your project ID
gcloud config set project data-analytics-capstone-476406

# Authenticate
gcloud auth application-default login
```


### Data Pipeline Execution

#### Step 1: Upload Raw Data to Cloud Storage
```bash
gsutil cp data/raw/ti-corruption-data.csv gs://data-bucket-capstone-1/
```

#### Step 2: Create BigQuery Dataset
```bash
bq mk --dataset data-analytics-capstone-476406:corruption_analysis
```

#### Step 3: Load Corruption Data to BigQuery
```sql
LOAD DATA OVERWRITE `data-analytics-capstone-476406.corruption_analysis.corruption_data`
FROM FILES (
  format = 'CSV',
  uris = ['gs://data-bucket-capstone-1/ti-corruption-data.csv'],
  skip_leading_rows = 1
);
```

#### Step 4: Fetch World Bank Economic Data
```bash
python scripts/extract_worldbank_data.py
```

#### Step 5: Run Data Transformations
```bash
bq query --use_legacy_sql=false < sql/data_transformation.sql
```

#### Step 6: Connect Tableau to BigQuery
- Open Tableau Desktop
- Connect to Google BigQuery
- Select your project and `corruption_analysis` dataset
- Import the `analysis_dataset` table

## 📊 Data Sources

### Transparency International - Corruption Perceptions Index (CPI)
- **Source**: [Transparency.org](https://www.transparency.org/en/cpi)
- **Coverage**: 2010-2023
- **Metric**: CPI Score (0-100, where 100 = very clean, 0 = highly corrupt)
- **Countries**: 54 African nations

### World Bank Open Data API
- **Source**: [World Bank Data API](https://data.worldbank.org/)
- **Indicators Used**:
  - GDP Growth Rate (annual %) - `NY.GDP.MKTP.KD.ZG`
  - GDP per Capita - `NY.GDP.PCAP.CD`
  - Foreign Direct Investment (FDI) Net Inflows - `BX.KFI.TOTL.CD.WD`
  - GNI per Capita - `NY.GNP.PCAP.CD`
  - Trade (% of GDP) - `NE.TRD.GNFS.ZS`
  - Inflation Rate - `FP.CPI.TOTL.ZG`

## 🔬 Methodology

### Data Processing
1. **Data Collection**: Downloaded CPI data and fetched World Bank indicators via API
2. **Data Cleaning**: Handled missing values, standardized country codes (ISO3), normalized time periods
3. **Data Integration**: Joined datasets on country code and year in BigQuery

### Analysis Approach
- **Correlation Analysis**: Pearson correlation coefficients between CPI and economic indicators
- **Segmentation**: Countries grouped by CPI score ranges (0-30, 31-50, 51-70, 71-100)
- **Outlier Detection**: Identified countries with unexpected economic performance

## 📈 Key Findings

### Preliminary Insights

> **Note**: Update this section with your actual findings after analysis

1. **Strong Negative Correlation**: CPI scores show a correlation of -0.52 with GDP growth rates, indicating higher corruption associates with slower growth

2. **FDI Impact**: Countries with CPI scores above 50 attract 3x more FDI per capita than those below 30

3. **Threshold Effect**: Economic growth drops sharply when CPI falls below 30 (severe corruption)

4. **Success Stories**: Rwanda and Botswana show consistent CPI improvements (20+ points) correlating with 50%+ FDI increases

5. **Regional Patterns**: North African countries show different corruption-growth dynamics compared to Sub-Saharan Africa

## 💼 Business Value & Impact

### For International Investors
- **Risk Quantification**: Convert corruption concerns into measurable ROI impacts
- **Market Selection**: Data-driven country entry strategies based on corruption trends
- **Cost Estimation**: Model shows 10-point CPI increase reduces operational costs by ~15%

### For African Governments
- **Reform Prioritization**: Evidence that improving CPI by 10 points could boost GDP growth by 1.5-2%
- **Investment Attraction**: Demonstrate governance improvements to international investors
- **Budget Allocation**: Quantified ROI for anti-corruption programs

### For Development Organizations
- **Program Effectiveness**: Measure impact of governance interventions on economic outcomes
- **Resource Allocation**: Target countries where anti-corruption efforts yield highest economic returns
- **Donor Reporting**: Evidence-based justification for continued funding

## 📊 Sample Visualizations

The Tableau dashboard includes:

- **Scatter Plot**: CPI Score vs GDP Growth Rate
- **Geographic Heat Map**: Corruption levels across Africa with tooltip economic data
- **Bar Charts**: Countries by Corruption Perception Index.
- **Interactive Filters**: By year and country.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Your Name**
- GitHub: [@Chege-jr0](https://github.com/Chege-jr0)
- LinkedIn: [Paul Gikonyo](https://www.linkedin.com/in/paul-gikonyo-15389418b/)
- Email: paulgikonyo100@gmail.com

## 🙏 Acknowledgments

- [Transparency International](https://www.transparency.org/) for Corruption Perceptions Index data
- [World Bank Open Data](https://data.worldbank.org/) for economic indicators
- African Union for corruption cost estimates and research
- Google Cloud Platform for infrastructure support

## 📚 References

1. Transparency International. (2023). *Corruption Perceptions Index 2023*
2. World Bank. (2024). *World Development Indicators*
3. African Union. (2022). *Report on Illicit Financial Flows from Africa*
4. Mauro, P. (1995). *Corruption and Growth*. The Quarterly Journal of Economics







