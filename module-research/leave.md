# Leave / Time off: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Time off added for **Min Test Barber**: Annual leave,
> Mon 28 Sep 09:00–13:00, **"Approved" left unchecked**, description "ZZTest half-day leave". See `test-data-log.md` row 27.

## Navigation

- `Team → Scheduled shifts → Add → Time off` (also Team member Actions → Add time off); `Settings → Team → Time off types`.

## OBSERVED

### Time off types

- Annual leave, Sick leave, Training, Other absence reasons; **Add** custom types. Evidence: `evidence/staff/settings-team-time-off.png`

### Create time off (performed)

- Fields: **Team member** (list limited to members of the current roster location: Min, Aung at Branch B), **Type**, **Start date**
  (date picker), **Start time**, **End time** (5-min steps, so **partial / half days** are possible), **Repeat** checkbox, **Description**
  (≤100), **"Approved" checkbox (unchecked by default)**, note "**Online bookings cannot be placed during time off.**" → Save → "Time off
  added". Evidence: `evidence/leave/add-time-off-01.png`, `evidence/leave/add-time-off-01.aria.txt`, `evidence/leave/add-time-off-filled.png`
- Clicks: Add → Time off → member → type → date (picker) → start → end → Save ≈ 8 + typing.

### Impact

- **Roster:** Min's Monday showed "Annual leave 09:00 – 13:00" and a remaining shift "13:00 – 19:00". His weekly total dropped from 59 h to
  55 h (Branch B view). Evidence: `evidence/leave/roster-with-time-off.png`
- **Availability:** with the leave **unapproved**, Branch B Monday slots started at **13:00** for both "Any team member" and Min. So **the
  Approved flag didn't gate the blocking effect**. Evidence: `evidence/leave/availability-with-time-off.png`
- **Branch impact:** time off was created from the Branch B roster. Whether it also blocks the member's other locations wasn't tested
  (Min works only at Branch B).
- **Reports:** "Team time off report — Detailed view of team time off" exists in the catalogue. Evidence: `evidence/reports/reports-index-01.aria.txt`

## USER-PROVIDED

- None beyond the brief's research questions (§16).

## INFERRED

- The "Approved" checkbox looks like a record-keeping flag rather than a workflow gate, because unapproved leave already blocked bookings.

## NOT VERIFIED

- **Leave requests by barbers** (e.g. from the Fresha mobile app) and any approval notification (no barber login).
- Full-day leave spanning several days; editing / cancelling time off; leave history per member.
- **Payroll impact:** none observed. Wages depend on timesheet hours, not on leave records.
- Effect on a multi-location member's other branch.

## Notes for the gap analysis

- Half-day leave works through time ranges. There's no approval workflow gating availability, which is a potential owner decision
  (who approves leave, and whether pending leave blocks bookings).
