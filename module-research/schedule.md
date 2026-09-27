# Schedule / Availability: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27, two locations (Baber Shop = Yangon address,
> opening Mon–Fri 10–19, Sat 10–17, Sun closed; **Branch B** = Mon 09–19, Tue–Fri 10–19, Sat 10–17, Sun 10–16).
> See `test-data-log.md` rows 1, 4, 27.

## Navigation

- `Team → Scheduled shifts` (roster, `/team/scheduled-shifts`), per-member `Edit → Set repeating shifts`, `Add → Time off / New team
  member / Business closed period`; `Settings → Scheduling` (closed periods, availability, booking options); location opening hours.

## OBSERVED

### Roster (scheduled shifts)

- Weekly roster **per location** (location picker), Previous / This / Next week, per-day totals, per-member weekly totals **for that
  location only**. Note on page: "The team roster shows your availability for bookings and is not linked to your business standard opening
  hours." Evidence: `evidence/schedule/scheduled-shifts-01.png`, `evidence/schedule/scheduled-shifts-baber-shop.png`
- Per-member **Edit** menu: Schedule → **Set repeating shifts**, **Unassign from location**, Delete all shifts; Team member → View / Edit.
  **Add** menu: Time off, New team member, **Business closed period**. Options: Scheduling settings. (Text capture, `research-log.md` §6.)
- **Default shifts:** when a member was assigned to a location, Fresha created repeating shifts **equal to that location's opening hours**.
- **Multi-location member:** Aung (both locations) received default shifts at **both** locations on the **same days and times** (e.g. Tue
  10:00–19:00 at each). These overlapping shifts were **saved without any warning**. Evidence: `evidence/schedule/scheduled-shifts-baber-shop.png`,
  `evidence/schedule/scheduled-shifts-01.png`

### Repeating shift editor

- Header shows the location; **Schedule type: Every week / Every 2 weeks / Every 3 weeks / Every 4 weeks**; **Start date**; **Ends: Never /
  Specific date**; per weekday checkbox + start–end (5-min steps); **"Add a shift"** (several segments per day) / "Remove shift"; "Team
  members will not be scheduled on business closed periods." "Changes saved will apply to all upcoming shifts for the selected period."
  Evidence: `evidence/schedule/repeating-shifts-editor-01.png`, `evidence/schedule/repeating-shifts-editor-01.aria.txt`

### Brief scenario: Monday 09:00–13:00 Branch A, 14:00–18:00 Branch B (performed)

1. Baber Shop (A): Aung → Set repeating shifts → Monday 09:00–13:00, Ends Never → Save ("Working hours set").
   Evidence: `evidence/schedule/repeating-shifts-aung-baber-monday.png`
2. Branch B: Aung → Set repeating shifts → Monday 14:00–18:00 → Save.
3. Roster week of 28 Sep: Baber Shop Mon **09:00–13:00**; Branch B Mon **14:00–18:00**.
   Evidence: `evidence/schedule/roster-next-week-3210802.png`, `evidence/schedule/roster-next-week-3210819.png`
4. Booking availability honoured it: Branch B, Mon 28, Aung → **14:00–17:15** only (45-min service); "Any team member" at Branch B →
   09:00–18:15 (Min covers the morning). Evidence: `evidence/booking/new-appt-times-mon28-aung.png`, `evidence/booking/new-appt-times-mon28-any.png`

### Date-specific, temporary, days off, holidays

- Repeating patterns with start / end dates provide temporary schedules. The Edit menu offers "Delete all shifts". Single-day edits
  were **not** tested.
- **Business closed period:** Start date, End date (**whole days**), Description (e.g. Public Holiday), Locations (All / specific). "Online
  bookings cannot be placed when your business is closed." Evidence: `evidence/schedule/closed-period-form.png`
- **Time off** (see `leave.md`): partial-day time ranges appear on the roster ("Annual leave 09:00–13:00") and reduce the weekly hours.
  Evidence: `evidence/leave/roster-with-time-off.png`

### Availability calculation (summary of observed inputs)

`location + member "Works at" + member shifts at that location − time off − closed periods − member's existing bookings at ANY location
− blocked time + service duration (location / member override) + slot interval (15 min) + booking-window & lead-time rules (online)`
Each term was observed to affect the offered times (tests in `booking.md`). Blocked time and closed periods weren't tested for their effect.

### Conflicts

- Shift conflicts across locations are **not prevented** (overlapping shifts saved).
- Booking conflicts are **soft-warned** for staff ("Team member is not available"; "isn't scheduled to work at this time") and can be
  overridden (see `booking.md`).

## USER-PROVIDED

- Barbers may work at several branches; the brief asks specifically about the Monday split scenario (brief §15).

## INFERRED

- Because the roster is per location, the per-member weekly total shown doesn't add hours across branches (Aung showed 47 h at
  Baber Shop and 53 h at Branch B for the same week).

## NOT VERIFIED

- Editing a single date without changing the repeating pattern.
- Effect of blocked time and closed periods on availability (forms observed, not tested for effect).
- Behaviour when a shift crosses midnight.

## Notes for the gap analysis

- Fresha supports split multi-branch days, but **also accepts overlapping cross-branch shifts**, which the planned system may want to validate.
