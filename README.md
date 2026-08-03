# 🏠 Household Expenses Tracker + Net Worth

A single-file, no-backend household finance app. Open `index.html` in any modern browser — all data is stored locally in your browser via `localStorage`.

Two builds are included:

| File | Charts | PDF import | Extras |
|------|--------|------------|--------|
| `index.html` | Chart.js (CDN) | Yes (pdf.js CDN) | Full version |
| `test.html` | Hand-rolled canvas (no CDN, works offline) | No (CSV only) | One-click sample data loader + "clear all" button for quick testing |

`test.html` is fully self-contained — no network access needed — so it also works in restricted environments that block CDNs.

## Features

### 📊 Expenses
- Add, edit, and delete expenses with category, "for" item (e.g. a specific car or phone), date, and who paid
- 25 built-in categories plus custom categories (saved for reuse)
- **Recurring expenses** (weekly / bi-weekly / monthly / yearly) that auto-generate entries each time the app opens, with pause/resume
- Monthly summary with total, this-month and average-per-month stats, per-person breakdown, and a spending-by-category chart
- Live search filter and CSV export

### 📥 Statement Import (CSV + PDF)
- Import bank/credit-card statements from CSV or text-based PDF files
- Automatic column detection with a manual **column-mapping UI** (date / description / amount, header-row toggle)
- Handles quoted CSV fields, `$1,234.56`, negative, trailing-minus, and `(parenthesized)` amounts, and multiple date formats (ISO, `MM/DD/YYYY`, `DD/MM/YYYY`, `Jul 12, 2026`)
- Auto-categorization from merchant keywords (editable per row before import)
- Preview table with per-row checkboxes so you can skip payments/credits

### 💰 Net Worth & Debt
- Track assets (cash, investments, real estate, vehicles…) and liabilities (with APR and minimum payment)
- Net worth summary plus asset-allocation and liability-breakdown doughnut charts
- **❄️ Debt snowball calculator**: enter an extra monthly payment and get a month-by-month payoff timeline chart (one line per debt + total), payoff order, debt-free date, and total interest paid — with a warning if payments don't cover interest

## Notes
- Charts use [Chart.js](https://www.chartjs.org/) and PDF parsing uses [pdf.js](https://mozilla.github.io/pdf.js/), both loaded from a CDN. Without internet access the app still works fully — only the charts and PDF import are unavailable.
- Data never leaves your browser. Clearing site data clears the tracker.
