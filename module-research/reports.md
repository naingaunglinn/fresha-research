# Reports: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Catalogue fully captured. Six reports opened in detail
> (Sales summary, Payments summary, Cash register summary, Commission summary, Attendance summary; Daily sales summary under Sales).
> **Premium** reports need the paid **Insights** add-on. The sandbox trial showed "Premium" badges.

## Navigation

- `Reports` (`/reports`): All reports (60), Favourites, **Dashboards (4)**, **Standard (51)**, **Premium (9)**, Custom (0), Folders,
  **Data connector**; category filter **Sales, Finance, Appointments, Team, Clients, Inventory, Other**.
  Evidence: `evidence/reports/reports-index-01.png`, `evidence/reports/reports-index-01.aria.txt`

## OBSERVED: catalogue (names and descriptions as shown)

Report names, descriptions and the Premium (P) marks are OBSERVED. **The grouping into categories in the left column is INFERRED** from
the catalogue order; the UI offers category filters but I didn't record each report's category.

| Category (INFERRED grouping) | Reports |
| --- | --- |
| Dashboards | Performance dashboard; Online presence dashboard; Loyalty dashboard; AI Concierge dashboard |
| Sales | Performance summary (P); Performance over time (P); **Sales summary**; Sales by time period (P); **Sales list**; Sales log detail; Gift card by time period (P); Gift card list; Membership list; Packages list; Packages summary; Packages benefits consumption (P) |
| Finance | **Cash register summary**; Discount summary; Taxes summary; **Finance summary**; **Payments summary**; **Payment transactions**; **Cash flow summary**; **Cash flow statement**; Service charges; Liability summary; Liability activity; Prepayments by time period (P); Prepayment list; Taxes list |
| Appointments | **Appointments summary** ("including cancellations and no-shows"); **Appointments list**; **Appointments cancellations & no-show summary**; Waitlist detail; Waitlist summary (P) |
| Team | Working hours activity; Break activity; **Attendance summary**; Wages detail; Wages summary; Fee deduction activity; Fee deduction summary; **Pay summary**; Scheduled shifts; Working hours summary; Team time off report; **Tips summary**; Tips detail; **Commission activity**; **Commission summary** |
| Clients | Client summary (P, "new, returning and walk-in clients"); **Client list**; Client insights (P) |
| Inventory | **Stock on hand**; **Stock movement summary**; **Stock movement log**; Product list; Ordered stock |
| Other | AI Concierge summary; AI Concierge activity |

(P) = Premium. **OBSERVED absence:** no Expense report, **no Profit & Loss**, no dedicated branch comparison report (branch
comparisons are done with the Location filter / "Group by Location").

## OBSERVED: common report controls

- Header "**Data from N mins ago**" (26–28 min observed). Sale #3, made shortly before viewing, wasn't yet included. The refresh schedule itself is NOT VERIFIED. Reports are **not real-time**.
- Date range presets (Today, Yesterday, Last 7/30/90 days, Last month/year, Week/Month/Quarter/Year to date, Tomorrow, Next 7 days, Next
  month, Next 30 days, All time) + custom range. Evidence: `evidence/booking/appointments-list-date-range.png`
- **Filters** drawer (varies): Location, Team member, Status, Channel, Type, Loyalty sales, Client tags, Client segments; Premium filters:
  Client gender, Client retention, Supplier, Brand, Product category, Service category. Evidence: `evidence/reports/sales-summary.aria.txt`
- **Group by** (Sales summary): Type, Category, Item, **Team member**, Resource, Client, Loyalty sales, Channel, **Location**, Client tags, Client
  segments; **Premium: Source, Gender, Retention, Hour, Day, Month, Quarter, Year**. So grouping by day/month needs Insights.
  Evidence: `evidence/reports/sales-summary-groupby.png`
- **Customize** (columns, grouping, date picker, default filters, charts) requires the Insights add-on ("Upgrade now to create customized
  reports"; "Grouping 18 of 28 available", "Columns 8 of 25").
- **Options:** Duplicate, Add to favorites, **Export → CSV / Excel / PDF**. Evidence: `evidence/reports/sales-summary.png`

## OBSERVED: reports opened

| Report | Columns / metrics | Filters | Evidence |
| --- | --- | --- | --- |
| Sales summary | Type, Sales qty, Items sold, Gross sales, Total discounts, Refunds, Net sales, Taxes, Total sales | Location, Team member, Status, Channel, Type, Loyalty, Client tags/segments (+Premium) | `evidence/reports/sales-summary.png` |
| Payments summary | Payment method, No. of payments, Payment amount, No. of refunds, Refunds, Net payments (Cash and KBZPay separate) | Location, Team member, Type | `evidence/reports/payments-summary.png` |
| Cash register summary | Date, Register, Opening by, Fresha terminals, Fresha online, Redemptions, Custom methods, Cash opening float, Cash payments, Cash in, Cash out, Cash total, Cash counted, Cash difference, Custom methods difference, Total balance, Of which tips, Closed by, Counted, Cash to bank, Cash closing float | Location, Register, Opened by | `evidence/reports/cash-register-summary.png` |
| Commission summary | Team member, Sales qty, Items sold, Gross sales, Refunds, Tax, Discounts, Costs, Commission base, Commission, % Commission | Team member, Location, Type, Service category, Item | `evidence/reports/commission-summary.png` |
| Attendance summary | Team member, Scheduled shifts, On time / Early / Late clock ins, On time / Early / Late clock outs, Punctuality, Missed shifts, Attendance | Team member, Location | `evidence/reports/attendance-summary.png` |
| Daily sales summary (Sales menu, live) | Transaction summary by item type; cash movement by payment type; tips | Filters, day navigation, Export | `evidence/finance/daily-sales-summary-01.png` |

## OBSERVED: lists with export (outside Reports)

- Sales list (PDF / CSV / Excel), Appointments list (Export), Clients (Excel / CSV), Team (CSV / Excel), Products (CSV / Excel), Service menu
  (PDF / Excel / CSV), Stock history (Excel / CSV / PDF).

## Permissions

- Default roles Basic / Low / Medium / High all had "**Can access reports**" unticked and "Can view all team members' data" ticked. The owner has
  full access. Evidence: `evidence/roles/permission-matrix.md`

## USER-PROVIDED

- Planned export formats: **Excel / CSV / PDF** (brief §26).

## NOT VERIFIED

- Contents of the reports that weren't opened (e.g. Finance summary, Cash flow statement, Client list report, Stock on hand, Appointments
  summary, Pay summary).
- Premium reports (Insights add-on not purchased).
- Data connector (add-on).
- Exact refresh schedule of report data (only the "N mins ago" label was seen).

## Notes for the gap analysis

- Payroll, expense and P&L reporting are thin or absent. Branch comparison works by filter or grouping. Time-series grouping (day/month) and
  custom reports are **paid extras**.
