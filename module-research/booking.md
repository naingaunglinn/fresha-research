# Booking / Appointments: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27, staff side (partner web app) observed
> end to end. The customer side was observed on a **third-party public Fresha venue** (anonymous, stopped before
> login/submit). The sandbox's own online booking was **not published**, by the user's decision.
> Test appointments are listed in `test-data-log.md` rows 6–8, 13–15, 33–34.

## Navigation

- `Calendar` (`/calendar?date=…&view=day&location_id=…`); `Sales → Appointments` (appointments list);
  `Settings → Scheduling` (booking rules); `Online presence → Link builder / Marketplace profile`.

## OBSERVED: calendar

- Toolbar: Today, date navigation, **location picker (one location at a time; lists single locations only, so there's no
  combined all-branches view)**, team picker (Scheduled team / All team / per-member checkboxes), filters drawer
  (appointment status, type, channel, payment status, services, appointment creation date, requested team member, client
  segments, saved filters), calendar settings, **Waitlist**, refresh, view **Day / 3 day / Week / Month**, **Add** menu
  (**Appointment, Group appointment, Blocked time, Sale, Quick payment**).
  Evidence: `evidence/booking/calendar-01.png`, `evidence/booking/calendar-menu-view.png`,
  `evidence/booking/calendar-menu-location.png`, `evidence/booking/calendar-menu-team.png`, `evidence/booking/calendar-filters-drawer-b.png`
- One column per team member; time outside a member's shift is hatched; red current-time line.
- A member's appointment at **another branch** appears as a hatched block **"Booking at <branch>"** in their column.
  Calendar settings include "Display cross-location appointments". Evidence: `evidence/booking/calendar-baber-tue29-aung.png`,
  `evidence/settings/scheduling-time-and-calendar.png`
- Clicking an empty slot opens: **Add appointment / Add group appointment / Add blocked time / Quick actions settings**.
  Evidence: `evidence/booking/calendar-slot-click.png`

## OBSERVED: booking entry points (staff)

| Entry | UI sequence (observed) | Selection order | Clicks* |
| --- | --- | --- | --- |
| **Time/staff-first** (slot) | Click empty slot in barber's column → Add appointment → (Add client → search → pick, or leave empty = walk-in) → pick service → Save | Time + barber → client → service | ~6 + typing |
| **Service-first** ("View available times") | Add → Appointment → "Select a time to book" banner → **View available times** → (client) → service → team member (default **Any team member**) → Continue → date strip → time → Continue → Save | Client → service → barber → date → time | ~10–13 |
| **Pick-from-calendar** | Add → Appointment → click a slot on the calendar (banner "Select a time to book") | Time first | ~4 + drawer |
| **Client-first** | The drawer opens with "Add client — or leave empty for walk-ins" on the left, so client can be chosen first in any flow | Client first | same as above |
| **Branch-first** | Choose location in calendar location picker, then any flow above | Branch first | +2 |

\*Clicks counted while driving the flow in this session. They exclude scrolling and typing.

Evidence: `evidence/booking/new-appt-01.png` (banner), `evidence/booking/new-appt-drawer-01.png`,
`evidence/booking/new-appt-after-service.png`, `evidence/booking/new-appt-time-step.png`,
`evidence/booking/new-appt-confirm-step.png`, `evidence/booking/slot-new-appt-01.png`, `evidence/booking/slot-new-appt-02.png`.

### Drawer details

- Client panel: search, **Add new client**, **Walk-In**, existing clients. Evidence: `evidence/booking/new-appt-add-client-01.aria.txt`
- Service list shows duration and price; services the selected member doesn't provide are flagged
  "Team member doesn't provide this service". Evidence: `evidence/booking/slot-new-appt-01.png`
- Team member per service line: **Any team member** (default in the service-first flow) or a specific member of that location.
  Evidence: `evidence/booking/new-appt-team-member-picker.png`
- Time step: date strip (months ahead), **Available times** in **15-min steps**, "Pick from calendar", and when nothing fits:
  "Fully booked on this date — Available from Mon 28 Sep — Next available date — **Join the waitlist**".
  Evidence: `evidence/booking/new-appt-time-step.png`, `evidence/booking/new-appt-times-mon28-any.png`
- Summary: date, time, **"Doesn't repeat"** (Every day / Every week / Every month / Custom), services with time·duration·member,
  Add service, Total, To pay, **Options** (Add a note, Add payment policy), **Checkout**, **Save**.
  Evidence: `evidence/booking/new-appt-confirm-step.png`, `evidence/booking/new-appt-options-menu.png`, `evidence/booking/new-appt-repeat-options.png`
- The drawer's time field accepts **any time 00:00–23:55 in 5-min steps**, not only available slots.
  Evidence: `evidence/booking/drawer-time-picker.png`
- Closing with unsaved changes → "You have unsaved changes… Do you wish to exit? Go back / Yes, exit".
  Evidence: `evidence/booking/unsaved-changes-modal.png`

## OBSERVED: availability calculation

| Test | Result | Evidence |
| --- | --- | --- |
| Branch B, Mon 28 Sep, Haircut 45 min, **Any team member** (Min 09–19, Aung 14–18 at Branch B) | 09:00 … 18:15 | `evidence/booking/new-appt-times-mon28-any.png` |
| Same, **Aung** only (Mon: Baber Shop 09–13, Branch B 14–18) | 14:00 … 17:15, so the **per-branch split shift is honoured** | `evidence/booking/new-appt-times-mon28-aung.png` |
| Today (Sun 15:43) at Branch B, closing 16:00 | "Fully booked on this date… Available from Mon 28 Sep" | `evidence/booking/new-appt-time-step.png` |
| Min on unapproved half-day leave 09–13 | Slots start 13:00 for Any and Min | `evidence/leave/availability-with-time-off.png` |
| Haircut (Min) + Blow Dry (Aung), Tue 29; Aung busy at **Baber Shop** until 11:00 | First slot **10:15** (services chained; cross-branch busy time respected) | `evidence/booking/multi-service-02-times.png` |
| Duration/price with branch & barber overrides | Branch B Min 50 min / 45; Aung 50 min / 50; Any "from 45" | `services.md` |

## OBSERVED: conflicts and double booking

- **Cross-branch double booking is possible for staff.** Aung had a Branch B booking 10:00–10:45 (Tue 29). At Baber Shop I
  created a walk-in for Aung at 10:15. The drawer showed an inline warning **"Team member is not available"**, but **Save
  succeeded** ("Appointment created") with no confirmation dialog. The calendar then showed the two overlapping side by side.
  Evidence: `evidence/booking/cross-branch-conflict-before-save.png`, `evidence/booking/calendar-after-double-booking.png`
- The inline warning **persisted** on the saved appointment. Evidence: `evidence/booking/appt-details-walkin-01.png`
- Rescheduling into a slot outside the member's shift → "Reschedule appointment? <member> isn't scheduled to work at this time —
  Go back / **Reschedule**" (override allowed). Evidence: `evidence/booking/reschedule-hint-modal.png`
  - Anomaly: this warning also appeared for a click at about 16:05, inside Aung's 14:00–18:00 Branch B shift. Cause
    **NOT VERIFIED** (possibly a click-position artefact).
- **The same client could hold two future bookings** (Mon 28 and Tue 29) with no warning. Evidence:
  `evidence/booking/appointments-list-all-time.png`

## OBSERVED: appointment lifecycle

- Statuses in the appointment drawer: **Booked, Confirmed, Arrived, Started, No-show, Cancel**. Settings list **Booked,
  Confirmed, Arrived, Started, Completed, Canceled, No-show**, and custom statuses can be added.
  Evidence: `evidence/booking/appt-status-menu.png`, `evidence/settings/scheduling-appointment-statuses.png`
- Changing a status closes the drawer; activity logs "Appointment status updated to Arrived / Started by <user>".
  Evidence: `evidence/audit/appt-activity-02-status-changes.png`
- Existing-appointment **Options**: Add a note, Add a form, Add payment policy, **View appointment activity**, Set as repeating,
  Add to group appointment, Rebook, **Reschedule**, **No-show**, **Cancel**; buttons **Pay now**, **Checkout**.
  Evidence: `evidence/booking/appt-options-menu-existing.png`
- **Checkout and completion**:
  - Checking out a *future* appointment early (Tue 29, checked out on Sun 27) left it **"Started"** with "View sale" and
    **"Complete now"**. "Complete now" → "Completed". Evidence: `evidence/booking/walkin-after-checkout-refund.png`, `evidence/booking/completed-appt.png`
  - Checking out a *same-day, already started* appointment (Jane Doe, 27 Sep 11:00) set it to **"Completed" automatically**.
    Evidence: `evidence/booking/same-day-checkout-appt-status.png`
  - The **sale date is the checkout date**, not the appointment date (Sale #1 dated 27 Sep for a 29 Sep appointment).
    Evidence: `evidence/payments/checkout-07-complete.png`

### Reschedule (performed)

`Open appointment → Options → Reschedule` → calendar in "Select a time to book" mode (**location picker disabled**, so there's
no cross-branch move in this flow) → click new slot → "Update appointment — ☑ Notify <client> about reschedule" (checked by
default) → **Update** → "Appointment rescheduled". ~5 clicks.
Evidence: `evidence/booking/reschedule-01.png`, `evidence/booking/reschedule-update-modal.png`
(Drag-and-drop rescheduling was not tested.)

### Cancel (performed)

`Options → Cancel` → "Are you sure you want to cancel?" (appointment total, **"No fee will be charged — No policy was applied to
this appointment"**, ☑ Send a cancellation notification, **Cancellation reason: default "No reason provided"** = optional; list
Duplicate appointment / Appointment made by mistake / Client not available + custom reasons) → **Cancel appointment**. 4–6 clicks.
Evidence: `evidence/booking/cancel-modal.png`, `evidence/settings/scheduling-cancellation-reasons.png`

### No-show (performed on demo data)

`Options → No-show` → "Are you sure you want to mark as no-show?" (total, no fee / no policy, ☑ Send a no-show notification;
**no reason field**) → **Set as no-show** → "Appointment marked as no-show". Evidence: `evidence/booking/noshow-modal.png`

### Group / repeating / waitlist

- Staff: "Group appointment" in the Add menu and slot menu; "Add to group appointment" on existing appointments (not explored).
- Repeating: "Doesn't repeat" → Every day / Every week / Every month / Custom. Evidence: `evidence/booking/new-appt-repeat-options.png`
- Waitlist: calendar Waitlist drawer; settings "Automatically book", priority "First in line", online waitlist active.
  Evidence: `evidence/settings/scheduling-waitlist.png` (settings); calendar Waitlist button seen in the toolbar (`evidence/booking/calendar-01.png`), drawer content not captured

## OBSERVED: booking rules (Settings → Scheduling)

| Rule | Options observed | Evidence |
| --- | --- | --- |
| Advance booking window (online) | **"up to 1…12 months in advance"**; there's no day-based option such as 14 days | `evidence/settings/scheduling-availability-edit-0.aria.txt` |
| Booking cutoff / lead time | immediately; 15/30/45 min; 1–12 h; 24 h; 2–7 days; 14 days before start | same |
| Online cancel/reschedule cutoff | Anytime; 30 min … 72 h before start; "Show your contact number when online changes aren't allowed" | same |
| Slot interval / gap control | 15 min interval; Regular (max availability) / Reduce calendar gaps / Eliminate calendar gaps | `evidence/settings/scheduling-availability-edit-1.aria.txt` |
| "Any professional" assignment | Fill open calendars (day / prior 7 / prior 14 days), Take turns, Build ratings (fewest reviews), Custom priority order; Prioritize last booked team member; exclude members; allow splitting multi-service across members | `evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt` |
| Reassignment | Online-booked (and optionally team-booked) no-preference appointments can be moved to free a requested member; cutoff 15 min | `evidence/settings/scheduling-dynamic-assignment-edit-1.aria.txt` |
| Booking options | Clients can book specific members, view profiles/portfolio/ratings, gender filter off, group booking on, upselling, important info, **email to staff on online book / reschedule / cancel** | `evidence/settings/scheduling-booking-options.png` |

## OBSERVED: customer self-booking (third-party public venue, anonymous)

`Venue page ("Book now")` → **Book an appointment / Book group appointment** → **Select services** (categories; per-service
**add-ons** picker) → **Select professional** (**"Any professional — Maximum availability"** or a named barber with rating and
title) → **Select date and time** (date strip; times in the venue's 12-hour format; "Can't find a suitable time? Join waitlist")
→ **"Log in or sign up to book — We'll need to verify it's you"**: phone number with **SMS verification code**, or Continue with
email / Google / Apple. (Stopped here; nothing entered.)
Evidence: `evidence/booking/public-02-venue-page.png`, `evidence/booking/public-03-select-option.png`, `evidence/booking/public-04-services.png`,
`evidence/booking/public-04c-after-plus.png`, `evidence/booking/public-06-time.png`, `evidence/booking/public-07-time.png`,
`evidence/booking/public-09-after-time-continue.png`

## OBSERVED: links, widgets, QR

- Link builder: "Create shareable links and **QR codes**": Link to everything, **Link to services ("for certain services,
  locations or team members")**, packages, memberships, gift cards. Creating one shows "To sell services online, publish
  Fresha profile". Evidence: `evidence/booking/online-buttons-and-links.png`, `evidence/booking/link-builder-services-01.aria.txt`
- Other channels in navigation: Marketplace profile, Reserve with Google, Facebook & Instagram bookings, Smart Website (add-on),
  AI Concierge (add-on). Evidence: `evidence/_nav/nav-d-online-presence.png`, `evidence/booking/online-google-reserve.png`

## OBSERVED: history, audit, notifications

- Appointment activity (last 12 months): created (who, reference), status updates, sale created ("Checked out by … with sale
  receipt 1"), cancellation ("Canceled by …", **reason not shown**), notification failures. Evidence:
  `evidence/audit/appt-activity-03-after-checkout.png`, `evidence/audit/appt-activity-cancelled.png`
- Appointments list: Ref #, Client, Service, Created by, Created date, Scheduled date, Duration, Location, Team member, Price,
  Status; date presets Today … All time; Filters; Export. Evidence: `evidence/booking/appointments-list-all-time.png`,
  `evidence/booking/appointments-list-date-range.png`
- Client notifications sent automatically for new / rescheduled / cancelled appointments (see `notifications.md`).

## USER-PROVIDED

- Planned: flexible booking selection, **Any Barber**, **14-day default advance window**, **one active booking per customer**
  (brief §26).

## INFERRED

- Staff-created overlapping bookings are only soft-warned, so double booking a barber across branches depends on staff
  discipline in Fresha.

## NOT VERIFIED

- The sandbox's **own** online booking (not published): branch-specific links, QR, widget and customer self-booking against our
  configuration, and whether customers are limited to one active booking.
- Customer-side reschedule and cancel within the cutoffs.
- Drag-and-drop reschedule; group appointments; recurring series behaviour; waitlist auto-booking.
- Activity-log content for a **rescheduled** appointment (before/after times). Two load attempts failed and then the session ended.
- Staff (barber) receipt of booking notifications (no barber login).

## Notes for the gap analysis

- Fresha's advance window can't be set to 14 days (minimum 1 month).
- Fresha doesn't enforce one active booking per customer for staff-created bookings.
- Fresha allows staff to override conflicts (double booking, outside shift).
- The customer online flow order is Services → Professional → Time → Login, matching "service-first".
