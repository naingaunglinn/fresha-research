# Fresha Research & Gap Analysis

Sep 27, 2026 · @Brycen Claude Max

Fresha already covers most features planned for the 3-branch barbershop. Its gaps are in rules, controls and localisation, and 16 business rules need the owner's decision. All observations come from the user's Singapore / SGD test workspace, not the live Myanmar / MMK account.

## Executive summary

1. **Most planned features already exist in Fresha (OBSERVED):**
   - multi-branch staff with per-branch shifts, including the Monday 09–13 Branch A / 14–18 Branch B split;
   - branch-specific services, with price and duration per branch and even per barber within a branch;
   - "Any Barber" with several assignment strategies;
   - branch-level stock with native transfers and partial receipt;
   - split Cash + KBZPay payments, with KBZPay as a custom method;
   - daily cash registers (opening float, counted vs expected);
   - automatic commission, created at checkout and reversed on refund;
   - pay runs, and timesheets with a 50 m location check;
   - about 60 reports with CSV / Excel / PDF export.
2. **Its weaknesses are rules, controls and localisation (OBSERVED):**
   - staff can double-book a barber across branches, with only a soft warning;
   - one customer can hold several future bookings;
   - duplicate clients are merged afterwards, and the merge kept the newer profile's name;
   - quick-sale lines are credited to the logged-in user by default;
   - voids, discounts and register differences need no reason or approval;
   - there's no client, staff or settings change history, and cancellation reasons aren't logged;
   - there's no Burmese UI, no date-format setting, and no 14-day booking window (1–12 months only);
   - wages are hourly only, and there's no expense tracking or P\&L;
   - report data was 26–28 minutes old when viewed (refresh schedule not verified);
   - there's no QR attendance.
3. **Most open questions are business rules, not features.** Sixteen owner decisions are listed: 7 known from brief §27 and 9 surfaced by the research. The biggest are commission, payroll, daily closing with KBZPay reconciliation, customer identity (including whether "no SMS OTP" covers customers), and one-active-booking edge cases.

**Scope.** The research used the user's "Baber Shop" test workspace (trial plan, Singapore / SGD) on 27 Sep 2026. Testing added a second location, two test barbers, clients, products, sales, a register, a commission plan and pay-run data. The live Myanmar / MMK account wasn't accessed, so MMK formatting, +95 phone validation, Myanmar addresses and cash denominations are NOT VERIFIED.

## Major Fresha strengths

Fresha's strongest areas are branch-aware pricing and availability, payments, inventory, and pay integration. All nine rows were OBSERVED in the test workspace.

| Area | What Fresha does well | Details |
| --- | --- | --- |
| Pricing | Price and duration cascade from service to location to barber-at-location; "Any" shows a "from" price; price changes can optionally update existing bookings | `module-research/services.md` |
| Cross-branch availability | A barber's booking at Branch B blocks their time at Branch A; multi-service bookings chain across barbers (first slot moved from 10:00 to 10:15) | `module-research/booking.md` |
| Scheduling | Repeating shifts per location (1–4-week patterns, several segments a day), partial-day leave, closed periods per location, waitlist, slot-gap optimisation | `module-research/schedule.md` |
| Payments | Split and part-paid sales; "cash received by" and "payment taken by" per payment; refunds by original method with a mandatory reason; clear dialogs for irreversible actions (void lists the stock it returns) | `module-research/payments.md` |
| Inventory | Stock and reorder levels per location; stocktakes with review and difference cost; transfers with partial receipt; stock history with the reason and on-hand quantity after each entry | `module-research/inventory.md` |
| Commission and pay runs | Integrated with sales: refund reversal, discount deduction, per-location rows, adjustments, review and approval, step-up verification | `module-research/commission.md`, `module-research/payroll.md` |
| Daily closing | Registers with expected vs counted per payment method (KBZPay included), float carry-over, cash to bank, petty cash with attachment | `module-research/finance.md` |
| Permissions | 121 granular toggles, including branch scope and client phone visibility | `module-research/roles-permissions.md` |
| Responsive web | Usable at phone and tablet widths, with a bottom navigation on mobile | `ux-analysis.md` |

## Major Fresha pain points

Nine problems surfaced while running the workflows, led by barber attribution and cross-branch double booking. All were OBSERVED in this session; the user supplied no first-hand pain points, so none is USER-PROVIDED.

1. **Barber attribution errors are easy.** Quick-sale service and product lines default to the logged-in user, and fixing each line takes about 3 clicks. A walk-in sale can't be attached to a customer after payment.
2. **Cross-branch double booking isn't prevented.** Staff see only an inline "Team member is not available". Default shifts for a two-branch barber overlap at both branches.
3. **Key actions are hidden** under "Options": reschedule, cancel, no-show, void and refund. Reschedule can't move a booking to another branch.
4. **One branch per calendar view**, so managers switch location repeatedly.
5. **Localisation gaps:** no Burmese, no date-format setting, and inconsistent 12/24-hour display. The receipt printed "$" for SGD.
6. **Weak controls:** discounts, voids and cash differences need no reason or approval. Cancellation reasons are optional and not logged. Voids erase commission lines without trace.
7. **Reporting:** data was 26–28 minutes old when viewed; the refresh schedule wasn't verified. Day and month grouping and custom reports need the paid Insights add-on. There are no expense or P&L reports.
8. **Long checkout:** the tip step always appears, and a split Cash + KBZPay payment takes about 12 clicks.
9. **Paid essentials:** deposits and no-show fees need Fresha Payments (card), and SMS and WhatsApp reminders need a paid balance.

Click and screen counts for each repeated workflow are in `ux-analysis.md`.

## Important differences: locked decisions vs Fresha

Of the 25 rows, 16 are KEEP, 5 IMPROVE and 4 NEED OWNER DECISION; none proposes changing a locked rule. Rows follow brief §26, plus a stock-transfer timing row the brief doesn't lock. Verification labels and evidence paths are explained under Evidence and labels.

| Planned (brief §26) | Fresha observed | Difference | Recommendation | Reason | Verification |
| --- | --- | --- | --- | --- | --- |
| Staff authentication: passwordless, Google SSO or Email OTP | Passwordless email verification code, plus "Continue with mobile", Google and Apple; a password also exists (Login & security); trusted devices skip 2FA; active-session list with sign-out-all | Fresha adds phone and password options | KEEP | Fresha shows email-code and Google login work for this kind of business; our narrower set is a deliberate, locked choice | OBSERVED (`evidence/_setup/00-login-page.png`, `evidence/settings/personal-login.png`) |
| No SMS OTP (listed beside the staff-auth rules; whether it covers customers isn't stated) | Partners can also use "Continue with mobile". Customers must verify to book online: phone + SMS code (offered first), or email / Google / Apple | Fresha's customer login puts the SMS code first | KEEP | Fresha's partner login works with an email code or Google, without SMS, so the rule is workable for staff. Customer scope is open (B-6, OD-11) | OBSERVED (public venue: `evidence/booking/public-09-after-time-continue.png`) |
| Multi-branch staff | "Works at" several locations; repeating shifts per location; the Mon 09–13 A / 14–18 B split is honoured; overlapping shifts at two branches saved without warning; other-branch bookings shown as blocks | Fresha doesn't validate cross-branch shift overlap | IMPROVE | Specify overlap validation for shifts; Fresha's defaults create overlaps automatically | OBSERVED (`evidence/schedule/scheduled-shifts-baber-shop.png`) |
| Branch-specific service eligibility | Service → locations and team members; member → services; pickers limited to the location's members; ineligible members flagged "doesn't provide this service" | Equivalent | KEEP | Fresha confirms the model is workable | OBSERVED |
| Branch-specific price / duration | Location override and team-member-at-location override, cascading; "Any" shows a "from" price; a price change can optionally update existing bookings (off by default) | Fresha also supports barber-level price and duration per branch | NEED OWNER DECISION | Do barbers at one branch charge different prices (e.g. senior vs junior)? If not, branch-level pricing is enough (OD-8) | OBSERVED (`evidence/services/advanced-pricing-all-locations.aria.txt`) |
| Flexible booking selection | Staff: time/barber first (slot), service first ("View available times"), client first (drawer), branch via picker. Customer: services → professional → time → login | Equivalent in intent | KEEP | All four entry orders are proven in practice | OBSERVED (staff); OBSERVED on a third-party public venue (customer) |
| Any Barber | "Any team member / Any professional"; strategies: fill calendars (day / 7 / 14 days), take turns, fewest reviews, priority order; prioritise last booked; exclude members; auto-reassign; split multi-service across members (on) | Our assignment rule isn't specified | NEED OWNER DECISION | How are Any Barber bookings distributed: fairness, filling gaps, or the customer's last barber? (OD-9) | OBSERVED (`evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt`) |
| 14-day default advance booking window | Online window options 1–12 months only; lead time "immediately … 14 days before" | Fresha can't express a 14-day window | KEEP | A Fresha limitation, not a reason to change the locked rule | OBSERVED (`evidence/settings/scheduling-availability-edit-0.aria.txt`) |
| One active booking per customer | No such rule: staff created two future bookings for one client with no warning; online side not tested | Fresha doesn't enforce it | NEED OWNER DECISION | Edge cases: staff override, family or group bookings, multi-service appointments, walk-ins while a future booking exists (OD-10) | OBSERVED (staff); NOT VERIFIED (online) |
| Simple walk-in flow | Walk-in = appointment with no client, or a quick sale; quick-sale lines default to the logged-in user; a walk-in sale can't be linked to a client afterwards (no client field in Edit sale) | Fresha's quick path risks wrong barber attribution | IMPROVE | Specify explicit barber attribution in the walk-in flow, and whether a customer can be attached later | OBSERVED (`evidence/walk-in/quick-sale-02-haircut.png`, `evidence/walk-in/edit-sale-details.png`) |
| Cash + KBZPay | Cash built in; KBZPay = custom method with a name only, no transaction reference; one-tap full amount; split and part-paid supported; refunds by original method or cash; register close counts KBZPay manually | No KBZPay reference or reconciliation data | NEED OWNER DECISION | Must staff record a KBZPay reference, and how is KBZPay reconciled daily? (OD-6) | OBSERVED (`evidence/payments/add-custom-payment-method.png`, `evidence/finance/register-close-01.png`) |
| Branch-level stock | Stock per location; per-location low-stock level and reorder quantity; stock history per location; product list shows the total | Equivalent | KEEP | Fresha runs the same model (stock, reorder levels and history per location), and it worked in testing | OBSERVED |
| Stock transfers | Native transfer orders (source → destination); partial receipt; stock moves only on receipt (no in-transit); PDF / CSV | Equivalent capability | KEEP | Fresha confirms branch-to-branch transfers with receipt are workable | OBSERVED (`evidence/inventory/product-stock-history-after-transfer.png`) |
| Stock transfer timing (NOT SPECIFIED IN BRIEF) | Stock leaves the source only when the destination receives it (no in-transit state); partial receipt possible | Our spec doesn't say when stock leaves the source | IMPROVE | Define dispatch vs receipt timing and partial-receipt handling in the spec | OBSERVED (`evidence/inventory/product-stock-history-after-transfer.png`) |
| QR + location attendance | Distance check ("more than 50m away"); auto clock-in/out from shifts; manager-entered timesheets with before/after audit; no QR and no device check found; attendance summary report (late / early / missed) | FRESHA GAP: QR | KEEP | Fresha lacks the QR part; its lateness and missed-shift metrics are a useful reference | OBSERVED (web); NOT VERIFIED (mobile app) |
| Myanmar + English UI | 39 languages, no Burmese | FRESHA GAP | KEEP | Locked; Fresha has no Burmese, so there's no alternative to weigh | OBSERVED (`evidence/settings/language-picker.png`) |
| MMK | Currency fixed at workspace creation; the test workspace uses SGD; receipt PDF printed "$"; the live account uses MMK | MMK formatting unknown | KEEP | Locked, and the live Fresha account already uses MMK. How Fresha formats MMK is NOT VERIFIED | USER-PROVIDED (live account); NOT VERIFIED (formatting) |
| 12-hour time | 12 h / 24 h setting; search results showed 12 h while 24 h was set | Equivalent option; Fresha inconsistent | KEEP | Fresha offers the same 12-hour option; its inconsistent display is a pitfall to avoid, not an argument against the rule | OBSERVED |
| DD/MMM/YYYY dates | No date-format setting; several formats appear in the UI | Fresha can't enforce a format | KEEP | Locked; Fresha has no date-format setting, so there's no alternative to weigh | OBSERVED (`evidence/settings/date-time-settings-edit.aria.txt`) |
| In-app staff notifications | Bell (Appointments / Reviews / Tips / Online sales); per-user preferences by event and channel (email / push / in-app), location filter, "only my appointments"; own actions apparently not notified | Fresha has richer per-user filtering | IMPROVE | Consider the location filter and "only my appointments" filter when specifying notifications | OBSERVED; INFERRED (own actions) |
| 90-day notification history | Bell retention not shown; appointment activity kept "last 12 months", sale activity "last 90 days" | Not comparable | KEEP | Fresha's bell retention is NOT VERIFIED, so there's no evidence against 90 days | NOT VERIFIED (Fresha bell retention) |
| Weekly backup | No backup or restore UI; only exports and a paid Data Connector add-on | Fresha exposes no backup | KEEP | Fresha exposes no backup, so nothing contradicts the rule | OBSERVED absence |
| 1-year backup retention | As above | No Fresha equivalent | KEEP | Fresha shows no backup or retention setting, so nothing contradicts the rule | OBSERVED absence |
| Excel / CSV import | CSV only; clients and products only; column mapping; preview with per-row errors; duplicates rejected (in-file: both rows; existing: not updated); invalid rows downloadable | No Excel import and no staff or service import | IMPROVE | Our spec should state the duplicate policy for imports: reject, update or merge | OBSERVED (`evidence/import-export/client-import-04-errors.png`) |
| Excel / CSV / PDF export | Reports: CSV / Excel / PDF; lists: CSV / Excel (sales list and service menu also PDF) | Equivalent | KEEP | Fresha offers the same three formats | OBSERVED |

## Other areas: not locked by the brief

Of these 24 areas, 15 need an owner decision; the others are 3 IMPROVE, 2 ADD, 2 REMOVE (from scope) and 2 NEED MORE RESEARCH. Where the plan column cites §27, the area is already a known open decision.

| Area | Fresha observed | Our plan (brief) | Recommendation | Reason | Verification |
| --- | --- | --- | --- | --- | --- |
| B-1 Commission calculation | % or fixed; per item type (services, add-ons, products, packages, memberships, gift cards, no-show/late fees); per location; per weekday; tiered; deduct discounts / taxes / costs; "only on fully paid invoices"; created at checkout, deleted on refund, removed silently on void; cart discount pro-rated before commission | Not specified (open owner decision, §27) | NEED OWNER DECISION | Known open decision; Fresha shows the range of rules to choose from (OD-1) | OBSERVED |
| B-2 Commission and revenue timing | Sale date = checkout date; early checkout counted in the checkout week; same-day checkout auto-completes the appointment | Not specified | NEED OWNER DECISION | Part of "completed vs paid" in brief §13 (OD-1) | OBSERVED |
| B-3 Tips | Tip goes to the service provider (editable); % on the whole cart including products; tips flow into pay runs; register cash-out "Pay team member tips" | Not specified | NEED OWNER DECISION | Tip ownership and payout are payroll rules (OD-4) | OBSERVED |
| B-4 Salary and payroll | Hourly wages only; pay periods daily to quarterly; per-location pay rows; adjustments (+/−); cash-advance option; review (Needs review / Approved / Skip); completion needs an emailed code | Not specified (payroll rules open, §27) | NEED OWNER DECISION | The brief leaves payroll rules open (§14 / §27), and Fresha's hourly-only wages don't settle salary type, advances or tips (OD-4) | OBSERVED; paid state NOT VERIFIED |
| B-5 Daily closing | Registers per location: opening float with denomination counter; cash in/out (reasons, attachment); expected vs counted per payment method (incl. KBZPay); closing float; cash to bank; no difference reason or approval; "require open register to take sales" on by default | Not specified (daily closing open, §27) | NEED OWNER DECISION | Tolerance, approval and KBZPay reconciliation are the owner's call (OD-6) | OBSERVED |
| B-6 Customer identity and duplicates | No mandatory client field; duplicate email: soft warning, then irreversible merge (kept the newer profile's name); import rejects duplicates; online customers must log in (phone SMS / email / Google / Apple) | Not specified | NEED OWNER DECISION | Is phone mandatory and unique? Does "no SMS OTP" also cover customers, and if so, how do online customers prove identity? The one-booking rule depends on it (OD-11) | OBSERVED; phone matching NOT VERIFIED |
| B-7 Double booking and overrides | Staff can save a cross-branch double booking (soft warning "Team member is not available") and reschedule outside shifts (confirm dialog) | Not specified | NEED OWNER DECISION | May any role override conflicts, and must an override have a reason? (OD-12) | OBSERVED (`evidence/booking/cross-branch-conflict-before-save.png`) |
| B-8 Leave approval | Time off with types and time ranges (half-day); "Approved" checkbox; unapproved leave still blocks bookings; no request workflow seen | Not specified | NEED OWNER DECISION | Who requests and approves leave, and does pending leave block bookings? (OD-13) | OBSERVED; barber requests NOT VERIFIED |
| B-9 No-show and cancellation policy | Cancellation reason optional; no-show without reason; fees and deposits need Fresha Payments (card); "Block client" with reasons (e.g. too many no-shows) | Not specified | NEED OWNER DECISION | Consequences for no-shows and late cancellations: fees, blocking, required reasons (OD-14) | OBSERVED |
| B-10 Preferred barber | No preferred-barber field; "Prioritise last booked team member" option | Threshold is an open owner decision (§27) | NEED OWNER DECISION | A known open decision, and Fresha has no preferred-barber concept to borrow (OD-3) | OBSERVED absence |
| B-11a What barbers may see | Basic role: no reports, no client contact details, can't view own sales; "Can view all team members' data" on; pay runs owner-only | Not specified (barber dashboard is an open owner decision, §27) | NEED OWNER DECISION | A known open decision; Fresha's role toggles show the choices involved: own sales, others' data, client contacts, branch scope (OD-7) | OBSERVED |
| B-11b Role scope per branch | One role per member, workspace-wide, plus a "Can view and access all locations" switch; 121 granular permissions | Not specified | IMPROVE | Fresha can't give different roles per branch; specify whether roles or permissions differ by branch (e.g. manager at one, barber at another) | OBSERVED |
| B-12 Audit trail | Record-scoped logs (appointments 12 months, sales 90 days, stock, timesheets with before/after, pay-run events); no client, staff or settings change history; cancellation reason not logged; void leaves no commission trace | Not specified | ADD | Define a consistent audit requirement (who, when, before/after, reason); Fresha's gaps show what to avoid | OBSERVED |
| B-13 Staff deactivation | Archive (restorable); future bookings stay assigned with "not available" | Not specified | IMPROVE | Specify handling of future bookings, shifts and pay on deactivation | OBSERVED |
| B-14 Reports | About 60 reports; data 26–28 min old when viewed (refresh schedule not verified); day/month grouping and custom reports are paid (Insights); branch via filter or grouping; no expense or P&L | Not specified (§18 lists required reports) | IMPROVE | Specify which reports must be real-time (e.g. daily closing) and which groupings are required: branch, barber, day, month | OBSERVED |
| B-15 Expenses and P&L | None (only register cash-outs with an attachment) | Company-wide expense allocation is an open owner decision (§27) | NEED OWNER DECISION | A known open decision, and Fresha has nothing to copy (OD-5) | OBSERVED absence |
| B-16 Taxes and service charges | Tax rates per business or location; tax-inclusive or exclusive pricing; service charges; none configured | Not specified | NEED OWNER DECISION | Are prices tax-inclusive, and does any tax or service charge apply? (OD-15) | OBSERVED (settings only) |
| B-17 Discounts | Cart and line discounts (SGD or %), no reason or approval; "apply discounts" permission from the Medium role; commission computed after discount | Not specified | NEED OWNER DECISION | Who may discount, and does commission use the discounted price? (OD-1, OD-12) | OBSERVED |
| B-18 Customer notifications | Automated reminders (3 d / 24 h / 1 h), confirmations, reschedule / cancel / no-show messages by email, SMS or WhatsApp; SMS and WhatsApp use a paid balance; per-client consents | Not specified (only staff in-app notifications are) | NEED OWNER DECISION | Do customers receive reminders, and through which channel, at what cost? (OD-16) | OBSERVED |
| B-19 Booking links, QR, widgets | Link builder: links and QR per service / location / team member; requires publishing the marketplace profile | Not specified | NEED MORE RESEARCH | Not tested (the test profile wasn't published); confirm how the live account uses links or QR | OBSERVED (menu); NOT VERIFIED (function) |
| B-20 Gift cards, packages, memberships, loyalty, waitlist | Present in Fresha (catalogue, sales, reports, automations) | Not specified | NEED MORE RESEARCH | Check whether the live account actually uses them before scoping | OBSERVED (existence only) |
| B-21 Marketplace, AI Concierge, Smart Website, Reserve with Google, reviews | Fresha-ecosystem channels and paid add-ons | Not specified | REMOVE | Remove from scope: tied to Fresha's own marketplace, and the brief describes an internal system | OBSERVED |
| B-22 Patch tests, consultation forms, resources (rooms) | Salon and spa features: patch test, forms, bookable resources | Not specified | REMOVE | Remove from scope unless the owner says otherwise: not barbershop-relevant in the brief | OBSERVED |
| B-23 Security step-up | Completing a pay run requires an emailed 4-digit code | Not specified | ADD | For consideration: step-up verification for payroll finalisation and other high-risk finance actions | OBSERVED |

## Assumptions under pressure

Six locked decisions rest on an assumption the research puts under pressure, and one date rule isn't stated in the plan yet. None of this changes a locked rule.

| Decision | Implicit assumption | What the research showed | Evidence |
| --- | --- | --- | --- |
| One active booking per customer | A customer can be reliably identified | Fresha identifies online customers through a verified account (phone SMS code, email, Google or Apple); staff-side client records have no mandatory unique field. If "no SMS OTP" also covers customers, the identity rule needs an explicit answer (B-6, OD-11) | `evidence/booking/public-09-after-time-continue.png` |
| Simple walk-in flow | The barber is known automatically | The barber depends on how the sale is started; quick-sale lines default to the logged-in user | `evidence/walk-in/quick-sale-02-haircut.png` |
| Cash + KBZPay | Recording the method is enough | KBZPay carries no reference; reconciliation is a manual count at register close | `evidence/finance/register-close-01.png` |
| Stock transfers | A transfer is a single movement | Two steps (ordered, then received) with partial receipt; stock leaves the source only at receipt | `evidence/inventory/stock-transfer-T1-receive.png` |
| Multi-branch staff | Schedules won't collide | Fresha auto-created identical shifts at both branches for a two-branch barber, and allowed a cross-branch double booking | `evidence/schedule/scheduled-shifts-baber-shop.png`, `evidence/booking/cross-branch-conflict-before-save.png` |
| In-app staff notifications | Staff learn about changes made by others | Fresha appears not to notify the person who acted (INFERRED); it offers per-location and "only my appointments" filters that multi-branch staff may need | `module-research/notifications.md` |
| Revenue and commission dates (not in §26) | Not stated: service date or payment date? | Fresha uses the checkout date, which moved an early-paid appointment into an earlier pay period | `evidence/payments/checkout-07-complete.png` |

## Missing features

Thirteen capabilities weren't found in Fresha, and seven areas couldn't be verified. "OBSERVED absence" means the screens visited didn't contain the feature; Fresha may still offer it in another plan or app.

**Not provided by Fresha (OBSERVED absence):**

- expense tracking and P\&L;
- company-wide expense allocation;
- QR attendance and device checks;
- Burmese language;
- a date-format setting;
- a 14-day booking window;
- per-branch roles;
- client, staff and settings change history;
- a loan or advance register (only a per-sale cash-advance option in pay runs);
- a monthly salary type;
- a combined multi-branch calendar;
- a KBZPay reference and reconciliation;
- a preferred-barber field.

**Could not be verified (NOT VERIFIED):**

- the live account's configuration and MMK formatting;
- the barber's own view and mobile app, and notifications to other staff;
- the paid state and period locking of pay runs (blocked by an emailed verification code);
- customer self-booking against our own configuration (the test marketplace profile wasn't published);
- a low-stock alert firing;
- the reschedule audit entry;
- Premium reports.

## Potential risks

Eight risks follow from the findings. The first four are operational and depend on rules the spec hasn't set yet.

1. **Attribution and commission disputes** if walk-ins, quick sales or early checkouts default to the operator or shift pay periods. Fresha evidence: the logged-in-user default and checkout-date revenue.
2. **Double booking of multi-branch barbers** if overlapping shifts and conflict overrides aren't validated. Fresha auto-creates overlapping shifts.
3. **Customer identity:** if "no SMS OTP" also covers customers, the one-active-booking rule and duplicate prevention need another reliable key (OD-11).
4. **Cash and KBZPay reconciliation gaps** if KBZPay isn't referenced and differences need no reason or approval.
5. **Data migration from Fresha:** the client export has no visit count, total spend or last visit. Importing history will need other sources (sales and appointment exports), and duplicates must be resolved before import.
6. **Scope creep:** Fresha has many salon, spa and marketplace features (packages, memberships, gift cards, loyalty, forms, patch tests, resources, AI concierge). The brief doesn't justify copying them.
7. **Reporting expectations:** owners used to Fresha may expect its report catalogue. Fresha's own report data was 26–28 minutes old when viewed, and time grouping is paid, so "the same as Fresha" is itself limited.
8. **Research limits:** observations come from a Singapore test workspace with 2 locations and 3 bookable staff, not the live 3-branch, 15-barber account.

## OWNER DECISIONS STILL NEEDED

Sixteen business rules need the owner's answer before the specification: 7 known from brief §27 and 9 surfaced by the research. Nothing here is decided, and Fresha's behaviour is a reference, not a recommendation.

### Known open areas (brief §27)

| # | Decision | Questions for the owner | Fresha reference (OBSERVED) | Evidence |
| --- | --- | --- | --- | --- |
| OD-1 | Commission calculation | Percentage or fixed amount? Different by service, product, barber or branch? Computed before or after discounts and taxes? Earned when the service is completed or when it's paid? What happens on refund and void? Service date or payment date? | % or fixed, per item type, per location, per weekday, tiered; toggles to deduct discounts, taxes or cost, and "only on fully paid invoices"; created at checkout, deleted on refund, removed without trace on void; cart discounts pro-rated before commission; checkout date drives the pay period | `module-research/commission.md`, `evidence/payroll/pay-run-activity-after-discount.png` |
| OD-2 | KPI rules | Which KPIs are tracked per barber and per branch, and how is each defined? Examples: services count, revenue (gross or net of discounts and refunds), product sales, punctuality or attendance, no-show rate, repeat customers | Reports on sales, commission, tips, attendance (on-time, late, missed shifts, punctuality %) and cancellations or no-shows; "Top team member" and "Top services" dashboard widgets; time-series grouping is a paid add-on | `module-research/reports.md` |
| OD-3 | Preferred barber threshold | When does a barber count as a customer's preferred barber (e.g. N of the last M visits), and what does the system do with it? | No preferred-barber field; the only related option is "Prioritize last booked team member" for "Any" bookings | `module-research/customers.md`, `evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt` |
| OD-4 | Payroll rules | Monthly salary, hourly, commission-only, or a mix? Pay period? Advances and loans: tracked and repaid how? Deductions for absence, lateness or leave? Who owns tips, and how are they paid out? Can barbers keep cash from sales as an advance? How is a multi-branch barber's pay split across branches? | Hourly only, no salary type; periods daily to quarterly; manual +/− adjustments; "record cash payments for sales as paid (advance)"; tips go to the service provider and flow into pay runs, and register cash-out has "Pay team member tips"; pay rows per member per location; review Approved / Skip, and an emailed verification code to complete | `module-research/payroll.md` |
| OD-5 | Company-wide expense allocation | Which expenses are company-wide versus branch-level? How are company-wide costs allocated to branches: equal split, by revenue, by headcount, other? | No expense module and no P&L (OBSERVED absence), so there's no model to copy | `module-research/finance.md` |
| OD-6 | Daily closing workflow | Who opens and closes each branch? Is there an opening float? Must cash and KBZPay each be counted and matched? Must KBZPay payments carry a transaction reference? What difference is tolerated, and does it need a reason or manager approval? Is cash kept as float or banked? Can sales happen before the day is opened? | Registers per location; opening float with denomination counter; cash in/out with reasons and attachment; expected / counted / difference per method; closing float and cash to bank; no reason or approval for differences; "Require register to be opened to start taking sales" on by default; KBZPay has no reference field | `module-research/finance.md` |
| OD-7 | Barber dashboard: sales and commission visibility | What may a barber see about their own and others' sales, commission, tips, customers (including phone numbers) and other branches? | Defaults: the Basic role can't view own sales, open reports or view client contact details; "Can view all team members' data" is on; branch scope is a single "all locations" switch | `module-research/roles-permissions.md`, `evidence/roles/permission-matrix.md` |

### Surfaced by the research

| # | Decision | Questions for the owner | Fresha reference (OBSERVED) | Evidence |
| --- | --- | --- | --- | --- |
| OD-8 | Barber-level pricing within a branch | Do barbers at the same branch charge different prices or durations for the same service (e.g. senior vs junior)? | Price and duration per branch × barber; showed "from SGD 45" for "Any" and SGD 50 for one barber. Our plan specifies branch-level pricing only | `module-research/services.md` |
| OD-9 | "Any Barber" distribution | When a customer chooses Any Barber, who gets the booking? May a multi-service booking be split between barbers? May bookings be reassigned later? | Options: most availability (fill calendars), take turns, fewest reviews, fixed priority order, prefer the customer's last barber | `evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt` |
| OD-10 | One-active-booking edge cases | Does the rule apply to staff-created bookings as well as online ones? Does a multi-service appointment count as one? What about bookings for family or friends, or a walk-in while a future booking exists? Can staff override it? | No such rule: staff created two future bookings for one client without warning; group appointments for others are offered | `module-research/booking.md` |
| OD-11 | Customer identity and the scope of "no SMS OTP" | Does the locked "no SMS OTP" rule cover customers too, or staff only? The brief lists it beside the staff-auth rules without saying. Is a phone number mandatory and unique per customer? If SMS OTP is excluded for customers, how does an online customer prove who they are? What happens when a duplicate is detected: block, warn or merge? | Online customers verify by phone SMS code, email, Google or Apple; staff-side duplicates are only warned about and merged later (the merge kept the newer profile's name); import rejects duplicates | `module-research/customers.md` |
| OD-12 | Overrides, reasons and approvals | Which actions need a manager's approval or a mandatory reason: booking a barber who is busy or off-shift, discounts, refunds and voids, cancellations, register differences? | Conflicts are soft-warned and overridable; discounts and voids need no reason; refunds require one; cancellation reason is optional; no approval step anywhere except pay runs | `module-research/booking.md`, `module-research/payments.md` |
| OD-13 | Leave requests and approval | Do barbers request leave themselves? Who approves it? Does pending leave block bookings? Is half-day leave allowed? | Leave has an "Approved" checkbox, but unapproved leave already removed availability; partial days are supported | `module-research/leave.md` |
| OD-14 | No-show and late-cancellation consequences | Are there fees, deposits, blocking after N no-shows, or required reasons? | Fees and deposits need card payments (Fresha Payments); "Block client" lists reasons such as "Too many no-shows"; no-show has no reason field | `module-research/booking.md`, `module-research/customers.md` |
| OD-15 | Taxes and service charges | Are listed prices tax-inclusive? Does any tax or service charge apply, and does it differ by branch? | Tax-inclusive or exclusive setting; tax rates per business or per location; optional service charges | `module-research/settings.md` |
| OD-16 | Customer reminders and messages | Should customers receive booking confirmations and reminders? Through which channel, and who pays for SMS? | Automatic confirmations and reminders (3 days / 24 hours / 1 hour) by email, SMS or WhatsApp; SMS and WhatsApp use a paid balance. Our plan specifies staff in-app notifications only | `module-research/notifications.md` |

Not raised as owner decisions, because they're spec and design choices covered in the gap tables: a combined all-branches calendar, shift-overlap validation, audit scope and retention, import duplicate handling, and real-time versus delayed reports.

## Recommended next research

Five checks remain where something is genuinely unclear. Items 2, 4 and 5 need the test workspace, whose free trial ends around Oct 4, 2026. That date comes from the 27 Sep 2026 banner "free trial ends in 7 days"; extending the trial or activating the plan would lift it.

1. **Live account check with the owner** (30–60 min, read-only): MMK formatting on screen and receipts; how many locations, staff and roles are configured; whether packages, memberships, gift cards, waitlist, booking links or QR are used; current commission and pay-run settings (the current rules behind OD-1 and OD-4).
2. **Barber view:** invite one barber-level test login (Basic role) to confirm what barbers see and which notifications they receive.
3. **Fresha mobile app (barber side):** clock-in with the 50 m check, leave requests, notification delivery.
4. **Pay-run completion:** the owner enters the emailed code once on a test run, to observe the paid and locked state.
5. **Customer self-booking** against our own configuration, only if the owner accepts briefly publishing the test profile.

## Evidence and labels

Every finding cites evidence in the local `fresha-research/` folder; paths in this doc (`evidence/…`, `module-research/…`, `ux-analysis.md`) are relative to it.

- **OBSERVED:** seen in the Fresha UI during this session, with evidence.
- **USER-PROVIDED:** stated by the user, in the brief or in answers during the session.
- **INFERRED:** reasoning from observations, marked as such and never presented as fact.
- **NOT VERIFIED:** couldn't be checked; the module write-ups give the reason.
- **OBSERVED absence:** not found in the screens, menus and catalogues visited; Fresha may still offer it in another plan or app.
- **FRESHA GAP:** a planned capability Fresha doesn't appear to offer, based on observed absence.

The folder holds 541 evidence files (screenshots, accessibility-tree text captures, downloaded CSV and PDF files), 20 per-module write-ups, a UX and speed analysis, a 321-item coverage checklist for brief §4–§24, and a log of everything created or changed in Fresha during testing. Its screenshots and receipt PDF show the test workspace owner's contact details and address, so review them before sharing the folder. The research was done by Claude (AI agent) in a browser the user logged into; no password, code or session token was handled.
