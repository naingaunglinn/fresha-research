# Walk-in: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Two walk-in paths were performed:
> (A) a walk-in **appointment** (Baber Shop, Aung, later checked out as Sale #1 and refunded), and (B) a **quick sale** without an
> appointment (Sales #3 and #5). See `test-data-log.md` rows 8, 10, 12, 24, 35, 36.

## OBSERVED

### Path A: walk-in as an appointment ("leave client empty")

1. Calendar → click the barber's slot (or Add → Appointment) → drawer shows **"Add client — Or leave empty for walk-ins"**.
2. Leave client empty → pick service → Save → calendar block titled **"Walk-In"**.
3. Optional status steps: status dropdown → **Arrived** → **Started** (each change closes the drawer; each is logged in activity).
4. Open appointment → **Checkout** → (first time only: POS intro "Free to use… Start now") → Cart → Tip → Payment → Pay now.
5. For a same-day appointment, checkout sets **Completed** automatically. For a future appointment checked out early, it stayed
   **Started** until "Complete now".

Evidence: `evidence/booking/cross-branch-conflict-before-save.png` (walk-in drawer), `evidence/booking/calendar-after-double-booking.png`
("Walk-In" block), `evidence/audit/appt-activity-02-status-changes.png`, `evidence/payments/checkout-01.png`,
`evidence/booking/same-day-checkout-appt-status.png`, `evidence/booking/walkin-after-checkout-refund.png`

Clicks: create ~4 (slot, Add appointment, service, Save); optional statuses +4; checkout ~5 (Checkout, tip, Continue to payment,
method, Pay now); split payment adds ~5.

### Path B: walk-in as a quick sale (no appointment)

1. Calendar → **Add → Sale** (or Sales → Add new) → POS screen: "Add client — Leave empty for walk-ins", cart, tabs
   **Appointments / Services / Products / Packages / Memberships / Gift cards / Quick sale** (editable quick-sale tiles).
2. Tap a service tile. **The line's team member defaults to the logged-in user** ("Haircut 45min • Naing Aung Linn"),
   not a barber.
3. To credit the barber: line **Edit** → Team member → Apply. Same for products ("ZZTest Pomade — Naing Aung Linn" by default).
4. Continue to payment → tip → payment method → Pay now → sale "Completed", client "Walk-In".

Evidence: `evidence/walk-in/quick-sale-01.png`, `evidence/walk-in/quick-sale-02-haircut.png`, `evidence/walk-in/quick-sale-03-cart.png`,
`evidence/walk-in/quick-sale-05-cash.png`, `evidence/walk-in/quick-sale-06-done.png`

Clicks for 1 service + 1 product with barber correction: ~17 (≈6 of them only to change the default team member).

### Customer handling for walk-ins

- Walk-ins need **no customer record**: sale and appointment show "Walk-In". Client sources include "Walk-In", which is the
  default client source on the new-client form. Evidence: `evidence/customers/quick-add-client-01.aria.txt`,
  `evidence/settings/clients-settings.png`
- A customer without a phone can be created (no field is mandatory on the client form); the test client had only an email.
- **Converting a walk-in into customer history after checkout:** "Edit sale details" allows changing the team member per line and
  "payment collected by", but has **no client field**. "Changes will be reflected in all reports."
  Evidence: `evidence/walk-in/edit-sale-details.png`, `evidence/walk-in/edit-sale-details.aria.txt`
- During checkout the cart header still offers "Add client" (before payment). Evidence: `evidence/payments/checkout-02-cart-or-tip.png`

### Barber selection, start, completion, payment

| Step | Fresha behaviour | Evidence |
| --- | --- | --- |
| Select barber | From the calendar column (slot click) or the per-line team member (quick sale; defaults to logged-in user) | as above |
| Select service | Service list / quick-sale tiles, with branch- and barber-specific price applied | `services.md` |
| Start service | Status "Started" (manual) | `evidence/audit/appt-activity-02-status-changes.png` |
| Complete service | Via checkout (same-day auto-complete) or "Complete now" | `booking.md` |
| Payment | Cash / KBZPay (custom) / split / other (see `payments.md`) | `evidence/payments/checkout-03-payment.png` |

## USER-PROVIDED

- Planned: a **simple walk-in flow** (brief §26). ~70 customers/day across branches (brief §2).

## INFERRED

- In Fresha, when a receptionist or owner rings up walk-ins through the quick sale, the service is credited to the
  receptionist unless someone edits each line. That affects barber sales and commission reports.

## NOT VERIFIED

- Barber-operated walk-in on the barber's own device/app (no barber login).
- Whether a walk-in sale can be linked to a client later from the client profile (no such action observed; only "Sell" from the
  client profile, which starts a new sale).

## Notes for the gap analysis

- Fresha's fastest walk-in path (slot → service → Save → Checkout) is short, but **barber attribution depends on how the sale
  was started**. The quick-sale default of "logged-in user" is a known attribution risk.
- Walk-in records can't be re-attributed to a client after payment in the observed UI.
