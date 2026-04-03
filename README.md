# 🌍 Global Development Analytics Dashboard

> **End-to-end data pipeline + Power BI dashboard** built on the **World Bank REST API** — covering 266 countries, 7 development domains, and 24 indicators across 2016–2024.

---

## 📌 Project Overview

This project pulls live development data directly from the **World Bank Open Data API**, cleans and structures it across seven thematic domains, and visualizes it through an interactive **Power BI dashboard** with 15+ report pages.

The goal: give analysts, policymakers, and researchers a single, navigable view of how countries compare on economic growth, health outcomes, poverty, trade, and more — all from a reproducible, API-driven pipeline.

---

## 🗺️ Architecture

```
World Bank REST API
        │
        ▼
  API_Data.ipynb          ← Data collection & cleaning (Python / requests)
        │
        ▼
  7 Domain CSVs           ← Structured, analysis-ready outputs
        │
        ▼
  Power_BI_API.pbix       ← Interactive dashboard (15+ visualizations)
```

---

## 📊 Domains & Indicators Covered

| Domain | Indicators | Records |
|---|---|---|
| 🏦 **Economic Activity** | GDP growth (annual %), GDP per capita (current US$) | 4,788 |
| 🌱 **Environment** | Renewable energy consumption (%), Forest area (% of land area) | 4,788 |
| ❤️ **Health** | Life expectancy, Infant mortality, Health expenditure (% GDP), HIV incidence, Maternal mortality, Tuberculosis, Immunization rates + 6 more | 31,122 |
| 💼 **Labour Market** | Total unemployment (%), Youth unemployment (%), Labour force size | 7,182 |
| 💸 **Poverty & Inequality** | Poverty headcount ratio (national lines), Gini index | 4,788 |
| 💻 **Technology Access** | Internet users (% of population), Mobile subscriptions per 100 people | 4,788 |
| 🚢 **Trade & Globalization** | Exports of goods & services (current US$), Imports (current US$) | 4,788 |

**Total: 266 countries · 24 indicators · 2016–2024 · ~62,000 records across all domains**

---

## 🔧 Technical Stack

| Layer | Tools |
|---|---|
| **Data Collection** | Python, `requests`, World Bank REST API |
| **Data Wrangling** | `pandas`, `numpy` |
| **EDA / Analysis** | `seaborn`, `matplotlib` — correlation heatmaps, regression plots |
| **Dashboard** | Microsoft Power BI (`.pbix`) |
| **Storage** | CSV (domain-separated, analysis-ready) |

---

## 📁 Repository Structure

```
world-bank-analytics/
│
├── README.md
│
├── notebooks/
│   └── API_Data.ipynb          # Full pipeline: API → clean CSVs
│
├── data/
│   ├── economic.csv            # GDP growth & GDP per capita
│   ├── environment.csv         # Renewable energy & forest area
│   ├── health.csv              # 13 health indicators
│   ├── labour_market.csv       # Unemployment & labour force
│   ├── poverty.csv             # Poverty headcount & Gini index
│   ├── technology.csv          # Internet & mobile access
│   ├── trade.csv               # Exports & imports
│   └── final_df.csv            # Full World Bank indicator catalogue (29,323 indicators)
│
├── powerbi/
│   └── Power_BI_API.pbix       # Interactive Power BI dashboard
│
└── visuals/
    └── dashboard_preview.png   # Dashboard screenshot (see below)
```

---

## ⚙️ How to Reproduce

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/world-bank-analytics.git
cd world-bank-analytics
```

### 2. Install dependencies
```bash
pip install requests pandas numpy matplotlib seaborn
```

### 3. Run the notebook
Open `notebooks/API_Data.ipynb` in Jupyter or VS Code and run all cells.

The notebook will:
- Hit the World Bank Countries API to build a country master list (296 countries/regions)
- Fetch 24 indicators across 7 domains via paginated API calls
- Merge with country metadata (region, income level, lending type, coordinates)
- Export 7 domain-specific CSVs to `/data/`

> **Note:** The full indicator catalogue (`final_df.csv`) was collected from 525 API pages and contains 29,323 World Bank indicators. This step can be skipped if you only need domain data.

### 4. Open the dashboard
Open `powerbi/Power_BI_API.pbix` in **Power BI Desktop** (free, Windows).

---

## 🔌 API Reference

This project uses the **World Bank Open Data API** (no authentication required).

| Endpoint | Purpose |
|---|---|
| `https://api.worldbank.org/countries?format=json&per_page=300` | Fetch country master list |
| `https://api.worldbank.org/v2/indicators?format=json&per_page=500&page={n}` | Fetch all available indicators |
| `https://api.worldbank.org/countries/all/indicators/{CODE}?format=json&per_page=1000&page={n}` | Fetch indicator data for all countries |

**Key API parameters:**
- `format=json` — JSON response format
- `per_page` — results per page (max 1000 for indicator data)
- `page` — pagination (auto-looped in the notebook)

---

## 📈 Sample Analyses

### Health Expenditure vs. Life Expectancy
A regression plot across all countries shows a positive correlation between current health expenditure (% of GDP) and life expectancy at birth — with notable outliers (high-spend, low-outcome countries) worth investigating.

### Indicator Correlation Heatmap (Health Domain)
A 13×13 correlation matrix across health indicators reveals:
- Strong negative correlation between **maternal mortality** and **skilled birth attendance**
- Strong positive correlation between **life expectancy** and **basic drinking water access**
- Negative correlation between **HIV incidence** and **immunization rates**

---

## 📌 Key Design Decisions

- **Domain separation:** Data is split into 7 domain CSVs rather than one flat file to enable focused analysis without unnecessary joins.
- **Aggregates included:** Country groups (e.g., "Africa Eastern and Southern") are retained to allow regional benchmarking in Power BI.
- **Coordinates preserved:** Longitude/latitude from the countries API are kept to support map visuals in Power BI.
- **Indicator catalogue:** The full `final_df.csv` (29,323 indicators) is available as a reference for extending the pipeline to new domains.

---

## 🔮 Potential Extensions

- Add **time-series forecasting** (Prophet / ARIMA) for GDP or life expectancy
- Build a **Streamlit web app** for browser-based exploration
- Schedule automated **weekly API refreshes** with GitHub Actions
- Add **clustering analysis** to group countries by development profile
- Expand to additional domains: Education, Infrastructure, Governance

---

## 👤 Author

**Satya Prakash Rai**  
B.Tech Mining Engineering — IIT (ISM) Dhanbad, 2025  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/YOUR_PROFILE)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?logo=github)](https://github.com/YOUR_USERNAME)

---

## 📄 Data Source

All data sourced from the **[World Bank Open Data](https://data.worldbank.org/)** platform, available under the [Creative Commons Attribution 4.0 license (CC BY 4.0)](https://datacatalog.worldbank.org/public-licenses#cc-by).
