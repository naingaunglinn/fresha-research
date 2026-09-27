# Audit / Activity history: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial), 2026-09-27. Fresha has **no central audit log**. History lives on individual records.

## OBSERVED: where history exists

| Record | What is logged | Who / when | Before → after | Reason | Retention shown | Evidence |
| --- | --- | --- | --- | --- | --- | --- |
| Appointment ("View appointment activity") | Created (with reference), status updates (Arrived, Started), sale created ("Checked out… sale receipt 1"), **canceled**, notification failures | ✓ ("by Naing Aung", timestamp) | Status: new value only | **Cancellation reason not shown** in the log | "last **12 months**" | `evidence/audit/appt-activity-02-status-changes.png`, `evidence/audit/appt-activity-03-after-checkout.png`, `evidence/audit/appt-activity-cancelled.png` |
| Sale (Activity tab) | Sale created / completed, each payment with **"Payment taken by"**, void ("Voided by") | ✓ | – | Void: no reason captured | "last **90 days**" | `evidence/audit/sale-activity.png` |
| Refund document | Refund #N with reason (Client's request), items, methods | ✓ (via sale) | – | ✓ (required list) | n/a | `evidence/payments/refund-04-done.png` |
| Stock (product → Stock history) | Adjustments, transfers received, sales, returns | ✓ (member, location, date) | Stock on hand **after** each entry; cost price | ✓ (reason / description) | "Load more" pagination | `evidence/inventory/product-stock-history-after-transfer.png` |
| Stock transfer / stocktake | Transfer drawer has an **Activity** tab (not opened); stocktake summary: started / completed, **counted by**, **reviewed by** | ✓ | Expected vs counted | Stocktake note (optional) | n/a | `evidence/inventory/stock-transfer-T1-detail.png`, `evidence/inventory/stocktake-05-complete.png` |
| Timesheet (Activity tab) | Creation lines and edits | ✓ | **✓ "Clock-in time edited from 10:00 to 10:10"** | – (no reason field) | n/a | `evidence/attendance/timesheet-activity.png` |
| Pay run breakdown (Activity tab) | Commission created / deleted (with cause text, e.g. "Deleted because the sale was refunded by …"), tip created | ✓ | Amounts | Cause text (system) | per period | `evidence/payroll/pay-run-breakdown-after-refund.png` |
| Register period | Opened by / at, closed period times, counted, difference; cash-out with reason, note, user and date | ✓ | Expected vs counted | Cash-out reason category + note; **no reason for count differences** | Closed-register record (drawer); list refresh not verified | `evidence/finance/register-closed.png` |
| Client merge | Client details note "profile has been merged with …" | – | – | – | – | `evidence/customers/client-profile-tab-client-details.png` |
| Client messages | Messages history (time, client, appointment, channel, type, status) | – | – | – | list | `evidence/notifications/messages-history-01.png` |

## OBSERVED absence

- **No activity/history view for client profile edits** (profile tabs: Overview, Appointments, Sales, Client details, Items, Records, Wallet,
  Loyalty, Reviews; none is an audit trail). Evidence: `evidence/customers/client-profile-01.png`
- **No activity/history for team member changes** (role, locations, wages, commission plan), service or price changes, settings changes, or
  permission changes, found in the screens visited.
- Voids leave **no commission-deletion trace** in pay-run activity (refunds do).
- No permission named for viewing audit logs (see `roles-permissions.md`).

## USER-PROVIDED

- Brief §21 requires researching who changed what, timestamps, before/after and reasons.

## NOT VERIFIED

- Activity-log content for a **rescheduled** appointment (whether old and new times are shown). Two attempts timed out before the browser
  session ended.
- Whether a central audit log exists in higher plans or the Data connector add-on.

## Notes for the gap analysis

- Fresha's history is **record-scoped and uneven**: good for stock and timesheets (before/after), partial for appointments (no cancellation
  reason, statuses without "from"), and absent for client, staff and settings changes. Retention differs per record type (12 months vs 90 days).
