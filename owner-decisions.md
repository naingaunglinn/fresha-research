# Owner Decisions

These are business rules that **only the barbershop owner can confirm**. For each, the research shows what Fresha does, so the owner can
see the realistic options. **Nothing here is decided.** Fresha's behaviour is a reference, not a recommendation.

## OWNER DECISIONS STILL NEEDED

### Known open areas (brief §27)

**OD-1 · Commission calculation**
- Questions:
  - Is commission a percentage or a fixed amount?
  - Does it differ by service, product, barber or branch?
  - Is it computed on the price **before or after discounts** and taxes?
  - Is it earned when the service is **completed** or when it is **paid**?
  - What happens on refund and void?
  - Does it follow the **service date or the payment date**?
- Fresha reference (OBSERVED):
  - % or fixed amount, per item type, per location, per weekday, tiered.
  - Toggles to deduct discounts, taxes or cost, and "only on fully paid invoices".
  - Commission created at checkout, deleted on refund, removed without trace on void.
  - Cart discounts pro-rated before commission.
  - Checkout date drives the pay period.
- Evidence: `module-research/commission.md`, `evidence/payroll/pay-run-activity-after-discount.png`

**OD-2 · KPI rules**
- Question: which KPIs are tracked per barber and per branch, and how is each defined? Examples: services count, revenue (gross or net of discounts
  and refunds), product sales, punctuality or attendance, no-show rate, repeat customers.
- Fresha reference (OBSERVED):
  - Reports on sales, commission, tips, attendance (on-time, late, missed shifts, punctuality %) and cancellations or no-shows.
  - "Top team member" and "Top services" dashboard widgets.
  - Time-series grouping is a paid add-on.
- Evidence: `module-research/reports.md`

**OD-3 · Preferred barber threshold**
- Question: when does a barber count as a customer's "preferred" barber (e.g. N of the last M visits), and what does the system do with it?
- Fresha reference (OBSERVED): there's no preferred-barber field; the only related option is "Prioritize last booked team member" for "Any"
  bookings.
- Evidence: `module-research/customers.md`, `evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt`

**OD-4 · Payroll-specific rules**
- Questions:
  - Monthly salary, hourly, commission-only, or a mix?
  - Pay period?
  - Advances and loans (tracked how, repaid how)?
  - Deductions for absence, lateness or leave?
  - Who owns **tips**, and how are they paid out?
  - Can barbers keep cash from sales as an advance?
  - How is a multi-branch barber's pay split across branches?
- Fresha reference (OBSERVED):
  - **Hourly only**, with no salary type.
  - Periods from daily to quarterly.
  - Manual +/− adjustments.
  - Option "record cash payments for sales as paid (advance)".
  - Tips go to the service provider and flow into pay runs; register cash-out has "Pay team member tips".
  - Pay rows are per member per location.
  - Review Approved/Skip and an emailed verification code to complete.
- Evidence: `module-research/payroll.md`

**OD-5 · Company-wide expense allocation**
- Question: which expenses are company-wide versus branch-level, and how are company-wide costs allocated to branches (equal split, by revenue,
  by headcount, other)?
- Fresha reference: **no expense module and no P&L** (OBSERVED absence). There is no model to copy.
- Evidence: `module-research/finance.md`

**OD-6 · Daily closing workflow**
- Questions:
  - Who opens and closes each branch?
  - Is there an opening float?
  - Must cash and **KBZPay** each be counted and matched?
  - Must KBZPay payments carry a **transaction reference**?
  - What difference is tolerated?
  - Does a difference need a reason or manager approval?
  - What happens to cash (kept as float or banked)?
  - Can sales happen before the day is opened?
- Fresha reference (OBSERVED):
  - Registers per location.
  - Opening float with denomination counter.
  - Cash in/out with reasons and attachment.
  - Expected / counted / difference per method.
  - Closing float and cash to bank.
  - **No reason or approval for differences.**
  - "Require register to be opened to start taking sales" is ON by default.
  - KBZPay has no reference field.
- Evidence: `module-research/finance.md`

**OD-7 · Barber dashboard: sales and commission visibility**
- Question: what may a barber see about their own and others' sales, commission, tips, customers (including phone numbers) and other
  branches?
- Fresha reference (OBSERVED defaults):
  - Basic role can't view own sales, open reports or view client contact details.
  - "Can view all team members' data" is on.
  - Branch scope is a single "all locations" switch.
- Evidence: `module-research/roles-permissions.md`, `evidence/roles/permission-matrix.md`

### New questions surfaced by the research

**OD-8 · Barber-level pricing within a branch**
- Question: do barbers at the same branch charge different prices or durations (e.g. senior vs junior) for the same service?
- Why it's a real decision: Fresha supports price and duration per **branch × barber**. It showed "from SGD 45" for "Any" and SGD 50 for
  one barber. Our plan specifies branch-level pricing only.
- Evidence: `module-research/services.md`

**OD-9 · "Any Barber" distribution rule**
- Question: when a customer chooses Any Barber, who gets the booking?
- Options Fresha offers (OBSERVED):
  - most availability (fill calendars);
  - take turns;
  - fewest reviews;
  - fixed priority order;
  - prefer the customer's last barber.
- Also:
  - May a multi-service booking be split between barbers?
  - May bookings be reassigned later?
- Evidence: `evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt`

**OD-10 · One-active-booking rule: edge cases**
- Question: does the rule apply to staff-created bookings as well as online ones? Does a multi-service appointment count as one? What
  about booking for family or friends (group bookings), or a walk-in while a future booking exists? Can staff override it?
- Why: Fresha has no such rule. Staff created two future bookings for one client without warning, and Fresha offers group
  appointments for others.
- Evidence: `module-research/booking.md`

**OD-11 · Customer identity and the scope of "no SMS OTP"**
- Questions:
  - Does the locked "no SMS OTP" rule cover customers too, or staff only? The brief lists it beside the staff-auth rules without saying.
  - Is a phone number mandatory and unique per customer?
  - If SMS OTP is excluded for customers, how does an online customer prove who they are?
  - What should happen when a duplicate is detected (block, warn, merge)?
- Why: the one-active-booking rule and customer history depend on it.
- Fresha reference (OBSERVED):
  - Online customers verify by phone SMS code, email, Google or Apple.
  - Staff-side duplicates are only warned about and merged later (the merge **kept the newer profile's name**).
  - Import rejects duplicates.
- Evidence: `module-research/customers.md`

**OD-12 · Overrides, reasons and approvals**
- Question: which actions need a manager's approval or a mandatory reason? For example:
  - booking a barber who is already busy or off-shift;
  - discounts;
  - refunds and voids;
  - cancellations;
  - register differences.
- Fresha reference (OBSERVED):
  - Conflicts are soft-warned and overridable.
  - Discounts and voids need no reason.
  - Refunds require a reason.
  - Cancellation reason is optional.
  - There's no approval step anywhere except pay runs.
- Evidence: `module-research/booking.md`, `module-research/payments.md`

**OD-13 · Leave requests and approval**
- Question: do barbers request leave themselves? Who approves it? Does **pending** leave block bookings? Is half-day leave allowed?
- Fresha reference (OBSERVED): leave has an "Approved" checkbox, but unapproved leave already removed availability; partial days
  are supported.
- Evidence: `module-research/leave.md`

**OD-14 · No-show and late-cancellation consequences**
- Question: are there fees, deposits, blocking after N no-shows, or required reasons?
- Fresha reference (OBSERVED):
  - Fees and deposits need card payments (Fresha Payments).
  - "Block client" lists reasons such as "Too many no-shows".
  - No-show has no reason field.
- Evidence: `module-research/booking.md`, `module-research/customers.md`

**OD-15 · Taxes and service charges**
- Question: are listed prices tax-inclusive? Does any tax or service charge apply, and does it differ by branch?
- Fresha reference (OBSERVED): tax-inclusive/exclusive setting, tax rates per business or per location, optional service charges.
- Evidence: `module-research/settings.md`

**OD-16 · Customer reminders and messages**
- Question: should customers receive booking confirmations and reminders? Through which channel, and who pays for SMS?
- Fresha reference (OBSERVED): automatic confirmations and reminders (3 days / 24 hours / 1 hour) by email, SMS or WhatsApp; SMS and WhatsApp
  use a paid balance.
- Our plan specifies staff in-app notifications only.
- Evidence: `module-research/notifications.md`

## Not raised as owner decisions (design or technical choices)

- Whether to show a combined all-branches calendar, how to validate overlapping shifts, audit-log scope and retention, import duplicate
  handling, real-time versus delayed reports. These are specification and design decisions (see `gap-analysis.md`).
