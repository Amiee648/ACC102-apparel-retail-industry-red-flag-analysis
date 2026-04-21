# ACC102-apparel-retail-industry-red-flag-analysis

A Python-based financial red flag screener for the North American apparel retail industry, identifying operational divergence through growth rate analysis.

## Quick Access
- Main notebook:https://github.com/Amiee648/ACC102-apparel-retail-industry-red-flag-analysis/blob/main/A%20Beginner-friendly%20Financial%20Red%20Flag%20Screener%20for%20Sportswear%20and%20Apparel%20Retail%20Companies_%E5%89%AF%E6%9C%AC.ipynb 
- Demo video: 

## Problem
This project builds a simple financial red flag screener for the North American apparel retail industry. The purpose is to help beginner investors and business students identify potential warning signs by comparing revenue growth with inventory growth, fixed asset growth, and accounts receivable growth over the most recent fiscal years.

This notebook does not aim to prove fraud. Instead, it provides a simple and interpretable screening approach for identifying companies whose business expansion may not be fully supported by sales growth. The output is intended to help users compare firms, spot possible warning signals, and create a watchlist for further analysis.

## Target User
This project is intended for beginner investors and business students who want a reproducible screening framework to compare apparel retail peers and surface potential operational risk.

## Data Source
**Source:** WRDS (Compustat - Fundamentals Annual) via a dynamic Python connection using the `wrds` library.
*   **Sample:** Full apparel retail industry sample defined by SIC codes 5600-5699: Apparel and Accessory Stores.
*   **Timeframe:** Fiscal years 2018 to present.
*   **Date Accessed:** April 18, 2026.
*   **Access Note:** WRDS is a restricted academic database requiring institutional credentials. The raw Compustat dataset is not included in this repository. Data is extracted dynamically at runtime via the notebook.

## Methods
1. Load and clean the data from WRDS.
2. Calculate year-over-year growth rates for sales, inventory, fixed assets, and receivables.
3. Apply red flag rules to compare each metric against sales growth:
   - Flag inventory or fixed assets if growth exceeds sales growth by more than 15%
   - Flag receivables if growth exceeds sales growth by more than 20%
4. Generate a warning score for each company-year observation.
5. Aggregate warning scores to identify outliers.
6. Visualize both the overall risk ranking and the detailed growth divergence for top risk companies.

## Key Findings
- **SCVL**, **BURL**, and **DXLG** display the highest cumulative warning scores in the full industry analysis.
- The most common red flag drivers are:
  - inventory growth outpacing sales,
  - fixed asset growth outpacing sales,
  - receivables growth outpacing sales.

## How to Run
1. **Prerequisites:** Ensure you have a valid WRDS account with access to Compustat data. If you do not have WRDS access, contact your academic institution or visit [WRDS](https://wrds-www.wharton.upenn.edu/).
2. **Install Dependencies:** Install required packages using pip:
   ```bash
   pip install -r requirements.txt
   ```
   Or manually:
   ```bash
   pip install pandas wrds matplotlib
   ```
3. **Set Credentials:** Open the notebook (`A Beginner-friendly Financial Red Flag Screener for Sportswear and Apparel Retail Companies.ipynb`) and update the WRDS connection line with your credentials:
   ```python
   db = wrds.Connection(wrds_username="your_wrds_username")
   ```
4. **Run the Notebook:** Execute all cells sequentially. The notebook will:
   - Connect to WRDS and fetch Compustat data dynamically
   - Perform data cleaning and growth rate calculations
   - Generate visualizations and output results directly in the notebook
5. **Outputs:** Analysis results and visualizations will be displayed in the notebook output cells. To save figures, modify the visualization cells to include `plt.savefig()` commands.

**Note:** No data files are included in this repository. All data is fetched dynamically from WRDS at runtime, ensuring you always have the latest financial information.

## Repository Structure
*   `A Beginner-friendly Financial Red Flag Screener for Sportswear and Apparel Retail Companies.ipynb`: The main Jupyter notebook containing the complete analysis workflow.
*   `requirements.txt`: List of Python dependencies required to run the notebook.
*   `figures/`: Directory containing output visualizations (e.g., `three_companies.png` for the multi-dimensional red flag charts).
*   `README.md`: Project documentation.

## Data Availability
This project does not include raw financial data files for the following reasons:
- **WRDS Licensing:** The Compustat data is sourced from WRDS, a restricted academic database. Distributing this data would violate licensing agreements.
- **Dynamic Data Fetching:** Instead of static datasets, the notebook fetches data dynamically from WRDS at runtime, ensuring analyses always use current financial information.
- **Access Requirements:** Users must have institutional access to WRDS to run this project. If your institution provides WRDS access, you can run the notebook directly.

**For reproducibility:** The notebook uses fixed filter criteria (see `3. Load and Clean Data` section) to ensure consistent data extraction across runs. The SQL query specifies the exact data selection logic, making the analysis transparent and auditable.

---
  
## Limitations
- This notebook is a screening tool, not a definitive judgment of quality or fraud.
- It identifies unusual financial patterns, but not the exact reason behind them.
- Further qualitative analysis is required using company filings, earnings commentary, and industry context.
- The sample covers the full U.S. apparel retail industry (SIC 5600-5699) and may not generalize to other sectors.
- The screening thresholds are currently set at 15% for inventory and fixed asset divergence, and 20% for receivables divergence.
- Growth rate calculations may be sensitive to one-off events, accounting changes, or seasonal fluctuations.
- The analysis assumes consistent financial reporting standards across companies, which may not always hold true.
- Significant growth spikes in specific years (e.g., high fixed asset growth in 2019) may reflect legitimate operational events such as acquisitions, store expansion, capital restructuring, or accounting reclassifications rather than financial anomalies. Users should validate findings against raw financial data and management commentary to understand the drivers.
