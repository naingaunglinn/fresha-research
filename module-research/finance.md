# Finance (revenue, expenses, daily closing, reconciliation): Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Register **"ZZTest Register B"** (Branch B) was
> created, opened (float SGD 50), used for a petty-cash cash-out (SGD 5) and closed with a SGD 1 shortage. See `test-data-log.md` rows 28–31.

## Navigation

- `Sales → Daily sales summary | Register | Payments | Sales`; `Reports → Finance / Sales` categories; `Settings → Sales → Registers`.

## OBSERVED

### Revenue and income views

- **Daily sales summary** (live, one day at a time; Previous / Today / Next day; Filters; **Export**; Add new):
  - *Transaction summary* by item type: Services, Service add-ons, Products, Shipping, Gift cards, Packages, Memberships, **Late
    cancellation fees, No-show fees**, Refund amount → Sales qty, Refund qty, Gross total.
  - *Cash movement summary* by payment type: Cash, KBZPay, Other, Gift card redemptions → **Payments collected / Refunds paid**,
    "Of which tips".
  - Example (27 Sep): Services 2 sold / 1 refunded, products 1; Cash collected 75 / refunded −20; KBZPay 24 / −20; total
    collected SGD 99, of which tips SGD 4.
  - Evidence: `evidence/finance/daily-sales-summary-01.png`
- Reports (Finance category): **Finance summary** ("sales, payments and liabilities"), **Payments summary** (by payment method),
  Payment transactions, **Cash flow summary / statement**, Taxes summary / list, Discount summary, Service charges, Liability
  summary / activity, Prepayments, **Cash register summary** (see `reports.md`). Evidence: `evidence/reports/reports-index-01.aria.txt`
- Report data is **not real-time**: headers read "Data from 26–28 mins ago". The Daily sales summary reflected sales immediately.

### Registers = daily opening and closing (performed)

| Step | Observed fields / behaviour | Evidence |
| --- | --- | --- |
| Setup (per location) | Register name (≤32); **Require register to be opened to start taking sales (ON by default)**; Set minimum float; Allow midday counts; Prompt if register was left open; Auto-print / auto-email count report | `evidence/finance/register-start-01.png` |
| Open | Opening float (SGD) + **denomination cash counter** (SGD 1,000/100/50/10/5/2 notes; 1/0.50/0.20/0.10/0.05 coins), note; "Opened by <user> today at 17:11" | `evidence/finance/register-open-01.png`, `evidence/finance/register-open-count.png`, `evidence/finance/register-opened.png` |
| Cash in / Cash out | **Cash-out reasons:** Petty cash for purchases, **Pay team member tips**, Deposit to bank or safe, Other adjustment; amount (+ counter), note, **Add attachment**, user + date stamp | `evidence/finance/register-cash-out.png`, `evidence/finance/register-cash-out-2.png` |
| View | Expected by payment type: Fresha terminals, Tap to Pay, Online, Card, Redemptions (gift cards, deposits, Fresha credit), **Custom methods (Other, KBZPay)**, **Cash = opening float + cash payments + cash in − cash out**; total balance; of which tips; note that online purchases aren't included | `evidence/finance/register-view.png` |
| Close | Table **Expected / Counted / Difference** per payment type; **custom methods (KBZPay) and Cash must be counted manually**; **Cash closing float** ("added to the float of the next day"); **Cash to bank**; note | `evidence/finance/register-close-01.png`, `evidence/finance/register-close-filled.png` |
| Closed record | "Branch B • Sep 27, 2026, 17:11 – 17:13", Cash expected 45 / counted 44 / **−1**; **no approval step and no reason required for the difference** | `evidence/finance/register-closed.png` |

- Register list in Settings → Sales → Registers (All locations / Active). Evidence: `evidence/settings/sales-registers.png`
- The Cash register summary report lists opened by / closed by, counted, difference, cash to bank, closing float per register
  period. Evidence: `evidence/reports/cash-register-summary.aria.txt`

### Expenses, P&L, approvals

- **OBSERVED absence:** there's **no Expenses module** in the navigation, settings or report catalogue, and **no profit & loss report**. The
  only expense-like record is a register **cash-out** ("Petty cash for purchases", with attachment).
  Evidence: `evidence/_nav/nav-d-sales.png`, `evidence/reports/reports-index-01.aria.txt`, `evidence/finance/register-cash-out.png`
- No approval workflow was observed for cash-outs, discounts, refunds or register differences. Refunds require a reason; voids and
  discounts don't.

### Refunds (finance view)

- Refunds are separate documents in the sales sequence (Refund #2) and appear as "Refunds paid" by payment type in the Daily sales
  summary and "No. of refunds / Refunds" in Payments summary. Evidence: `evidence/reports/payments-summary.png`

### Reconciliation

- Payment-method reconciliation = **register close counts** (expected vs counted per method, including KBZPay) plus the Payments
  summary report. No bank or KBZPay statement import was observed.

### Audit

- Sale activity (90 days) records creation, payments (who took them), void. Register periods record opened/closed by and times.
  Cash-out entries record the user and date. (See `audit-log.md`.)

## USER-PROVIDED

- Brief §12 lists expenses, company-wide expenses, daily closing and P&L as research topics. Brief §27 lists **company-wide expense
  allocation** and **daily closing workflow** as open owner decisions.

## INFERRED

- With the default "Require register to be opened to start taking sales" ON, a branch that forgets to open its register can't take
  in-person sales. Not tested by attempting a sale while closed.

## NOT VERIFIED

- Sale blocking while the register is closed (not attempted).
- Finance summary, Cash flow statement and Liability report contents (catalogue only).
- Currency denominations for **MMK** in the cash counter.
- Bank deposits / Fresha wallet payouts (no billing details, no Fresha Payments).

## Notes for the gap analysis

- Fresha provides a **daily closing mechanism (registers)** but **no expense tracking or P&L**. Company-wide expense allocation has no
  equivalent in Fresha.
