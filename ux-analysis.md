# UX / Speed Analysis: Fresha partner web app

> **Method.** Click and screen counts were recorded while performing each workflow in the sandbox on 2026-09-27 (desktop Chrome,
> ~1908×960). A "click" is a deliberate pointer action (menu open, option pick, button). Typing, scrolling and waiting are excluded.
> Counts are **approximate** (±1–2) and reflect the shortest path I found, not an exhaustive search. Mobile and tablet observations come
> from the **responsive web app** at 390 px and 820 px widths. The **Fresha native apps weren't tested** (NOT VERIFIED).
> **No first-hand user pain points were supplied** during the session, so everything below is OBSERVED or INFERRED.

## Repeated daily workflows

| Workflow | Shortest observed path | Clicks | Screens / panels | Friction observed | Evidence |
| --- | --- | --- | --- | --- | --- |
| **Start a booking (staff, known slot)** | Calendar → click barber's slot → Add appointment → Add client → search → pick → pick service → Save | ~6 + typing | Calendar, slot menu, drawer (client panel, service list, summary) | Needs the right branch selected first (one location per calendar view) | `evidence/booking/slot-new-appt-01.png` |
| **Start a booking (service-first / "Any barber")** | Add → Appointment → View available times → (client) → service → Continue → date → time → Continue → Save | ~10–13 | Banner mode, drawer (Services → Time → Summary) | "View available times" is hidden behind the "Select a time to book" banner. Price shows "from" until a barber is assigned | `evidence/booking/new-appt-01.png`, `evidence/booking/new-appt-time-step.png` |
| **Start a walk-in (appointment)** | Slot → Add appointment → service → Save (client left empty) | ~4 | Drawer | Fast. Barber comes from the column | `evidence/booking/calendar-after-double-booking.png` |
| **Start a walk-in (quick sale)** | Add → Sale → service tile → **Edit → team member → Apply** → Continue to payment → tip → method → Pay now | ~10 per service (+3 per product line to fix the barber) | POS grid, cart, edit modal, tip, payment | **Lines default to the logged-in user**; crediting the barber needs 3 extra clicks per line | `evidence/walk-in/quick-sale-02-haircut.png`, `evidence/walk-in/quick-sale-03-cart.png` |
| **Complete a service** | Open appointment → status → Arrived / Started (optional), then Checkout (same-day auto-completes) or "Complete now" (early checkout) | 2 per status + checkout | Drawer | Each status change **closes the drawer**. Early checkout leaves "Started" | `evidence/audit/appt-activity-02-status-changes.png` |
| **Checkout (one method)** | Checkout → tip choice → Continue to payment → method → Pay now | ~5 (first time +1 POS intro) | Cart → Tip → Payment → Sale | Tip step appears every time. Custom method (KBZPay) = one tap full amount | `evidence/payments/checkout-03-payment.png` |
| **Checkout (Cash + KBZPay split)** | … → Split payment → Add payment method → Cash → (cash received by) → amount → Add → Add payment method → KBZPay → Add payment → Pay now | ~10–12 | Payment, split list, 2 modals | Keypad entry for cash. There's no KBZPay reference field | `evidence/payments/checkout-split-06-both.png` |
| **Reschedule** | Open appointment → Options → Reschedule → click new slot → Update | ~5 | Drawer, calendar in pick mode, confirm modal | Action hidden under **Options**. **Can't change branch** in this mode. Drag-and-drop not tested | `evidence/booking/reschedule-01.png` |
| **Cancel** | Open appointment → Options → Cancel → (reason dropdown → reason) → Cancel appointment | 4–6 | Drawer, modal | Reason is optional (default "No reason provided") | `evidence/booking/cancel-modal.png` |
| **No-show** | Open → Options → No-show → Set as no-show | 4 | Drawer, modal | No reason field | `evidence/booking/noshow-modal.png` |
| **Find customer** | Top-bar Search → type → pick result | 2 + typing | Search overlay | Fast. Finds by name or appointment reference; not by service | `evidence/customers/global-search-03.png` |
| **Record a service usage of stock** | Product → Actions → Remove stock → location → qty → reason (Internal use) → Save | ~7 | Drawer, 2 modals | Manual; not linked to the service performed | `evidence/inventory/remove-stock-02.png` |
| **Receive stock (transfer)** | Stock orders → order → Actions → Receive stock → quantities (auto-fill) → Receive order → (partial choice → Confirm) → Done | 5–8 | Drawer, full-screen receive, modal | Clear partial-receipt handling | `evidence/inventory/stock-transfer-T1-receive.png` |
| **Transfer stock** | Stock orders → Add → Add new transfer → source → Add products → pick → Add product → qty → Create order → Done (+ receive at destination) | ~9 + receive | Full-screen wizard | Quantity defaults to the product's reorder qty (10), which is easy to over-transfer | `evidence/inventory/stock-transfer-05.png` |
| **Daily closing (register)** | Register → View → Close register → type counted Cash / KBZPay / Other → closing float → cash to bank → Close register | ~6 + typing | Drawer, close form | No difference reason or approval | `evidence/finance/register-close-filled.png` |
| **Add location** | Locations → Add → 4 steps → Save | ~8 + typing | 4 wizard steps | Phone and email mandatory; address search limited to country | `evidence/branches/add-location-02.png` |
| **Add barber** | Team → Add → profile → Services → Locations → Settings (role) → Add | ~8 + typing | One long form with side nav | Email mandatory | `evidence/staff/add-team-member-01.png` |

## Cross-cutting observations

**OBSERVED**
- **Hidden actions:** Reschedule, No-show and Cancel sit under the appointment's **Options** menu. Void and refund sit under the sale's **Open options**.
- **Soft warnings instead of blocks:** cross-branch double booking ("Team member is not available") and out-of-shift reschedules can be saved.
  That's quick for staff but error-prone.
- **Default attribution risk:** quick-sale lines default to the logged-in user. The tip screen briefly showed the logged-in user before
  switching to the service provider.
- **One branch per calendar view:** multi-branch managers switch location to see each branch. Cross-branch bookings appear only as grey
  "Booking at <branch>" blocks.
- **Inconsistent time and date formats:** workspace set to 24 h, yet global search showed "11:00 AM". Dates appear as "Sun, Sep 27, 2026", "27 Sep
  2026, 15:59" and "Sunday, 27 Sep 2026 at 15:59". The receipt PDF uses "$" for SGD.
- **Report latency:** "Data from 26–28 mins ago". The Daily sales summary is live.
- **Terminology:** "Team member" / "Professional" (not "Barber"), "Walk-In", "Checkout", "Pay run", "Register", "Stocktake".
  Burmese UI isn't available.
- **Irreversible actions** are clearly worded (merge clients, void sale, complete stocktake: "cannot be undone"). Irreversible merge keeps the
  newer profile name.
- **Mobile (390 px responsive web):** "Download the app" banner, single-member calendar column with a team switcher, bottom navigation (Calendar,
  Sales, +, Clients, More), no horizontal scroll. Evidence: `evidence/ux/mobile-390-calendar.png`, `evidence/ux/mobile-390-daily-sales.png`,
  `evidence/ux/mobile-390-clients.png`
- **Tablet (820 px portrait):** desktop sidebar kept, condensed icon toolbar. Evidence: `evidence/ux/tablet-820-calendar.png`
- **Desktop:** dense but complete. Many full-screen wizards (location, transfer, pay run, import, stocktake) with progress bars.

**INFERRED / environment-dependent**
- The web app **sometimes loaded to a blank page or a spinner on full navigation** and needed a reload (observed several times).
  Evidence: `evidence/ux/loading-hang-clients-list.png`. This may come from the WSL/Linux test browser rather than Fresha, so it is **not
  attributed to Fresha**.

## Speed hotspots for a barbershop (~70 customers/day, 3 branches)

1. **Walk-in to paid** is 8–15 clicks depending on path. The fastest path (slot → service → Save → Checkout → method → Pay) needs the barber's
   column, not the quick-sale screen, to get attribution right.
2. **Checkout** always passes the tip step. With split Cash + KBZPay it reaches ~12 clicks.
3. **Reschedule / cancel** need 4–6 clicks and the Options menu.
4. **Multi-branch overview** needs repeated location switching (no combined view).

## NOT VERIFIED

- Fresha native mobile/tablet apps (barber app, clock-in, notifications).
- Drag-and-drop rescheduling, keyboard shortcuts.
- Real-world speed with 15+ barber columns and ~70 bookings/day (sandbox had 2–3 members per location).
