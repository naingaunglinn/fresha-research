# Commission: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Commission plan created for **Aung Test Barber**:
> fixed **40%** on all services and products, every day, all locations, effective 27 Sep 2026 (workspace default rules). Then tested
> with Sale #1 (refunded), Sale #3 (service + product), Sale #5 (10% cart discount, then voided). See `test-data-log.md` rows 11, 10–12, 24, 35–36.
> **This module documents Fresha's behaviour only. The business rule for our system is an open owner decision** (`owner-decisions.md`).

## Navigation

- `Team → Team members → Edit → Commissions` ("Set up now" wizard); `Settings → Team → Commissions` (workspace defaults);
  service form `Commissions` section; product form "Enable team member commission"; `Team → Pay runs` (breakdown);
  reports Commission activity / summary.

## OBSERVED

### Configuration

| Level | What can be set | Evidence |
| --- | --- | --- |
| Workspace defaults | **Deduct discounts**, **Deduct taxes**, Deduct service cost, Deduct product cost (all "prior to calculating commission"); earn commission on services paid with a **package** / **membership**; earn full commission when loyalty points are redeemed; **"Earn commissions on fully paid invoices — Commission is only applied on invoices once they are marked as fully paid"**; earn commission even if it exceeds the amount paid; "You can customize commission settings per team member" | `evidence/staff/settings-team-comissions.png` |
| Per team member (wizard) | Type **Fixed rate** or **Tiered** ("higher rates applied once earnings exceed a defined threshold"); rate type **% of sale amount** or **fixed value (SGD)**; default rate; applies to **Services, Service add-ons, Products, Packages, Memberships, Gift cards, Late cancellation and no-show fees**; advanced: **commission rules** (workspace defaults or custom), **Locations** (all / specific), **Days** ("Commission is earned only on scheduled shifts that fall on the selected days"); **effective from** today / future / **past date "to recalculate data reporting"**, ends never / date; **several plans per member** ("Add") | `evidence/commission/setup-01.png`, `evidence/commission/setup-02-fixed.aria.txt`, `evidence/commission/setup-03-advanced.aria.txt`, `evidence/commission/setup-step-4.png`, `evidence/commission/after-apply.png` |
| Per service | "Calculate team member commission when the service is sold" on/off | `evidence/services/service-edit-haircut-tab-commissions.aria.txt` |
| Per product | "Enable team member commission" on/off | `evidence/inventory/products-start-01.aria.txt` |

### Calculation results (tested)

| Event | Pay-run effect (Aung, Baber Shop) | Evidence |
| --- | --- | --- |
| Sale #1: Haircut SGD 40 + tip 4 (checked out 27 Sep for a 29 Sep appointment) | Service commission **SGD 16** (40%), tip SGD 4. Activity: "Commission created — Updated because the commission settings changed" (plan applied the same day) | `evidence/payroll/pay-run-breakdown-aung.png` |
| Refund #2 of the haircut (tip not refunded) | **"Commission deleted — Deleted because the sale was refunded by Naing Aung Linn" −SGD 16**; tip remains | `evidence/payroll/pay-run-breakdown-after-refund.png` |
| Sale #3: Haircut 40 + Pomade 15 (both credited to Aung) | Service **16** + Product **6** | `evidence/payroll/pay-run-breakdown-after-product-sale.png` |
| Sale #5: Haircut 40 + Pomade 15 with **10% cart discount** (49.50) | Service **14.40** (40% × 36) + Product **5.40** (40% × 13.50): the **discount was pro-rated per line and deducted before commission** | `evidence/payroll/pay-run-activity-after-discount.png` |
| Void of Sale #5 | Sale #5 commission lines **disappeared** from the pay-run activity. There's **no "deleted" entry** (unlike refund) | `research-log.md` §17 |

- **Timing:** commission is created **when the sale is checked out** (sale date = checkout date), not when the appointment takes place
  (Sale #1 was checked out 2 days early and counted in the week of 21–27 Sep).
- **Attribution:** commission goes to the **team member on each sale line**. Quick sales default lines to the logged-in user
  unless edited (see `walk-in.md`). "Edit sale details" can change the team member afterwards ("Changes will be reflected in all
  reports").
- Commission appears **per location** in pay runs (Aung has separate Baber Shop and Branch B rows).

### Commission reports

- **Commission summary** (group by team member etc.): Sales qty, Items sold, Gross sales, Refunds, Tax, Discounts, Costs, **Commission
  base**, Commission, % Commission; filters Team member, Location, Type, Service category, Item; export CSV / Excel / PDF.
  Evidence: `evidence/reports/commission-summary.png`
- **Commission activity** ("Full list of all sales with commissions payable"), catalogue only. Evidence: `evidence/reports/reports-index-01.aria.txt`

### Payroll integration

- Commissions flow automatically into **pay runs** (Commissions: Service, Service add-ons, Product, Gift card, Voucher, Membership,
  Package, No-show, Cancellation) together with wages and tips. See `payroll.md`.

## USER-PROVIDED

- Commission calculation is an **open owner decision** (brief §13 and §27). Nothing was assumed.

## INFERRED

- A "completed vs paid" distinction exists in Fresha only through the setting "Earn commissions on fully paid invoices" (commission on
  part-paid invoices is withheld when ON). This setting was left at its default and not toggled.

## NOT VERIFIED

- Tiered commission behaviour (wizard option seen, not configured).
- Location-specific or day-specific commission effects (options seen, not configured).
- Commission on part-paid invoices, packages, memberships, gift cards, no-show / late-cancellation fees.
- Whether the "fully paid invoices" workspace default was ON or OFF: the settings page lists the option without showing its state in
  the captured text.

## Notes for the gap analysis

- Fresha's model can express most likely business rules: % or fixed, per item type, per location, per weekday, tiered, and discount
  / tax / cost deduction toggles. **None of this confirms what the barbershop actually does**. See the owner decisions.
