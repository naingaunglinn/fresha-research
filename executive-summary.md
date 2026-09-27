# Executive Summary: Fresha Research & Gap Analysis

**Date:** 2026-09-27 · **Researcher:** Claude (AI agent), driving a dedicated browser the user logged into
**Workspace researched:** "Baber Shop", the user's **test/sandbox** Fresha workspace (trial plan, **Singapore / SGD**), extended with a second
location, two test barbers, test clients, products, sales, a register, a commission plan and pay-run data (all listed in `test-data-log.md`).
**Not researched:** the barbershop's **live** account (Myanmar / MMK, per the user). Country-specific behaviour (MMK formatting, +95 validation,
Myanmar addresses, cash denominations) is therefore **NOT VERIFIED**.

## Executive Summary

1. **Fresha already does most of what the planned system intends at the feature level.** It supports:
   - multi-branch staff with per-branch shifts, including the Monday 09–13 Branch A / 14–18 Branch B split;
   - branch-specific service eligibility, and **price/duration per branch and even per barber within a branch**;
   - "Any Barber" with several assignment strategies;
   - branch-level stock with **native transfers** (partial receipt);
   - split payments with a custom KBZPay method;
   - daily cash registers (opening float, counted vs expected);
   - automatic commission (created at checkout, reversed on refund);
   - pay runs;
   - timesheets with a 50 m location check;
   - ~60 reports with CSV / Excel / PDF export.
2. **Fresha's weaknesses are in rules, controls and localisation, not in missing screens:**
   - staff can **double-book a barber across branches** (only a soft warning);
   - the same customer can hold several future bookings;
   - duplicates are merged afterwards (the merge kept the newer name);
   - quick-sale lines are **credited to the logged-in user** by default;
   - there's no reason or approval for voids, discounts or register differences;
   - the audit trail is uneven: no client, staff or settings history, and cancellation reasons aren't logged;
   - there's **no Burmese UI**, no date-format setting, and the advance booking window is **1–12 months only (no 14 days)**;
   - **wages are hourly only**;
   - there's **no expense tracking or P&L**;
   - report data was 26–28 minutes old when viewed (refresh schedule not verified);
   - QR attendance is absent.
3. **Most open questions are business rules, not features.** Sixteen owner decisions are listed (7 known + 9 surfaced by the research).
   The biggest are commission, payroll, daily closing / KBZPay reconciliation, customer identity (including whether "no SMS OTP" covers customers), and the one-active-booking edge cases.

## Major Fresha Strengths (OBSERVED)

- **Branch × barber pricing** with cascade (service → location → barber-at-location) and a "from" price for Any. Price changes can optionally update
  existing bookings. (`module-research/services.md`)
- **Cross-branch awareness in availability:** a barber's booking at Branch B blocks their time at Branch A, and multi-service bookings chain across
  barbers correctly (first slot moved from 10:00 to 10:15). (`module-research/booking.md`)
- **Rich scheduling:** repeating shifts per location (1–4-week patterns, multiple segments per day), partial-day leave, closed periods per
  location, waitlist, slot-gap optimisation. (`module-research/schedule.md`)
- **Payments:** split and part-paid sales; "cash received by" and "payment taken by" per payment; refunds per original method with a mandatory
  reason; clear irreversible-action dialogs (void shows the stock that will be returned). (`module-research/payments.md`)
- **Inventory:** per-location stock and reorder levels; stocktakes with review and difference cost; transfers with partial receipt; stock history
  with the reason and the on-hand quantity after each entry. (`module-research/inventory.md`)
- **Commission and pay runs** integrated with sales: refund reversal, discount deduction, per-location rows, adjustments, review/approval, step-up
  verification. (`module-research/commission.md`, `module-research/payroll.md`)
- **Daily closing** via registers: expected vs counted per payment method (KBZPay included), float carry-over, cash to bank, petty cash with
  attachment. (`module-research/finance.md`)
- **Granular permissions** (121 toggles) including branch scope and client phone visibility. (`module-research/roles-permissions.md`)
- **Responsive web** usable at phone and tablet widths, with a bottom navigation on mobile. (`ux-analysis.md`)

## Major Fresha Pain Points

**OBSERVED in this session** (no first-hand pain points were supplied by the user; nothing below is USER-PROVIDED):

1. **Barber attribution errors are easy:** quick-sale service and product lines default to the logged-in user, and fixing each line costs ~3 clicks.
   A walk-in sale can't be attached to a customer after payment.
2. **Double booking across branches isn't prevented:** there's only an inline "Team member is not available". Default shifts for a two-branch barber overlap
   at both branches.
3. **Key actions are hidden** under "Options" (reschedule, cancel, no-show, void, refund), and reschedule can't move a booking to another branch.
4. **One branch per calendar view**, so managers switch location repeatedly.
5. **Localisation gaps:** no Burmese; no date-format setting; inconsistent 12/24 h display; the receipt printed "$" for SGD.
6. **Controls:** no reason or approval for discounts, voids or cash differences. Cancellation reason is optional and isn't logged. Voids erase commission
   lines without trace.
7. **Reporting:** report data was 26–28 minutes old when viewed; the refresh schedule wasn't verified. Daily/monthly grouping and custom reports need the paid Insights add-on. No expense or P&L reporting.
8. **Checkout length:** always passes the tip step; a split Cash + KBZPay payment takes ~12 clicks.
9. **Paid-for essentials:** deposits and no-show fees need Fresha Payments (card); SMS and WhatsApp reminders need a paid balance.

## Important Differences (Fresha vs our planned system)

| Planned (brief §26) | Fresha | Details |
| --- | --- | --- |
| 14-day default advance window | Minimum option is **1 month** | `gap-analysis.md` A |
| One active booking per customer | **Not enforced** (staff side) | A |
| Myanmar + English UI | **No Burmese** | A |
| DD/MMM/YYYY | **No date-format setting** | A |
| QR + location attendance | Location distance check only; **no QR** | A |
| No SMS OTP (customer scope not stated) | Fresha's customer login offers a phone SMS code first, or email / Google / Apple | A, B-6, OD-11 |
| Excel/CSV import | **CSV only**, clients and products only; duplicates rejected | A |
| Cash + KBZPay | KBZPay possible as a **name-only** custom method, no reference | A |
| Branch-specific price/duration | Fresha also supports **per-barber** price/duration | A (owner decision OD-8) |

## Missing Features

**Not provided by Fresha (OBSERVED absence):**
- expense tracking and P&L;
- company-wide expense allocation;
- QR attendance and device checks;
- Burmese language;
- date-format setting;
- a 14-day booking window;
- per-branch roles;
- client, staff and settings change history;
- loan and advance tracking;
- monthly salary type;
- a combined multi-branch calendar;
- a KBZPay reference and reconciliation;
- a preferred-barber field.

**Could not be verified:**
- the live account's configuration and MMK formatting;
- the barber's own view and mobile app, and notifications to other staff;
- the paid state and period locking of pay runs (blocked by an emailed verification code);
- customer self-booking against our own configuration (the marketplace profile was not published);
- a low-stock alert firing;
- the reschedule audit entry;
- Premium reports.

## Potential Risks

1. **Attribution and commission disputes** if walk-ins, quick sales or early checkouts are allowed to default to the operator or shift pay
   periods (Fresha evidence: logged-in-user default; checkout-date revenue).
2. **Double booking of multi-branch barbers** if overlapping shifts and conflict overrides aren't validated (Fresha auto-creates overlapping
   shifts).
3. **Customer identity:** if "no SMS OTP" also covers customers, the one-active-booking rule and duplicate prevention need another reliable key (OD-11).
4. **Cash and KBZPay reconciliation** gaps if KBZPay isn't referenced and differences need no reason or approval.
5. **Data migration from Fresha:** Fresha's client export has **no visit count, total spend or last visit**. Importing history will need other
   sources (sales / appointment exports). Duplicates must be resolved before import.
6. **Scope creep:** Fresha has many salon, spa and marketplace features (packages, memberships, gift cards, loyalty, forms, patch tests, resources,
   AI concierge). Copying them isn't justified by the brief.
7. **Reporting expectations:** owners used to Fresha may expect its report catalogue. Fresha's delayed report data (26–28 min old when viewed) and paid time-grouping mean
   "the same as Fresha" is itself limited.
8. **Research limits:** observations come from a Singapore sandbox with 2 locations and 3 bookable staff, not the live 3-branch / 15-barber account.

## Owner Decisions

See `owner-decisions.md` (**OWNER DECISIONS STILL NEEDED**):

- OD-1 commission calculation
- OD-2 KPI rules
- OD-3 preferred-barber threshold
- OD-4 payroll rules (salary type, advances, deductions, tips, cash kept by barbers, multi-branch split)
- OD-5 company-wide expense allocation
- OD-6 daily closing and KBZPay reconciliation
- OD-7 barber dashboard visibility
- OD-8 barber-level pricing
- OD-9 "Any Barber" distribution
- OD-10 one-active-booking edge cases
- OD-11 customer identity and the scope of "no SMS OTP"
- OD-12 overrides, reasons and approvals
- OD-13 leave requests and approval
- OD-14 no-show / late-cancellation consequences
- OD-15 taxes and service charges
- OD-16 customer reminders channel

## Recommended Next Research

Only where something genuinely remains unclear.

> **Deadline:** the sandbox is on a **free trial that ends around 2026-10-04** (banner on 2026-09-27: "free trial ends in 7 days"). Items 2, 4 and
> 5 use this sandbox and must happen **before then**, unless the trial is extended or the plan activated.

1. **Live account check with the owner (30–60 min, read-only):**
   - MMK formatting on screen and receipts;
   - how many locations, staff and roles are configured;
   - whether packages, memberships, gift cards, waitlist, booking links or QR are actually used;
   - current commission and pay-run settings (these would show the *current* rules behind OD-1 and OD-4).
2. **Barber view:** invite one barber-level test login (Basic role) to confirm what barbers see and which notifications they receive.
3. **Fresha mobile app** (barber side): clock-in with the 50 m check, leave requests, notification delivery.
4. **Pay-run completion:** have the owner enter the emailed code once on a test run to observe the paid and locked state.
5. **Customer self-booking** against our own configuration, only if the owner accepts briefly publishing the test profile.
