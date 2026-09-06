# 🏠 Household Expenses Tracker + Net Worth

A single-file, no-backend household finance app: expenses with statement import, net worth and debt payoff, and a records vault for vehicles, homes, policies and accounts. Open `index.html` in any modern browser — all data is stored locally in your browser via `localStorage`.

Two builds are included:

| File | Charts | PDF import | Extras |
|------|--------|------------|--------|
| `index.html` | Chart.js (CDN) | Yes (pdf.js from CDN) | Full version, small file |
| `test.html` | Hand-rolled canvas (no CDN) | Yes (pdf.js embedded, ~2 MB file) | Works fully offline + one-click sample data loader for quick testing |

`test.html` is fully self-contained — no network access needed — so it also works offline and in restricted environments that block CDNs.

## Features

### 📊 Expenses
- Add, edit, and delete expenses with category, "for" item (e.g. a specific car or phone), date, and who paid
- 26 built-in categories (including **Transfers** for Interac e-Transfers, EFTs and account transfers) plus your own categories **and sub-categories** (e.g. Insurance › Home): add them from the 🏷️ Categories panel or inline from the category picker, use them everywhere a category is chosen (expense form, import preview, recurring bills), and remove them again with expenses moved to the parent category (or Other)
- The spending chart rolls sub-categories up to their parent category
- **Turn an existing category into a sub-category, or a sub-category back into its own category**: every top-level category (built-in or custom) that has no sub-categories of its own can be moved under another one with one click, moving its expenses and its learned merchant mapping with it; a ↑ button on any sub-category promotes it back to top-level
- **Recurring expenses** (weekly / bi-weekly / monthly / yearly) that auto-generate entries each time the app opens, with pause/resume
- Monthly summary with total, this-month and average-per-month stats, per-person breakdown, and a spending-by-category chart
- **Change a category right in the All Expenses table**: each row's category is a dropdown; picking a new one saves instantly, updates the chart, and teaches the merchant → category mapping used by future imports
- Live search filter and CSV export

### 📥 Statement Import (CSV + PDF)
- **Upload multiple bank and credit-card statements at once** — each file gets its own mapping/preview step
- Statement-type aware: credit card (purchases positive) vs. bank account (money out negative), with a "flip signs" toggle for banks that export the other way, and support for **separate "money out" / "money in" columns**
- **Payments, refunds and deposits are detected automatically** and left unchecked so they don't inflate your spending, each labelled with why (e-Transfer received, deposit / money in, refund, interest, payment / credit)
- **Opening / closing balance and column-total lines are never treated as expenses**: PDF import drops them, CSV import shows them unchecked as "balance row", and if any slipped in from an earlier import the All Expenses card offers a one-click cleanup
- **Duplicate detection**: transactions already in the tracker (same date + amount + description) are flagged and skipped, so re-uploading an overlapping statement is safe
- **Account tagging**: label each statement ("TD Visa", "Chequing"…) and the account shows in the Paid By column
- **Imported Statements list**: every import is logged with file name, account, transaction count, date range, and import date — remove a statement to remove its transactions too
- **Visible feedback everywhere**: import progress, results, and errors show as in-page status text and toasts (browser popups are suppressed in embedded/sandboxed viewers, so the app never relies on them); destructive buttons use a click-twice confirm
- Automatic column detection with a manual **column-mapping UI** (date / description / amount or debit+credit, header-row toggle)
- Handles quoted CSV fields, `$1,234.56`, negative, trailing-minus, `(parenthesized)` and `12.34 CR` amounts, and multiple date formats (ISO, `MM/DD/YYYY`, `DD/MM/YYYY`, `Jul 12, 2026`, `02 Jan 2026` / `2-Jan-26`, and year-less `Jul 12` / `07/12` / `02 Jan` with statement-year inference)
- **PDF statements** (text-based, not scanned): transaction lines are reconstructed from the page layout; card-style double dates (transaction + posting) are collapsed, bank-style trailing running balances are ignored, and a recipient / reference line printed under a transaction (typical for e-Transfers) is joined onto its description. Bank statements with separate **Money out / Money in** (withdrawals / deposits) columns are read column-aware using the statement's own header row, so deposits are never counted as spending; opening/closing balance rows are skipped
- Auto-categorization from merchant keywords, **and it learns**: when you correct a category before importing, future imports of that merchant (ignoring store numbers) use your choice

### 🗂️ Records (vehicles, homes, policies, accounts)
- A third tab for the details you'd want in a pinch, kept in one place: **Vehicles** (make, model, year, VIN, plate, purchase price and date, dealer, lender, loan APR, amortization, payment amount and frequency, insurance provider and policy number, odometer), **Homes / Property** (address, purchase price, current value, mortgage lender, rate, amortization, renewal date, payment, property tax, home insurance), **Insurance Policies** (type, provider, policy number, coverage, premium and frequency, beneficiary, start date, agent), **Investment / Savings Accounts** (RRSP, TFSA, FHSA, RESP, RRIF, non-registered, pension — institution, account number, balance, contribution room, advisor, beneficiary), and **Other** for anything else
- Every record can carry **custom fields** (any label + value, e.g. "Warranty expires — May 2027") on top of the preset ones, plus free-form notes
- Records are grouped by type with a one-line summary; expand any card for the full detail list, edit it in place, or delete it (click-twice confirm). Search matches every field, not just the name
- Export all records to CSV (one row per detail so every type fits the same columns)

### 💰 Net Worth & Debt
- **Connected to Records**: a vehicle or home with a current value (or purchase price as a fallback), an account balance, or a whole-life policy's cash value counts as an asset automatically, and a vehicle loan or mortgage balance counts as a liability, with the loan's APR and its monthly-equivalent payment (bi-weekly, weekly, semi-monthly and annual payments are converted). These rows are tagged "from Records" and link back to the record for editing
- Manual assets (cash, investments, real estate, vehicles…) and liabilities (with APR and minimum payment) for anything that has no record
- Net worth summary plus asset-allocation and liability-breakdown doughnut charts
- **❄️ Debt snowball calculator**: enter an extra monthly payment and get a month-by-month payoff timeline chart (one line per debt + total), payoff order, debt-free date, and total interest paid — with a warning if payments don't cover interest

## Notes
- Charts use [Chart.js](https://www.chartjs.org/) and PDF parsing uses [pdf.js](https://mozilla.github.io/pdf.js/), both loaded from a CDN. Without internet access the app still works fully — only the charts and PDF import are unavailable.
- Data never leaves your browser. Clearing site data clears the tracker.
