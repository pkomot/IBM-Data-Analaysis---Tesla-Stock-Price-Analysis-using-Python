# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This is a single-notebook data analysis project completed as the final assignment for the **IBM Data Analyst Professional Certificate**. Despite the repo name, the notebook analyzes **both Tesla (TSLA) and GameStop (GME)** stock price history alongside their quarterly revenue, then plots each pair on a combined chart.

Repository contents:
- `Final Assignment_Tesla.ipynb` — the entire project: data extraction, web scraping, and visualization, all in one Jupyter notebook.
- `README.md` — project description/portfolio write-up.
- `Python project` — a stray plain-text file (not code) containing the notes "My python project / Final Assignment"; it has no functional role in the analysis.

There is no application code, package, build system, linter, or test suite — everything lives in the notebook's cells.

## Running the notebook

Open and run `Final Assignment_Tesla.ipynb` top-to-bottom in Jupyter (or JupyterLab / VS Code's notebook UI). Required packages, installed/imported inline within the notebook itself:

```
pip install yfinance==0.1.67 pandas numpy requests beautifulsoup4 html5lib plotly
```

- `yfinance` — pulls historical stock price data via `Ticker(...).history(period="max")`.
- `requests` + `BeautifulSoup` (`bs4`, `html5lib` parser) — scrapes revenue tables from static IBM-hosted HTML pages.
- `plotly` (`plotly.subplots.make_subplots`, `plotly.graph_objects`) — renders the combined price/revenue charts. (These imports happen inside the `make_graph` cell context — ensure `plotly` is installed even though the top-level `import plotly...` isn't repeated elsewhere.)

There are no automated tests; correctness is verified by re-running cells and visually inspecting the rendered tables/plots (`tesla_revenue.tail()`, `gme_revenue.tail()`, and the two `make_graph(...)` chart outputs).

## Notebook architecture

The notebook implements the **same two-step pipeline twice**, once for Tesla and once for GameStop, then feeds both into one shared plotting function:

1. **Stock price extraction** (`yf.Ticker("TSLA")` / `yf.Ticker("GME")` → `.history(period="max")` → `reset_index(inplace=True)`) — gives a DataFrame of OHLC price history indexed by date.
2. **Revenue extraction via scraping** — each company's quarterly revenue lives on a separate static HTML page hosted by IBM's course infrastructure (`.../labs/project/revenue.htm` for Tesla, `.../labs/project/stock.html` for GameStop). The notebook `requests.get(url).text`s the page, parses it with `BeautifulSoup(html_data, 'html5lib')`, and manually walks `soup.find_all("tbody")[...]` / `<tr>`/`<td>` to build a `Date`/`Revenue` DataFrame, stripping `$` and `,` from the revenue strings.
3. **Shared `make_graph(stock_data, revenue_data, stock)` function** (defined once, early in the notebook) — builds a 2-row Plotly subplot (share price on top, revenue on bottom) via `make_subplots`, with a shared/synced x-axis and a range slider. It filters each series to a fixed cutoff date (`stock_data.Date <= '2021--06-14'`, `revenue_data.Date <= '2021-04-30'`) before plotting — these cutoffs are hardcoded and specific to when the original assignment was authored, not derived dynamically.

Because both the Tesla and GameStop sections re-import `pandas`, `requests`, and `BeautifulSoup` independently, cells are only guaranteed to work when run in order from the top — don't assume cell independence when editing.

## Conventions to preserve when editing

- Keep the two pipelines (Tesla / GameStop) structurally parallel — the notebook is explicitly organized as paired "Question N" sections that mirror each other.
- The revenue-scraping logic is coupled to the specific HTML structure of the two IBM-hosted pages (table position via `find_all("tbody")[i]`); if either URL/page structure changes, the parsing cells will need corresponding updates.
- `make_graph` is intentionally generic over `stock`/`revenue_data`/label — reuse it rather than writing new one-off plotting cells when adding another ticker.
