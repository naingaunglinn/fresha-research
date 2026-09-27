# Notifications: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Test clients used non-deliverable `@example.com` emails and no
> phone numbers, so client notifications were generated but failed ("Error"). No second staff user was logged in, so staff-to-staff
> delivery is not verified.

## Navigation

- Top bar **bell** (`notification-button`) → drawer; drawer → **Notification settings** (per user, per workspace:
  `/user-account/workspaces/<id>/settings/edit-workspace-notifications-modal/`); `Marketing → Automations` (client messages);
  `Marketing → Messages history`; `Settings → Scheduling → Booking options → Email notifications` (staff emails for online bookings).

## OBSERVED: staff (in-app / push / email)

- **Bell drawer**: tabs **Appointments, Reviews, Tips, Online sales**; items with a "Read" state; the sandbox showed three "New appointment (DEMO)"
  items ("10:00 today Blow Dry for Jack booked with Wendy"). **None of my own staff actions** (creating, rescheduling, cancelling appointments,
  no-show, sales) appeared in my bell. Evidence: `evidence/notifications/bell-01.png`
- **Notification preferences** (per user):
  - **Locations** filter ("Notifications are sent for activity at all locations" / selected locations)
  - Appointments: "Notify me about **Only my appointments** / **Activity concerning all team members**"
  - *Client activity (online)*: new appointment, appointment confirmed (card/deposit), reschedules, cancellations, waitlist entries: Push / In-app
    (+ Email option at group level)
  - *Team member activity (calendar)*: new appointments, reschedules, cancellations, no-shows (**ON**), appointment status updates (**OFF**),
    waitlist entries
  - Sales: online product sales (email / push / in-app), online membership and package sales, **tips**
  - Reviews: new review
  - Messaging: Client Connect (new client message), Team Connect (direct messages, mentions, thread replies, channel messages)
  - **Inventory: Low stock alerts; weekly Low stock summary**
  - Insights: **daily / weekly / monthly business performance summary (email)**
  - AI Concierge: client note
  - Evidence: `evidence/notifications/notification-settings.png`, `evidence/notifications/notification-settings.aria.txt`
- Staff **emails for online bookings**: Booking options → "Send emails to team members when clients book, reschedule or cancel appointments
  online — Send emails to specific addresses: <owner email>". Evidence: `evidence/settings/scheduling-booking-options.png`

## OBSERVED: client notifications

- **Automations catalogue** (channels **Email, Text message, WhatsApp**; communication balance **SGD 0**, auto top-up offered):
  - Reminders: **3 days**, **24 hours**, **1 hour** before (enabled)
  - Appointment updates: New appointment, Rescheduled, Canceled, **Did not show up**, Thank you for visiting (review link) (enabled), Thank you
    for tipping (disabled)
  - Waitlist: Joined the waitlist, Time slot available
  - Increase bookings: Reminder to rebook (enabled); Celebrate birthdays, Win back lapsed clients, Reward loyal clients (off)
  - Celebrate milestones: Welcome new clients (off)
  - Client messages: New chat message, Message received
  - Client loyalty: points, tiers, rewards, referrer rewards
  - Evidence: `evidence/notifications/automations-01.png`
- Automation detail: Performance (sent / delivered / opened / clicked by channel), Preview (e.g. email subject "Your appointment is confirmed
  for Wed, Sep 30 at 11:00", sender "Baber Shop <owner email>"), Details ("Send to clients when a new appointment is booked", channels Email,
  Text message, WhatsApp). Evidence: `evidence/notifications/automation-new-appointment-preview.png`,
  `evidence/notifications/automation-new-appointment-details.png`
- **Per-action toggles** default to notify: reschedule "☑ Notify <client> about reschedule", cancel "☑ Send a cancellation notification",
  no-show "☑ Send a no-show notification". Evidence: `evidence/booking/reschedule-update-modal.png`, `evidence/booking/cancel-modal.png`,
  `evidence/booking/noshow-modal.png`
- **Messages history**: Time sent, Client, Appointment ref, Channel, **Type (Confirmation, Cancellation, Reschedule)**, **Status (Error for
  example.com)**. Evidence: `evidence/notifications/messages-history-01.png`
- Failures are also logged on the appointment ("Notification failed to send — Cancellation Email failed to send").
  Evidence: `evidence/audit/appt-activity-cancelled.png`
- Clients have per-channel **notification consent** and separate **marketing consent** (all ON by default) and a preferred notification language.
  Evidence: `evidence/customers/quick-add-client-settings.aria.txt`

## USER-PROVIDED

- Planned: **in-app staff notifications** with **90-day notification history** (brief §26).

## INFERRED

- Fresha doesn't notify a user about their own actions. My actions produced no bell items even though team-activity notifications were ON.

## NOT VERIFIED

- Delivery of staff notifications to another staff user (barber) in-app or by push (no barber login).
- **Notification retention period** in the bell (not shown).
- Stock, payroll or security notifications actually firing (only preference toggles seen; no payroll or security category exists in preferences).
- SMS / WhatsApp sending in a Myanmar workspace (paid communication balance; +95 numbers).
- No-show message: "Did not show up" is enabled, yet no message appeared in Messages history for the demo no-show. Reason unknown.

## Notes for the gap analysis

- Fresha's staff notifications are configurable per user and channel. There's no payroll or finance-approval notification category.
  Client messaging (SMS / WhatsApp) is a paid, balance-based feature.
