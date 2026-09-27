# Staff / Employees / Barbers: Fresha research

> **Environment.** Sandbox workspace "Baber Shop" (trial, Singapore/SGD), observed 2026-09-27. Test barbers created:
> **Aung Test Barber** (works at Baber Shop + Branch B, Haircut + Blow Dry, Basic role, hourly SGD 5, 40% commission) and
> **Min Test Barber** (Branch B only, Haircut only, Basic role). See `test-data-log.md` rows 2–3.

## Navigation

- `Team → Team members` (`/team/team-members`), `Team → Scheduled shifts`, `Team → Timesheets`, `Team → Pay runs`
- `Settings → Team` (`/setup/team/...`): Permission roles, Time off types, Timesheets, Shifts, Pay runs, Commissions, PIN switching

## OBSERVED

### Team member list

- Columns: Name, Contact (email, phone), Permission role; status text **"Pending invitation"** under new members.
  Evidence: `evidence/staff/team-list-after-add.png`
- Filters: Locations, Type, Status. Sort: Custom order. Evidence: `Team → Team members → Filters` drawer (text capture, `research-log.md` §5); list screenshot `evidence/staff/team-members-list.png`
- List **Options**: Create share link, Change order, Team settings, **Export → CSV / Excel**; no import option.
  Evidence: `Team → Team members → Options` menu (text capture, `research-log.md` §5 and §17)
- Row **Actions**: Edit, Edit permission role, View calendar, View scheduled shifts, Add time off, **Archive**,
  Resend email invitation. (Observed via the Actions menu; see `research-log.md` §5.)
- Trial banner: "Activate your plan to ensure uninterrupted access after your free trial ends in 7 days".

### Add / edit team member form (performed twice)

| Section | Fields | Evidence |
| --- | --- | --- |
| Profile | First name*, Last name, **Email\*** (required), Phone, Additional phone, Country, Birthday, Gender, Pronouns, Calendar colour (17 colours), Job title ("Visible to clients online") | `evidence/staff/add-team-member-profile.aria.txt` |
| Work details | Start date, End date, **Employment type** (Employee / Self-employed), **Team member ID** ("An identifier used for external systems like payroll"), Notes (≤1000, private) | same |
| Addresses / Emergency contacts | "Add an address", "Add an emergency contact" | `evidence/staff/add-team-member-addresses.aria.txt`, `evidence/staff/add-team-member-emergency-contacts.aria.txt` |
| Services | All services / by category / individual services (service eligibility) | `evidence/staff/add-team-member-services.aria.txt` |
| Locations ("Works at") | All locations or specific; "At least one location must be selected." | `evidence/staff/add-team-member-locations.aria.txt` |
| Settings | Calendar bookings on/off ("appear on the calendar and receive appointments"); Advanced: **Exclude team member from online bookings**, **Team member excluded from auto assignment** (never auto-selected for "Any professional"); **Permission role** (default **Medium**) | `evidence/staff/add-team-member-settings.aria.txt`, `evidence/staff/add-team-member-settings-advanced.aria.txt` |
| Wages and timesheets | Off by default. When on: Compensation type **None / Hourly pay** (no salary option), Hourly rate, Overtime pay toggle; timesheet settings: proximity "Prevent manual timesheet entries when more than 50m away" (workspace default / enabled / disabled), Auto clock in, Auto clock out, Automated breaks | `evidence/staff/add-team-member-wages-and-timesheets.aria.txt`, `evidence/staff/add-team-member-wages-enabled.aria.txt`, `evidence/staff/add-team-member-hourly-pay.aria.txt` |
| Commissions | "Set up flexible commissions… percentage or fixed-rate… by day, location, or item… how discounts and taxes affect earnings" → wizard (see `commission.md`) | `evidence/staff/add-team-member-commissions.aria.txt` |
| Pay runs | On by default; preferred payment method (Pay manually = "Mark as paid outside of Fresha" / transfer); Automatic calculation; deductions (Fresha payment processing fees, Fresha new client fees); **Cash advances**: "Record cash payments for sales as 'paid' in pay runs" | `evidence/staff/add-team-member-pay-runs.aria.txt` |

- Saving a member with a role and an email → list status **"Pending invitation"** (the invites went to non-deliverable
  `@example.com` addresses). Evidence: `evidence/staff/team-list-after-add.png`
- Adding a member to a location **auto-creates repeating shifts equal to that location's opening hours** (see `schedule.md`).

### Deactivation (performed on the demo member "Wendy Smith (Demo)")

- `Actions → Archive` → modal: "Are you sure you want to archive this team member? Archived team members may be viewed by
  adjusting your filter settings, and may be restored at any time." → Confirm → "Team member archived".
  Evidence: `evidence/staff/archive-modal.png`
- The archived member's **existing appointment stayed "Booked" and assigned to her**, now showing "Team member is not
  available". The modal didn't mention future appointments. Evidence: `evidence/staff/archived-member-appointment.png`

### Team settings (workspace level)

| Setting | Observed values | Evidence |
| --- | --- | --- |
| Time off types | Annual leave, Sick leave, Training, Other absence reasons; Add custom | `evidence/staff/settings-team-time-off.png` |
| Timesheets | Location check (off), auto clock in/out (off), auto breaks (off); "can be customized individually per team member" | `evidence/staff/settings-team-timesheets-edit.aria.txt` |
| Pay runs | Frequency Daily / Weekly / Every 2 weeks / Every 4 weeks / Semi-monthly / Monthly / Quarterly; restarts on (weekday); starts from next cycle / custom date; automatic payouts of wages, commissions, other and tips (disabled) | `evidence/staff/settings-team-pay-runs-edit.aria.txt` |
| Commissions (defaults) | Deduct discounts / taxes / service cost / product cost; commission on package- and membership-paid services; full commission on loyalty redemption; **earn commissions only on fully paid invoices**; allow commission above amount paid | `evidence/staff/settings-team-comissions.png` |
| PIN switching | Off; "Quickly switch between users, without the need for emails and passwords" | `evidence/staff/settings-team-pin-switching.png` |

### Staff performance and reporting (OBSERVED in the report catalogue; see `reports.md`)

- Reports that cover team members: Commission activity / summary, Tips summary / detail, Wages detail / summary, Pay summary,
  Working hours activity / summary, Attendance summary, Break activity, Scheduled shifts, Team time off, and Performance
  summary / over time (Premium). The dashboard has a "Top team member" widget.
- Performance insights button in the top bar (not opened).

## USER-PROVIDED

- 15+ barbers, some working at several branches (brief §2). Planned: passwordless staff login (Google SSO or Email OTP), no SMS OTP (brief §26).
- No barber login or first-hand pain points were supplied during the session.

## INFERRED

- The member activates a login by accepting the emailed invitation (implied by "Pending invitation" and "Resend email invitation"; not completed).
- A barber can only log in after accepting the email invitation, so an email address is mandatory for every staff
  record, even staff who never log in.

## NOT VERIFIED

- The barber's own view (what a Basic-role barber sees after login, including the mobile app): no barber email was provided.
- Invitation acceptance / account activation flow (invite emails went to `@example.com`).
- Whether an archived member can still log in, and what "restore" does to their shifts.
- Staff performance screens beyond report names (Performance insights drawer not opened).
- Staff notifications received on the barber's own device (see `notifications.md`).

## Notes for the gap analysis

- Email is mandatory for staff in Fresha. Our plan's passwordless login also needs an email for Google SSO / Email OTP (consistent).
- Compensation is **hourly only** (no monthly salary type observed).
- Archiving doesn't handle future bookings.
- Multi-location members get overlapping default shifts (see `schedule.md`).
