# Attendance / Time tracking: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Timesheets are part of "Wages and timesheets", enabled
> only for **Aung Test Barber**. One manual timesheet was added by the owner, then edited. See `test-data-log.md` rows 25–26.

## Navigation

- `Team → Timesheets` (`/team/timesheets`); `Settings → Team → Timesheets`; team member form → Wages and timesheets → Timesheet settings;
  reports Attendance summary, Working hours activity / summary, Break activity.

## OBSERVED

| Topic | Fresha behaviour | Evidence |
| --- | --- | --- |
| Clock in / out (manager, web) | `Timesheets → Add → Select team member` ("**Expected today**: Aung 10:00–16:00 Branch B") → form with date + location from the shift, **Clock in** (pre-filled 10:00), **Add break**, **Clock out** (16:00), Hours worked, Total paid hours → Save → list row "Clocked out" | `evidence/attendance/timesheet-add-01.png`, `evidence/attendance/timesheets-02-after-add.png` |
| Clock in / out (barber self-service) | **No self clock-in control was found in the web partner app** during this session | NOT VERIFIED (mobile app) |
| Location verification | Workspace: "**Enable location check** — Allow team members to only clock in within the configured distance of the location". Per member: "Prevent manual timesheet entries when more than **50m** away" (workspace default / enabled / disabled) | `evidence/staff/settings-team-timesheets-edit.png`, `evidence/staff/add-team-member-wages-enabled.aria.txt` |
| Device verification | **OBSERVED absence:** no device-binding setting found | `evidence/staff/settings-team-timesheets-edit.aria.txt` |
| Branch identification | Each timesheet carries the location of the shift (Branch B) | `evidence/attendance/timesheet-detail.png` |
| QR attendance | **OBSERVED absence:** no QR clock-in option in timesheet settings, member settings or navigation → **FRESHA GAP** (vs planned QR + location) | same |
| Automation | Auto clock in at shift start, auto clock out at shift end, automated scheduled breaks (workspace or per member) | `evidence/staff/settings-team-timesheets-edit.aria.txt` |
| Late / early / absent | Timesheet detail shows **Expected vs actual** (e.g. "Clocked in — Expected 10:00 — 10:00"). **Attendance summary** report columns: Scheduled shifts, On time / **Early / Late** clock ins, On time / Early / Late clock outs, **Punctuality**, **Missed shifts**, **Attendance %** | `evidence/attendance/timesheet-detail.png`, `evidence/reports/attendance-summary.png` |
| Corrections | Timesheet Actions: **Edit**, **Delete timesheet**. The Activity tab logs "Naing Aung edited this timesheet — **Clock-in time edited from 10:00 to 10:10**" with date/time, plus creation lines ("Clock-in time of 10:00 added"). **No reason field** was observed for edits | `evidence/attendance/timesheet-activity.png` |
| Incomplete attendance | Status column exists ("Clocked out"). The state of a shift with clock-in but no clock-out wasn't produced | NOT VERIFIED |
| Reports | Attendance summary, Working hours activity ("worked hours, shifts, and timesheets"), Working hours summary, Break activity; export CSV / Excel / PDF | `evidence/reports/attendance-summary.png`, `evidence/reports/reports-index-01.aria.txt` |
| Payroll link | Timesheet hours drive hourly wages in pay runs (6 h × SGD 5 = SGD 30) | `research-log.md` §14 |

## USER-PROVIDED

- Planned: **QR + location attendance** (brief §26).

## INFERRED

- Barber self clock-in (and the 50 m proximity check) presumably happens in the Fresha mobile app, because the web app offered only
  manager-entered timesheets.

## NOT VERIFIED

- Barber self clock-in via the Fresha app; the proximity check actually rejecting a clock-in; auto clock-out behaviour.
- The Attendance summary's figures for the test timesheet: the report was generated from data ~28 minutes old and showed 1 missed shift
  and 0% attendance for Aung. Whether that reflects the later-added timesheet is NOT VERIFIED.

## FRESHA GAP

- **QR-based attendance: not found.** Device verification: not found. Location verification exists as a distance check (50 m), per workspace or member.
