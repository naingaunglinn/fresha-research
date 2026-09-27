# Coverage Checklist

Every bullet from brief §4–§24. Status must end as one of OBSERVED / USER-PROVIDED / INFERRED / NOT VERIFIED (plus FRESHA GAP / LOCKED-ON-PLAN qualifiers where relevant). Final state: **0 PENDING**. "OBSERVED absence" = feature not found in the screens, menus and catalogues visited.

## §4 Branch / Location (branches.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| branch/location creation | OBSERVED | `evidence/branches/add-location-01.aria.txt` | 4-step wizard; phone + email required; address search limited to workspace country |
| branch information | OBSERVED | `evidence/branches/location-detail-01.png` | name, email, phone, business types, address |
| opening hours | OBSERVED | `evidence/branches/location-opening-hours.png` | per weekday, several ranges per day |
| branch availability | OBSERVED | `evidence/booking/new-appt-times-mon28-aung.png` | availability computed per location; closed periods per location |
| staff assigned to branches | OBSERVED | `evidence/staff/add-team-member-locations.aria.txt` | 'Works at' all / specific locations |
| multi-branch staff | OBSERVED | `evidence/schedule/scheduled-shifts-baber-shop.png` | overlapping cross-branch shifts allowed |
| branch-specific settings | OBSERVED | `evidence/branches/location-sales.png` | receipt sequencing, tax defaults, tipping, receipt text |
| branch-specific services | OBSERVED | `evidence/services/service-edit-haircut-tab-locations.aria.txt` | All locations / per location |
| branch-specific pricing | OBSERVED | `evidence/services/advanced-pricing-all-locations.aria.txt` | location + barber-at-location overrides |
| branch-specific schedules | OBSERVED | `evidence/schedule/repeating-shifts-editor-01.png` | repeating shifts per location |
| branch filtering | OBSERVED | `evidence/booking/calendar-menu-location.png` | one location per calendar view; report Location filter |
| branch reports | OBSERVED (no dedicated report) | `evidence/reports/sales-summary-groupby.png` | Location filter / Group by Location only |
| branch permissions | OBSERVED | `evidence/roles/permission-matrix.md` | 'Can view and access all locations' |

## §5 Staff (staff.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| staff creation | OBSERVED | `evidence/staff/add-team-member-profile.aria.txt` | email required |
| staff profile | OBSERVED | `evidence/staff/add-team-member-profile.aria.txt` |  |
| employee information | OBSERVED | `evidence/staff/add-team-member-profile.aria.txt` | employment type, team member ID, start/end date |
| roles | OBSERVED | `evidence/roles/permission-roles-list.png` | Basic/Low/Medium/High/Owner/No access + custom |
| permissions | OBSERVED | `evidence/roles/permission-matrix.md` | 121 toggles |
| branch assignment | OBSERVED | `evidence/staff/add-team-member-locations.aria.txt` |  |
| multiple branches | OBSERVED | `evidence/schedule/scheduled-shifts-baber-shop.png` |  |
| service eligibility | OBSERVED | `evidence/staff/add-team-member-services.aria.txt` |  |
| schedule | OBSERVED | `evidence/schedule/scheduled-shifts-01.png` |  |
| availability | OBSERVED | `evidence/booking/new-appt-times-mon28-aung.png` |  |
| leave/time off | OBSERVED | `evidence/leave/add-time-off-01.png` |  |
| attendance | OBSERVED (manager entry) / NOT VERIFIED (self clock-in) | `evidence/attendance/timesheet-add-01.png` | self clock-in presumably in mobile app |
| staff login | NOT VERIFIED | `evidence/staff/team-list-after-add.png` | 'Pending invitation' observed; no barber login available |
| account activation | NOT VERIFIED | `evidence/staff/team-list-after-add.png` | invites went to @example.com |
| account deactivation | OBSERVED | `evidence/staff/archive-modal.png` | Archive (restorable); future bookings untouched |
| staff status | OBSERVED | `evidence/staff/team-list-after-add.png` | Pending invitation; archived via filter |
| staff performance | OBSERVED (report catalogue) | `evidence/reports/reports-index-01.aria.txt` | Performance insights drawer not opened |
| staff reports | OBSERVED | `evidence/reports/commission-summary.png` | commission, attendance, wages, tips reports |
| staff commission | OBSERVED | `evidence/commission/after-apply.png` |  |
| payroll-related features | OBSERVED | `evidence/staff/add-team-member-pay-runs.aria.txt` | hourly wages only |
| notifications | OBSERVED (preferences) / NOT VERIFIED (delivery) | `evidence/notifications/notification-settings.png` | no second staff login |

## §6 Services (services.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| service categories | OBSERVED | `evidence/services/service-menu-01.png` |  |
| service creation | OBSERVED (edit form) / NOT VERIFIED (Add flow not run) | `evidence/services/service-edit-haircut-01.aria.txt` | existing service edited; new service not created |
| service names | OBSERVED | `evidence/services/service-edit-haircut-01.aria.txt` | ≤255 chars |
| descriptions | OBSERVED | `evidence/services/service-edit-haircut-01.aria.txt` | ≤1000, Generate with AI |
| prices | OBSERVED | `evidence/services/service-edit-haircut-01.aria.txt` | Free / From / Fixed |
| duration | OBSERVED | `evidence/services/service-extra-time.png` | 5 min–12 h + processing / blocked / extra time |
| branch-specific services | OBSERVED | `evidence/services/service-edit-haircut-tab-locations.aria.txt` |  |
| branch-specific price | OBSERVED | `evidence/services/advanced-pricing-all-locations.aria.txt` |  |
| branch-specific duration | OBSERVED | `evidence/services/advanced-pricing-set.png` |  |
| staff eligibility | OBSERVED | `evidence/services/service-edit-haircut-tab-team-members.aria.txt` |  |
| service availability | OBSERVED | `evidence/services/service-edit-haircut-tab-online-booking.aria.txt` | limit by dates / weekday-time; online on/off |
| add-ons | OBSERVED (section; public venue picker) / NOT VERIFIED (own config) | `evidence/booking/public-04c-after-plus.png` |  |
| packages | OBSERVED (exists) / NOT VERIFIED (details) | `evidence/_nav/nav-d-catalog.png` |  |
| multiple services | OBSERVED | `evidence/booking/multi-service-03-summary.png` | chained, different barbers |
| service variations | NOT VERIFIED | `evidence/services/service-options-menu.png` | 'Add variant' option seen only |
| service history | OBSERVED | `evidence/customers/client-profile-tab-items.png` | client profile Items tab |
| service reporting | OBSERVED | `evidence/reports/sales-summary-groupby.png` | group by category / item; Top services widget |
| Branch+Service+Barber+Duration+Price availability calculation | OBSERVED | `evidence/services/booking-price-branchB-aung.png` | see services.md table |

## §7 Booking (booking.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| customer-first booking | OBSERVED | `evidence/booking/new-appt-add-client-01.aria.txt` |  |
| staff-first booking | OBSERVED | `evidence/booking/slot-new-appt-01.png` | slot in barber column |
| service-first booking | OBSERVED | `evidence/booking/new-appt-after-service.png` | View available times |
| date-first booking | OBSERVED | `evidence/booking/new-appt-time-step.png` | date strip / calendar date |
| branch-first booking | OBSERVED | `evidence/booking/calendar-menu-location.png` |  |
| multiple services | OBSERVED | `evidence/booking/multi-service-03-summary.png` |  |
| same barber for multiple services | INFERRED | `evidence/booking/multi-service-01.png` | per-line barber choice observed; same-barber combo not executed |
| different barber per service | OBSERVED | `evidence/booking/multi-service-03-summary.png` |  |
| Any Staff equivalent | OBSERVED | `evidence/booking/new-appt-team-member-picker.png` | Any team member / Any professional |
| available time slots | OBSERVED | `evidence/booking/new-appt-times-mon28-any.png` | 15-min interval |
| duration calculation | OBSERVED | `evidence/booking/multi-service-03-summary.png` | overrides + chaining |
| schedule conflicts | OBSERVED | `evidence/booking/reschedule-hint-modal.png` | soft warnings |
| double booking prevention | OBSERVED (soft warning only) | `evidence/booking/cross-branch-conflict-before-save.png` | save allowed |
| rescheduling | OBSERVED | `evidence/booking/reschedule-update-modal.png` | branch locked in reschedule mode |
| cancellation | OBSERVED | `evidence/booking/cancel-modal.png` |  |
| cancellation reasons | OBSERVED | `evidence/settings/scheduling-cancellation-reasons.png` | optional |
| booking statuses | OBSERVED | `evidence/booking/appt-status-menu.png` |  |
| no-show | OBSERVED | `evidence/booking/noshow-modal.png` | no reason field |
| booking cutoff | OBSERVED | `evidence/settings/scheduling-availability-edit-0.aria.txt` | lead time options |
| advance booking window | OBSERVED | `evidence/settings/scheduling-availability-edit-0.aria.txt` | 1–12 months only |
| booking confirmation | OBSERVED | `evidence/notifications/messages-history-01.png` | auto confirmation message; Confirmed status |
| booking links | OBSERVED (menu) / NOT VERIFIED (link creation needs published profile) | `evidence/booking/online-buttons-and-links.png` |  |
| booking widgets | OBSERVED (channels listed) / NOT VERIFIED | `evidence/_nav/nav-d-online-presence.png` |  |
| customer self-booking | OBSERVED (third-party public venue) / NOT VERIFIED (own config) | `evidence/booking/public-07-time.png` |  |
| branch-specific booking links | OBSERVED (text) / NOT VERIFIED | `evidence/booking/online-buttons-and-links.png` | 'Link to services… locations or team members' |
| QR possibilities | OBSERVED (text) / NOT VERIFIED | `evidence/booking/online-buttons-and-links.png` | 'shareable links and QR codes' |
| booking history | OBSERVED | `evidence/booking/appointments-list-all-time.png` |  |
| booking audit/history | OBSERVED / NOT VERIFIED (reschedule entry) | `evidence/audit/appt-activity-03-after-checkout.png` | 12 months |
| booking notifications | OBSERVED | `evidence/notifications/automations-01.png` |  |
| staff notifications | OBSERVED (preferences) / NOT VERIFIED (delivery) | `evidence/notifications/notification-settings.png` |  |
| customer notifications | OBSERVED | `evidence/notifications/messages-history-01.png` |  |

## §8 Walk-in (walk-in.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| walk-in customer | OBSERVED | `evidence/booking/calendar-after-double-booking.png` | 'Walk-In' block |
| customer without account | OBSERVED | `evidence/walk-in/quick-sale-06-done.png` | client 'Walk-In' |
| customer without phone | OBSERVED | `evidence/customers/quick-add-client-01.aria.txt` | no mandatory client field |
| selecting barber | OBSERVED | `evidence/walk-in/quick-sale-03-cart.png` | quick sale defaults to logged-in user |
| selecting service | OBSERVED | `evidence/walk-in/quick-sale-01.png` |  |
| starting service | OBSERVED | `evidence/audit/appt-activity-02-status-changes.png` | status Started |
| completing service | OBSERVED | `evidence/booking/same-day-checkout-appt-status.png` | auto-complete same day; Complete now for early checkout |
| payment | OBSERVED | `evidence/payments/checkout-03-payment.png` |  |
| customer record creation after service | OBSERVED (before payment only) | `evidence/walk-in/edit-sale-details.png` | 'Add client' available in the checkout cart before payment; not possible after payment (no client field in Edit sale details) |
| converting walk-in into customer history | OBSERVED (before payment only) | `evidence/payments/checkout-02-cart-or-tip.png` | only by adding the client during checkout; no conversion after payment observed |

## §9 Customers (customers.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| customer creation | OBSERVED | `evidence/customers/quick-add-client-01.aria.txt` |  |
| customer matching | OBSERVED | `research-log.md §11` | 'identical contact info' warning |
| duplicate detection | OBSERVED | `evidence/customers/clients-list-duplicate-banner.png` | soft warning + merge |
| phone number handling | NOT VERIFIED | `evidence/customers/quick-add-client-01.aria.txt` | no client phone entered; +65 default in SG sandbox |
| customer profile | OBSERVED | `evidence/customers/client-profile-01.png` |  |
| customer notes | OBSERVED (actions) / not executed | `evidence/customers/client-action-add-staff-alert.png` | staff alert, simple note, allergy |
| booking history | OBSERVED | `evidence/customers/client-profile-tab-appointments.png` |  |
| service history | OBSERVED | `evidence/customers/client-profile-tab-items.png` |  |
| payment history | OBSERVED | `evidence/customers/client-profile-tab-sales.png` |  |
| total visits | OBSERVED | `evidence/customers/client-profile-01.png` | Appointments count |
| total spending | OBSERVED | `evidence/customers/client-profile-01.png` | Total sales |
| preferred staff | OBSERVED absence | `evidence/customers/client-profile-tab-client-details.png` |  |
| preferred service | OBSERVED absence | `evidence/customers/client-profile-tab-client-details.png` |  |
| preferred branch | OBSERVED absence | `evidence/customers/client-profile-tab-client-details.png` |  |
| customer status | OBSERVED | `evidence/customers/client-action-block-client.png` | Blocked; Fresha verified filter |
| customer search | OBSERVED | `evidence/customers/global-search-03.png` |  |
| customer filters | OBSERVED | `research-log.md §11` | segments, group, blocked, verified, gender |
| customer segmentation | OBSERVED | `evidence/customers/client-segments-picker.png` | 11 built-in |
| customer account | OBSERVED | `evidence/booking/public-09-after-time-continue.png` | Fresha customer login to book |
| customer self-service | NOT VERIFIED | NOT VERIFIED | customer app not tested |
| customer communications | OBSERVED | `evidence/notifications/automations-01.png` |  |
| customer deletion/deactivation | OBSERVED (dialogs; not executed) | `evidence/customers/client-action-delete-client.png` |  |
| customer data export | OBSERVED | `evidence/import-export/client-export-sandbox_export_customer_list_2026-09-27.csv` | no visits/spend columns |

## §10 Payments (payments.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| checkout workflow | OBSERVED | `evidence/payments/checkout-02-cart-or-tip.png` | Cart → Tip → Payment |
| service payment | OBSERVED | `evidence/payments/checkout-07-complete.png` |  |
| product payment | OBSERVED | `evidence/walk-in/quick-sale-06-done.png` |  |
| service + product payment | OBSERVED | `evidence/walk-in/quick-sale-06-done.png` |  |
| payment methods | OBSERVED | `evidence/payments/checkout-03-payment.png` |  |
| partial payment | OBSERVED (Save part-paid option; not saved) | `evidence/payments/checkout-split-04-after-cash.png` |  |
| split payment | OBSERVED | `evidence/payments/checkout-split-06-both.png` |  |
| refunds | OBSERVED | `evidence/payments/refund-02.png` |  |
| discounts | OBSERVED | `evidence/payments/cart-discount-form.png` |  |
| tips | OBSERVED | `evidence/payments/checkout-02-cart-or-tip.png` |  |
| taxes | OBSERVED (settings) / NOT VERIFIED (calculation) | `evidence/settings/sales-tax-rates.png` | no tax configured |
| receipts | OBSERVED | `evidence/payments/receipt-sale-1.pdf` | '$' symbol, no barber name |
| payment status | OBSERVED | `evidence/payments/sale-5-voided.png` | Completed / Refunded / Voided; Fully paid |
| transaction history | OBSERVED | `evidence/audit/sale-activity.png` |  |
| sale records | OBSERVED | `evidence/payments/sales-list-01.png` |  |
| customer association | OBSERVED | `evidence/payments/sales-list-01.png` |  |
| barber association | OBSERVED | `evidence/walk-in/edit-sale-details.png` | per line; editable |
| branch association | OBSERVED | `evidence/payments/sales-list-01.png` | Location column |

## §11 Inventory (inventory.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| products | OBSERVED | `evidence/inventory/product-detail-01.png` |  |
| product categories | OBSERVED | `evidence/inventory/products-start-01.aria.txt` | category field; manage categories |
| stock | OBSERVED | `evidence/inventory/product-detail-01.png` |  |
| stock levels | OBSERVED | `evidence/inventory/product-detail-01.png` | per location |
| stock adjustments | OBSERVED | `evidence/inventory/remove-stock-02.aria.txt` |  |
| stock usage | OBSERVED | `evidence/inventory/remove-stock-02.aria.txt` | 'Internal use' manual |
| purchases | OBSERVED (flow entry) / NOT VERIFIED (no PO placed) | `evidence/inventory/stock-orders-01.png` |  |
| suppliers | OBSERVED | `evidence/inventory/supplier-add.aria.txt` |  |
| transfers | OBSERVED | `evidence/inventory/stock-transfer-T1-receive.png` | moves on receipt |
| branch-level stock | OBSERVED | `evidence/inventory/product-detail-01.png` |  |
| product sales | OBSERVED | `evidence/walk-in/quick-sale-03-cart.png` |  |
| low-stock alerts | OBSERVED (settings) / NOT VERIFIED (firing) | `evidence/inventory/product-add-filled.png` |  |
| inventory history | OBSERVED | `evidence/inventory/product-stock-history-after-transfer.png` |  |
| inventory reports | OBSERVED (catalogue) / NOT VERIFIED (contents) | `evidence/reports/reports-index-01.aria.txt` |  |
| stock counts | OBSERVED | `evidence/inventory/stocktake-04-review.png` |  |
| adjustment reasons | OBSERVED | `evidence/inventory/remove-stock-02.aria.txt` |  |

## §12 Finance (finance.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| revenue | OBSERVED | `evidence/finance/daily-sales-summary-01.png` |  |
| expenses | OBSERVED absence (FRESHA GAP) | `evidence/reports/reports-index-01.aria.txt` | only register cash-out |
| income | OBSERVED | `evidence/finance/daily-sales-summary-01.png` | payments collected by method |
| expense categories | OBSERVED absence | `evidence/finance/register-cash-out.png` | cash-out reasons only |
| branch expenses | OBSERVED absence | — |  |
| company-wide expenses | OBSERVED absence | — |  |
| payment reconciliation | OBSERVED | `evidence/finance/register-close-01.png` | expected vs counted |
| daily closing | OBSERVED | `evidence/finance/register-closed.png` | registers |
| profit/loss | OBSERVED absence (FRESHA GAP) | `evidence/reports/reports-index-01.aria.txt` |  |
| refunds | OBSERVED | `evidence/reports/payments-summary.png` |  |
| financial reports | OBSERVED | `evidence/reports/payments-summary.png` |  |
| approval workflows | OBSERVED absence | — | none except pay runs |
| attachments | OBSERVED | `evidence/finance/register-cash-out-2.png` | cash-out attachment |
| audit history | OBSERVED | `evidence/audit/sale-activity.png` |  |

## §13 Commission (commission.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| commission exists | OBSERVED | `evidence/commission/after-apply.png` |  |
| commission configuration | OBSERVED | `evidence/commission/setup-02-fixed.aria.txt` |  |
| percentage commission | OBSERVED | `evidence/payroll/pay-run-breakdown-aung.png` | 40% tested |
| fixed commission | OBSERVED (option; not configured) | `evidence/commission/setup-02-fixed.aria.txt` |  |
| service commission | OBSERVED | `evidence/payroll/pay-run-breakdown-aung.png` |  |
| product commission | OBSERVED | `evidence/payroll/pay-run-breakdown-after-product-sale.png` |  |
| staff-specific commission | OBSERVED | `evidence/commission/after-apply.png` |  |
| branch-specific commission | OBSERVED (option) / NOT VERIFIED (effect) | `evidence/commission/setup-03-advanced.aria.txt` |  |
| calculation timing | OBSERVED | `evidence/payroll/pay-run-breakdown-aung.png` | at checkout |
| completed vs paid behaviour | OBSERVED (partial) | `research-log.md §8` | checkout date; 'fully paid invoices' setting not toggled |
| refund reversal | OBSERVED | `evidence/payroll/pay-run-breakdown-after-refund.png` | void removes silently |
| commission reports | OBSERVED | `evidence/reports/commission-summary.png` |  |
| payroll integration | OBSERVED | `evidence/payroll/pay-run-breakdown-aung.png` |  |

## §14 Payroll (payroll.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| salary | OBSERVED (hourly only) | `evidence/staff/add-team-member-hourly-pay.aria.txt` | no salary type |
| payroll periods | OBSERVED | `evidence/staff/settings-team-pay-runs-edit.aria.txt` |  |
| commission | OBSERVED | `evidence/payroll/pay-run-breakdown-after-product-sale.png` |  |
| deductions | OBSERVED | `evidence/payroll/add-adjustment.png` | manual +/−; Fresha fee deductions |
| advances | OBSERVED | `evidence/staff/add-team-member-pay-runs.aria.txt` | cash-advance option; manual |
| loans | OBSERVED absence | — |  |
| attendance deductions | OBSERVED absence | — | wages follow timesheet hours |
| leave deductions | OBSERVED absence | — |  |
| payslips | NOT VERIFIED | NOT VERIFIED | no payslip document observed |
| payroll approval | OBSERVED | `evidence/payroll/pay-run-approved.png` | Needs review / Approved / Skip |
| payroll finalization | OBSERVED (code prompt) / NOT VERIFIED (final state) | `evidence/payroll/pay-run-verification-code-prompt.png` |  |
| payroll locking | NOT VERIFIED | NOT VERIFIED | blocked by verification code |
| payment status | OBSERVED (to pay / paid columns) / NOT VERIFIED (after completion) | `evidence/payroll/pay-run-step-2.png` |  |
| payroll reports | OBSERVED (catalogue) | `evidence/reports/reports-index-01.aria.txt` |  |
| branch allocation | OBSERVED | `evidence/payroll/pay-runs-start-01.png` | rows per member per location |

## §15 Schedule (schedule.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| weekly schedules | OBSERVED | `evidence/schedule/scheduled-shifts-01.png` |  |
| date-specific schedules | NOT VERIFIED | NOT VERIFIED | single-date edit not tested |
| temporary schedules | OBSERVED | `evidence/schedule/repeating-shifts-editor-01.aria.txt` | start / end dates on patterns |
| multiple segments per day | OBSERVED | `evidence/schedule/repeating-shifts-editor-01.aria.txt` | 'Add a shift' |
| multiple branches per day | OBSERVED | `evidence/schedule/roster-next-week-3210819.png` |  |
| staff availability | OBSERVED | `evidence/booking/new-appt-times-mon28-aung.png` |  |
| days off | OBSERVED | `evidence/schedule/scheduled-shifts-baber-shop.png` | 'Not working' days |
| holidays | OBSERVED (form) / NOT VERIFIED (effect) | `evidence/schedule/closed-period-form.png` | whole days |
| leave | OBSERVED | `evidence/leave/roster-with-time-off.png` |  |
| schedule conflicts | OBSERVED | `evidence/schedule/scheduled-shifts-baber-shop.png` | overlap allowed |
| booking availability calculation | OBSERVED | `evidence/booking/multi-service-02-times.png` |  |
| Mon 09-13 Branch A / 14-18 Branch B scenario | OBSERVED | `evidence/schedule/roster-next-week-3210802.png` | honoured by availability |

## §16 Leave (leave.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| leave creation | OBSERVED | `evidence/leave/add-time-off-filled.png` |  |
| leave types | OBSERVED | `evidence/staff/settings-team-time-off.png` |  |
| approval | OBSERVED (checkbox, not gating) | `evidence/leave/add-time-off-01.aria.txt` |  |
| half-day | OBSERVED | `evidence/leave/roster-with-time-off.png` |  |
| full-day | NOT VERIFIED | NOT VERIFIED | not executed |
| branch impact | NOT VERIFIED | NOT VERIFIED | multi-location member not tested |
| staff availability | OBSERVED | `evidence/leave/availability-with-time-off.png` |  |
| booking impact | OBSERVED | `evidence/leave/availability-with-time-off.png` | slots from 13:00 |
| payroll impact | OBSERVED absence | — | no leave link to pay |
| notifications | NOT VERIFIED | NOT VERIFIED |  |
| cancellation/editing | NOT VERIFIED | NOT VERIFIED |  |
| history | OBSERVED (report exists) / NOT VERIFIED (contents) | `evidence/reports/reports-index-01.aria.txt` | Team time off report |

## §17 Attendance (attendance.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| clock in | OBSERVED (manager) / NOT VERIFIED (self) | `evidence/attendance/timesheet-add-01.png` |  |
| clock out | OBSERVED (manager) / NOT VERIFIED (self) | `evidence/attendance/timesheet-add-01.png` |  |
| location verification | OBSERVED (setting) / NOT VERIFIED (behaviour) | `evidence/staff/settings-team-timesheets-edit.png` | 50 m |
| device verification | OBSERVED absence (FRESHA GAP) | `evidence/staff/settings-team-timesheets-edit.aria.txt` |  |
| branch identification | OBSERVED | `evidence/attendance/timesheet-detail.png` |  |
| QR | OBSERVED absence (FRESHA GAP) | `evidence/staff/settings-team-timesheets-edit.aria.txt` |  |
| corrections | OBSERVED | `evidence/attendance/timesheet-activity.png` | before/after, no reason |
| late | OBSERVED | `evidence/reports/attendance-summary.png` |  |
| early leave | OBSERVED | `evidence/reports/attendance-summary.png` | early clock-outs |
| absent | OBSERVED | `evidence/reports/attendance-summary.png` | missed shifts |
| incomplete attendance | NOT VERIFIED | NOT VERIFIED |  |
| automatic clock out | OBSERVED (setting) / NOT VERIFIED (behaviour) | `evidence/staff/settings-team-timesheets-edit.aria.txt` |  |
| attendance reports | OBSERVED | `evidence/reports/attendance-summary.png` |  |

## §18 Reports (reports.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| Booking report | OBSERVED | `evidence/booking/appointments-list-all-time.png` | catalogue + appointments list |
| Sales / Revenue report | OBSERVED | `evidence/reports/sales-summary.png` |  |
| Customer report | OBSERVED (catalogue) / NOT VERIFIED (contents) | `evidence/reports/reports-index-01.aria.txt` |  |
| Staff performance report | OBSERVED | `evidence/reports/commission-summary.png` |  |
| Branch report | OBSERVED absence | `evidence/reports/sales-summary-groupby.png` | Location filter / group-by instead |
| Inventory report | OBSERVED (catalogue) / NOT VERIFIED (contents) | `evidence/reports/reports-index-01.aria.txt` |  |
| Expense report | OBSERVED absence | `evidence/reports/reports-index-01.aria.txt` |  |
| Profit / Loss | OBSERVED absence | `evidence/reports/reports-index-01.aria.txt` |  |
| Payment report | OBSERVED | `evidence/reports/payments-summary.png` |  |
| Payroll report | OBSERVED (catalogue) / NOT VERIFIED (contents) | `evidence/reports/reports-index-01.aria.txt` |  |
| Daily closing | OBSERVED | `evidence/reports/cash-register-summary.png` | + Daily sales summary |
| per-report filters/date ranges/columns/metrics/grouping | OBSERVED | `evidence/reports/sales-summary-groupby.png` |  |
| branch/staff/service filtering | OBSERVED | `evidence/reports/sales-summary.aria.txt` |  |
| export formats | OBSERVED | `evidence/reports/sales-summary.png` | CSV / Excel / PDF |
| report permissions | OBSERVED | `evidence/roles/permission-matrix.md` |  |

## §19 Notifications (notifications.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| in-app notifications | OBSERVED | `evidence/notifications/bell-01.png` |  |
| booking notifications | OBSERVED | `evidence/notifications/automations-01.png` |  |
| cancellation notifications | OBSERVED | `evidence/notifications/messages-history-01.png` |  |
| reschedule notifications | OBSERVED | `evidence/notifications/messages-history-01.png` |  |
| staff notifications | OBSERVED (preferences) / NOT VERIFIED (delivery) | `evidence/notifications/notification-settings.png` |  |
| stock notifications | OBSERVED (preferences) / NOT VERIFIED (firing) | `evidence/notifications/notification-settings.png` |  |
| financial notifications | OBSERVED (preferences) | `evidence/notifications/notification-settings.png` | sales, tips |
| payroll notifications | OBSERVED absence | `evidence/notifications/notification-settings.aria.txt` | no category |
| security notifications | OBSERVED absence (in preferences) / NOT VERIFIED | `evidence/notifications/notification-settings.aria.txt` |  |
| notification history | OBSERVED | `evidence/notifications/bell-01.png` |  |
| read/unread | OBSERVED | `evidence/notifications/bell-01.png` | 'Read' state |
| retention | NOT VERIFIED | NOT VERIFIED |  |
| preferences | OBSERVED | `evidence/notifications/notification-settings.png` |  |

## §20 Roles / Permissions (roles-permissions.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| available roles | OBSERVED | `evidence/roles/permission-roles-list.png` |  |
| custom roles | OBSERVED (wizard; not saved) | `evidence/roles/add-permission-role.png` |  |
| permissions | OBSERVED | `evidence/roles/permission-matrix.md` |  |
| branch scope | OBSERVED | `evidence/roles/basic-role-workspace.aria.txt` |  |
| financial permissions | OBSERVED | `evidence/roles/basic-role-sales.aria.txt` |  |
| staff permissions | OBSERVED | `evidence/roles/basic-role-team.aria.txt` |  |
| booking permissions | OBSERVED | `evidence/roles/basic-role-calendar.aria.txt` |  |
| reporting permissions | OBSERVED | `evidence/roles/basic-role-reports.aria.txt` |  |
| inventory permissions | OBSERVED | `evidence/roles/basic-role-catalog.aria.txt` |  |
| payroll permissions | OBSERVED | `evidence/roles/basic-role-team.aria.txt` | 'Can run pay runs' |
| audit/log permissions | OBSERVED absence | `evidence/roles/permission-matrix.md` |  |

## §21 Audit (audit-log.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| booking changes | OBSERVED | `evidence/audit/appt-activity-02-status-changes.png` |  |
| cancellation | OBSERVED | `evidence/audit/appt-activity-cancelled.png` | reason not logged |
| reschedule | NOT VERIFIED | NOT VERIFIED | log not captured |
| customer changes | OBSERVED absence | `evidence/customers/client-profile-01.png` |  |
| staff changes | OBSERVED absence | — |  |
| finance changes | OBSERVED | `evidence/audit/sale-activity.png` |  |
| inventory changes | OBSERVED | `evidence/inventory/product-stock-history-after-transfer.png` |  |
| payroll changes | OBSERVED | `evidence/payroll/pay-run-breakdown-after-refund.png` |  |
| attendance corrections | OBSERVED | `evidence/attendance/timesheet-activity.png` |  |
| who changed what | OBSERVED | `evidence/attendance/timesheet-activity.png` |  |
| timestamps | OBSERVED | `evidence/audit/appt-activity-02-status-changes.png` |  |
| before/after information | OBSERVED (partial) | `evidence/attendance/timesheet-activity.png` | timesheets, stock-after; not appointments |
| reason fields | OBSERVED (partial) | `evidence/payments/refund-02.png` | refund & stock reasons; cancellation reason not logged |

## §22 Import / Export (import-export.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| customer import | OBSERVED (to preview) | `evidence/import-export/client-import-04-errors.png` |  |
| staff import | OBSERVED absence | — |  |
| service import | OBSERVED absence | — |  |
| product import | OBSERVED (step 1 + template) / NOT VERIFIED (run) | `evidence/import-export/product-import-01.png` |  |
| booking import | OBSERVED absence | — |  |
| finance import | OBSERVED absence | — |  |
| Excel | OBSERVED (export only; no Excel import) | `evidence/reports/sales-summary.png` |  |
| CSV | OBSERVED | `evidence/import-export/client-import-01.png` |  |
| PDF | OBSERVED (export) | `evidence/payments/receipt-sale-1.pdf` |  |
| templates | OBSERVED | `evidence/import-export/client-import-template_client_import_template.csv` |  |
| validation | OBSERVED | `evidence/import-export/client-import-04-errors.png` |  |
| duplicate handling | OBSERVED | `evidence/import-export/client-import-04-errors.png` | rejected |
| failed-row handling | OBSERVED | `research-log.md §11` | Download invalid rows |
| preview before import | OBSERVED | `evidence/import-export/client-import-04-errors.png` |  |

## §23 Settings (settings.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| company settings | OBSERVED | `evidence/settings/business-details-edit.png` |  |
| branch settings | OBSERVED | `evidence/branches/location-sales.png` |  |
| currency | OBSERVED (fixed SGD) + USER-PROVIDED (live MMK) | `evidence/settings/business-details-edit.png` |  |
| language | OBSERVED | `evidence/settings/language-picker.png` | no Burmese |
| date format | OBSERVED absence | `evidence/settings/date-time-settings-edit.aria.txt` |  |
| time format | OBSERVED | `evidence/settings/date-time-settings-edit.aria.txt` | 12 h / 24 h |
| booking settings | OBSERVED | `evidence/settings/scheduling-availability-edit-0.aria.txt` |  |
| cancellation settings | OBSERVED | `evidence/settings/scheduling-cancellation-reasons.png` |  |
| notification settings | OBSERVED | `evidence/notifications/notification-settings.png` |  |
| security settings | OBSERVED | `evidence/settings/personal-login.png` |  |
| data settings | OBSERVED absence | `evidence/_nav/settings-index.png` |  |
| integrations | OBSERVED | `evidence/booking/online-google-reserve.png` | add-ons page |
| maintenance/system settings | OBSERVED absence | `evidence/_nav/settings-index.png` |  |

## §24 UX (ux-analysis.md)

| Item | Status | Evidence | Note |
| --- | --- | --- | --- |
| start a booking | OBSERVED | `evidence/booking/slot-new-appt-01.png` |  |
| start a walk-in | OBSERVED | `evidence/walk-in/quick-sale-02-haircut.png` |  |
| complete a service | OBSERVED | `evidence/booking/same-day-checkout-appt-status.png` |  |
| checkout | OBSERVED | `evidence/payments/checkout-03-payment.png` |  |
| reschedule | OBSERVED | `evidence/booking/reschedule-01.png` |  |
| cancel | OBSERVED | `evidence/booking/cancel-modal.png` |  |
| find customer | OBSERVED | `evidence/customers/global-search-03.png` |  |
| record service | OBSERVED | `evidence/audit/appt-activity-02-status-changes.png` |  |
| receive stock | OBSERVED | `evidence/inventory/stock-transfer-T1-receive.png` |  |
| transfer stock | OBSERVED | `evidence/inventory/stock-transfer-05.png` |  |
| mobile usability | OBSERVED (responsive web) / NOT VERIFIED (app) | `evidence/ux/mobile-390-calendar.png` |  |
| tablet usability | OBSERVED (responsive web) / NOT VERIFIED (app) | `evidence/ux/tablet-820-calendar.png` |  |
| desktop usability | OBSERVED | `ux-analysis.md` |  |
