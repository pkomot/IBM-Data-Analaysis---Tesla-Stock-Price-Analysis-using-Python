# 🚗 Tesla & GameStop Stock Price Analysis using Python

This project is the final assignment for the **IBM Data Analyst Professional Certificate** (course: *Python Project for Data Science*). It walks through extracting historical stock and revenue data for **Tesla (TSLA)** and **GameStop (GME)**, then visualizing share price against revenue over time using an interactive dashboard.

## 🎯 Project Objective

Demonstrate proficiency in data extraction, wrangling, and visualization by:
- Pulling historical stock price data directly from Yahoo Finance via the `yfinance` API
- Scraping quarterly revenue data from HTML pages using `requests` and `BeautifulSoup`
- Cleaning and transforming raw text/HTML data into structured Pandas DataFrames
- Building a dual-panel interactive chart (share price vs. revenue) with Plotly

## 📁 Repository Contents

- `Final Assignment_Tesla.ipynb` — Jupyter Notebook containing all the code, analysis, and visualizations.
- `README.md` — Project documentation (this file).

## 🛠️ Tools & Libraries Used

- **Python 3**
- **[yfinance](https://pypi.org/project/yfinance/)** — Pulls historical stock price data for a given ticker
- **Pandas** — Data cleaning, transformation, and DataFrame manipulation
- **Requests** — Fetches raw HTML from revenue data sources
- **BeautifulSoup (bs4)** — Parses HTML tables to extract quarterly revenue
- **Plotly** (`graph_objects` + `subplots`) — Interactive dual-axis stock price / revenue charts
- **Jupyter Notebook** — Interactive development and analysis environment

## 📊 What the Notebook Does

1. **Define a graphing function** — `make_graph()` builds a two-row subplot showing historical share price on top and historical revenue on the bottom, sharing a common time axis.
2. **Extract Tesla stock data** — Uses `yfinance.Ticker("TSLA").history(period="max")` to pull the full price history into `tesla_data`.
3. **Scrape Tesla revenue data** — Downloads an HTML page of Tesla's quarterly revenue, parses it with BeautifulSoup, and cleans the values (strips `$` and `,`) into `tesla_revenue`.
4. **Extract GameStop stock data** — Repeats the same `yfinance` extraction for GME into `gme_data`.
5. **Scrape GameStop revenue data** — Repeats the scraping/cleaning process for GME into `gme_revenue`.
6. **Plot both stocks** — Calls `make_graph(tesla_data, tesla_revenue, 'Tesla')` and `make_graph(gme_data, gme_revenue, 'GameStop')` to visualize price against revenue for each company.

## ▶️ How to Run

1. Clone this repository and open `Final Assignment_Tesla.ipynb` in Jupyter Notebook / JupyterLab.
2. Install the required packages:
   ```bash
   pip install yfinance pandas requests beautifulsoup4 plotly lxml html5lib nbformat
   ```
3. Run all cells from top to bottom. The notebook will fetch live data from Yahoo Finance and the provided revenue data sources, then render interactive Plotly charts inline.

## 🧠 Skills Demonstrated

- API-based data extraction (`yfinance`)
- Web scraping and HTML parsing (`requests`, `BeautifulSoup`)
- Data cleaning and wrangling (`pandas`)
- Interactive, multi-panel data visualization (`plotly`)
- Comparative financial analysis across two companies

## 👤 About the Author

**Julius Kipketer Leley**
- 📚 PhD (Candidate) in Project Management, JKUAT
- 🎓 Certified in IBM Data Analyst, Google Analytics, PMP, PRINCE2, and more
- 🔍 Passionate about IT project management and data analytics
- 🌍 Actively building a portfolio in data-driven decision-making

## 🔗 Connect With Me

- [GitHub](https://github.com/pkomot)
- [LinkedIn](https://www.linkedin.com/in/julius-kipketer-leley-a885b011)

## 🚀 Future Enhancements

- Automate data refresh on a schedule using live APIs
- Extend the comparison to additional tickers (e.g., Ford, Rivian)
- Add moving averages and volatility indicators to the price panel
- Convert the notebook into a standalone interactive dashboard (Plotly Dash / Streamlit)

## 📜 Acknowledgements

This notebook is based on the final assignment from IBM's *Python Project for Data Science* course, part of the IBM Data Analyst Professional Certificate on Coursera.

---
