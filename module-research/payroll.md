# Payroll (pay runs): Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Aung Test Barber: hourly SGD 5, 40% commission; one manual
> timesheet (6 h) at Branch B; sales at Baber Shop. The pay-run wizard was taken to **"Complete"**, which demanded an emailed
> **verification code**. The research brief forbids handling OTP codes, so the run was **not completed**.
> **Payroll business rules are open owner decisions.**

## Navigation

- `Team → Pay runs` (`/team/payrun/overview`): Pay periods / Settlements; `Settings → Team → Pay runs`; team member form sections
  **Wages and timesheets**, **Commissions**, **Pay runs**.

## OBSERVED

### Salary and wages

- Compensation type per team member: **None / Hourly pay** only. There's **no monthly or fixed salary type**. Hourly rate, optional **Overtime
  pay** ("earn overtime when working above their regular hours"). Evidence: `evidence/staff/add-team-member-hourly-pay.aria.txt`
- Wages are computed from **timesheet hours** (Aung: 6 h × SGD 5 = **SGD 30** at Branch B). Evidence: `research-log.md` §14
- Blocked-time types carry **Paid / Unpaid** (Lunch 30 min Unpaid; Training and Meeting 1 h Paid). Evidence: `evidence/settings/scheduling-blocked-time-types.png`

### Pay periods

- Frequency: **Daily, Weekly, Every 2 weeks, Every 4 weeks, Semi-monthly, Monthly, Quarterly**; restarts on (weekday); starts from next
  billing cycle / custom date; schedule preview. Default in sandbox: Weekly, Monday. Evidence: `evidence/staff/settings-team-pay-runs-edit.aria.txt`
- Automatic payouts (wages, commissions, other; tips separately) from the Fresha business wallet: disabled; manual pay by default.

### Pay-run overview and breakdown

- Overview per period (e.g. Sep 21–27) filtered by location: Earnings, Other, Total, Paid, To pay, **Pay team**. **One row per team member
  per location** (Aung appears for Baber Shop and for Branch B). Evidence: `evidence/payroll/pay-runs-start-01.png` (overview after onboarding), `evidence/payroll/pay-runs-start-01.aria.txt`
- Row actions: **View breakdown, Pay, Edit team member, Add adjustment**. Evidence: `evidence/payroll/pay-run-row-actions.png`
- **Breakdown** (Overview tab): Wages (hourly rate, regular hours, regular total, overtime rate/hours/total); **Commissions** (Service,
  Service add-ons, Product, Gift card, Voucher, Membership, Package, No-show, Cancellation); **Tips** (At checkout, Pay by app, Terminal,
  After checkout); **Other** (payment processing fees, new client fees, other adjustments); Paid; To pay. **Activity** tab lists each
  earning event with reference number (e.g. "Commission created… 1 Service commission SGD 16", "Tip created… Tip at checkout SGD 4",
  "Commission deleted… refunded"). Evidence: `evidence/payroll/pay-run-breakdown-aung.png`, `evidence/payroll/pay-run-breakdown-after-refund.png`

### Deductions, advances, loans

- **Add adjustment**: tabs Wages / Commissions / Tips / Other; amount; **+ Add / − Deduct**; Add note. Evidence: `evidence/payroll/add-adjustment.png`
- Automatic deductions available per member: **Fresha payment processing fees**, **Fresha new client fees**. Evidence: `evidence/staff/add-team-member-pay-runs.aria.txt`
- **Cash advances** option per member: "Record cash payments for sales as 'paid' in pay runs — When a sale is paid in cash, record that this
  team member has taken the full cash amount as an advance within the pay period." Evidence: same file
- **OBSERVED absence:** there's no dedicated loan object, instalment schedule or advance register. Advances and loans can only be expressed as
  manual "Other / Deduct" adjustments.
- **OBSERVED absence:** no automatic attendance or leave deductions. Wages follow recorded timesheet hours, so missing hours simply aren't paid.

### Approval, finalisation, payment

1. `Pay team` / `Pay now` → **Team members pay run summary** (period, include-members checkboxes, wages / commissions / tips / other / total /
   paid / to pay, per-member Actions for adjustments, **Save and exit**). Evidence: `evidence/payroll/pay-run-step-2.png`
2. **Review pay run** per location: wallet balance ("SGD 0 available"), total to pay, period, date, **payment method "Paid manually"
   (Edit)**, Add note, review status **Needs review / Approved ("approved for payout") / Skip ("save changes for later")**.
   **Complete is blocked until every location is Approved or Skipped** ("Mark all locations as ready or skipped").
   Evidence: `evidence/payroll/pay-run-step-3b.png`, `evidence/payroll/pay-run-approved.png`
3. **Complete** → **"Enter verification code — A 4 digit code has been emailed to n***@gmail.com"** (5-minute timer, step-up
   authentication). Cancelled. Evidence: `evidence/payroll/pay-run-verification-code-prompt.png`
4. Leaving the wizard → "Leave pay run — unsaved changes will be discarded".

### Payroll reports (catalogue)

- **Pay summary** ("Overview of team member compensation"), Wages detail ("across locations") / summary, Commission activity / summary,
  Tips summary / detail, Fee deduction activity / summary, Working hours activity / summary. Evidence: `evidence/reports/reports-index-01.aria.txt`
- Marketing copy on the pay-run onboarding: "Share detailed earning reports for each team member".
  Evidence: `evidence/payroll/pay-runs-overview-01.aria.txt`

### Branch allocation

- Earnings are split **by location** (row per member per location), so a multi-branch barber is paid in several location rows.
  The review step groups payment by location ("Baber Shop — SGD 0 available").

## USER-PROVIDED

- Payroll-specific business rules are **open owner decisions** (brief §14 and §27).

## INFERRED

- The step-up verification suggests Fresha treats completing a pay run as a sensitive financial action even when paid manually.

## NOT VERIFIED

- Completed / paid state, **payroll locking**, and whether later sales in a paid period create new "to pay" amounts. The code step blocked this.
- Payslips: no payslip document observed. Whether the "earning reports" are shareable payslips is NOT VERIFIED.
- Automatic payouts (require Fresha wallet / bank).
- Overtime calculation, tiered commissions in pay runs, tips paid out from the register ("Pay team member tips" cash-out).

## Notes for the gap analysis

- Hourly-only wages, no loan or advance tracking, and no leave or attendance deductions are material differences if the barbershop pays
  monthly salaries or gives advances. Owner input is required.
