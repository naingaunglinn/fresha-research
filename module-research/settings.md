# Settings: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Only test-relevant settings were changed (location, custom
> payment method, register, commission plan). See `test-data-log.md`.

## Navigation

- `Settings` (`/setup`): **Business setup, Scheduling, Sales, Clients, Billing, Team, Forms, Payments**; also Online presence, Marketing,
  Other (Add-ons, Integrations) cards. User menu → **Personal settings** (Personal info, Login & security, Appearance).
  Evidence: `evidence/_nav/settings-index.png`

## OBSERVED

| Area | Observed settings | Evidence |
| --- | --- | --- |
| Company / business details | Business name; **Country and Currency fixed at creation** ("Your country is set to Singapore with SGD currency"); tax calculation (retail prices exclude / include tax); team default language; client default language; external links | `evidence/settings/business-details-edit.png` |
| **Language** | 39 UI languages (e.g. English UK/US, Thai, Vietnamese, Malay, Indonesian, Chinese CN/HK, Japanese, Korean…). **Burmese / Myanmar is not offered.** "Team members and clients can override the language displayed to them" | `evidence/settings/language-picker.png` |
| Branch settings | Per location: details, address, opening hours, receipt sequencing, tax defaults, tipping, receipt details | `branches.md` |
| **Currency** | SGD in sandbox (fixed). The live account uses MMK (USER-PROVIDED) | `evidence/settings/business-details-edit.png` |
| **Date format** | **No date-format setting** in "Date and time settings" | `evidence/settings/date-time-settings-edit.aria.txt` |
| **Time format** | **12 hours (e.g. 9:00pm) or 24 hours (e.g. 21:00)** | same |
| Time zone / week | 424 time zones incl. **"(GMT +06:30) Yangon"**; first day of week | same |
| Calendar settings | Appointment colour source; display processing time; display blocked time; **display cross-location appointments** | `evidence/settings/scheduling-time-and-calendar.png` |
| Booking settings | Booking window, lead time, cancel / reschedule cutoff, slot interval, intelligent slots, dynamic assignment, booking options, waitlist, resources, blocked time types, closed periods, appointment statuses | `booking.md`, `evidence/settings/scheduling-availability-edit-0.aria.txt` |
| **Cancellation settings** | Cancellation reasons list (custom); online cancel cutoff; fees require payment policy (Fresha Payments) | `evidence/settings/scheduling-cancellation-reasons.png`, `evidence/settings/payments-settings.png` |
| Sales settings | Pay now; tax rates (business / location; groups); receipts (fields, custom lines, footer, sequencing); registers; tipping; service charges; gift cards; **custom checkout methods (name only)** | `evidence/settings/sales-receipts.png`, `evidence/settings/sales-tipping.png`, `evidence/payments/custom-methods-after-kbzpay.png` |
| Client settings | Client sources (8 default + custom), client tags, Client Connect | `evidence/settings/clients-settings.png` |
| Team settings | Permission roles, time off types, timesheets, shifts, pay runs, commissions, PIN switching | `staff.md` |
| Forms | Form templates (e.g. COVID 19, inactive) | `evidence/settings/forms-settings.png` |
| Payments | Payment policy / payment methods / card terminals: onboarding to Fresha Payments | `evidence/settings/payments-settings.png` |
| Billing | Billing details, bank accounts, payment methods, communication balance, invoices and fees, subscriptions | `evidence/settings/legal-entities.png` |
| **Notification settings** | Per-user staff preferences; client automations (see `notifications.md`) | `evidence/notifications/notification-settings.png` |
| **Security (personal)** | Login details: password, **Google / Apple** connect; **Trusted devices ("can skip two-factor authentication")**; **Active sessions** (per device, sign out, sign out of all devices); Delete account | `evidence/settings/personal-login.png` |
| Appearance | Theme Light / Dark / System | `evidence/settings/personal-appearance.png` |
| Integrations / add-ons | Add-ons: Payments, Premium Support, **Insights**, Google Rating Boost, Client Loyalty, **Data Connector**, AI Concierge (beta), Client Connect (active), Smart Website, Team Connect, Bookable Resources; Integrations: Xero, QuickBooks… | `evidence/booking/online-google-reserve.png` |
| Partner login | Email + verification code, "Continue with mobile", Google, Apple; reCAPTCHA | `evidence/_setup/00-login-page.png` |
| Data / maintenance settings | **OBSERVED absence**: no backup, data-retention or maintenance settings screen found (only exports and the Data Connector add-on) | `evidence/_nav/settings-index.png` |

## USER-PROVIDED

- Planned: Myanmar + English, MMK, **12-hour time**, **DD/MMM/YYYY**, weekly backup with 1-year retention (brief §26).
- Live account = Myanmar / MMK.

## INFERRED

- Date display seems to follow locale rather than a setting. Formats seen in the UI include "Sun, Sep 27, 2026", "27 Sep 2026, 15:59" and
  "Sunday, 27 Sep 2026 at 15:59". Global search showed "11:00 AM" although the workspace was set to 24 h.

## NOT VERIFIED

- How MMK amounts are formatted; whether "Myanmar" was selectable at sign-up (only the user's statement that the live account is Myanmar/MMK).
- Two-factor authentication enrolment options (trusted devices mentioned; no 2FA setup screen opened).
- Backup / restore: not offered in the UI; Fresha's internal backup policy is outside the product UI.
