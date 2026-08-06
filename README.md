# 🏠 Household Expenses Tracker + Net Worth

A single-file, no-backend household finance app. Open `index.html` in any modern browser — all data is stored locally in your browser via `localStorage`.

Two builds are included:

| File | Charts | PDF import | Extras |
|------|--------|------------|--------|
| `index.html` | Chart.js (CDN) | Yes (pdf.js from CDN) | Full version, small file |
| `test.html` | Hand-rolled canvas (no CDN) | Yes (pdf.js embedded, ~2 MB file) | Works fully offline + one-click sample data loader for quick testing |

`test.html` is fully self-contained — no network access needed — so it also works offline and in restricted environments that block CDNs.

## Features

### 📊 Expenses
- Add, edit, and delete expenses with category, "for" item (e.g. a specific car or phone), date, and who paid
- 25 built-in categories plus custom categories (saved for reuse)
- **Recurring expenses** (weekly / bi-weekly / monthly / yearly) that auto-generate entries each time the app opens, with pause/resume
- Monthly summary with total, this-month and average-per-month stats, per-person breakdown, and a spending-by-category chart
- Live search filter and CSV export

### 📥 Statement Import (CSV + PDF)
- **Upload multiple bank and credit-card statements at once** — each file gets its own mapping/preview step
- Statement-type aware: credit card (purchases positive) vs. bank account (money out negative), with a "flip signs" toggle for banks that export the other way, and support for **separate "money out" / "money in" columns**
- **Payments, refunds and deposits are detected automatically** and left unchecked so they don't inflate your spending
- **Duplicate detection**: transactions already in the tracker (same date + amount + description) are flagged and skipped, so re-uploading an overlapping statement is safe
- **Account tagging**: label each statement ("TD Visa", "Chequing"…) and the account shows in the Paid By column
- Automatic column detection with a manual **column-mapping UI** (date / description / amount or debit+credit, header-row toggle)
- Handles quoted CSV fields, `$1,234.56`, negative, trailing-minus, `(parenthesized)` and `12.34 CR` amounts, and multiple date formats (ISO, `MM/DD/YYYY`, `DD/MM/YYYY`, `Jul 12, 2026`, and year-less `Jul 12` / `07/12` with statement-year inference)
- **PDF statements** (text-based, not scanned): transaction lines are reconstructed from the page layout; card-style double dates (transaction + posting) are collapsed and bank-style trailing running balances are ignored
- Auto-categorization from merchant keywords, **and it learns**: when you correct a category before importing, future imports of that merchant (ignoring store numbers) use your choice

### 💰 Net Worth & Debt
- Track assets (cash, investments, real estate, vehicles…) and liabilities (with APR and minimum payment)
- Net worth summary plus asset-allocation and liability-breakdown doughnut charts
- **❄️ Debt snowball calculator**: enter an extra monthly payment and get a month-by-month payoff timeline chart (one line per debt + total), payoff order, debt-free date, and total interest paid — with a warning if payments don't cover interest

## Notes
- Charts use [Chart.js](https://www.chartjs.org/) and PDF parsing uses [pdf.js](https://mozilla.github.io/pdf.js/), both loaded from a CDN. Without internet access the app still works fully — only the charts and PDF import are unavailable.
- Data never leaves your browser. Clearing site data clears the tracker.
