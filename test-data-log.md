# Test Data Log (Fresha research sandbox workspace "Baber Shop")

**Workspace:** `Baber Shop` — a Fresha *trial* workspace (Singapore / SGD, trial ending ~2026-10-04) that the user created as a research
sandbox (USER-PROVIDED, 2026-09-27). It is **not** the barbershop's live account (the live account is set to Myanmar / MMK — USER-PROVIDED).

**Authorisation (USER-PROVIDED, 2026-09-27):** "test as much as you can" — any change inside this sandbox is allowed, including test
checkouts, locations, team members, settings, commissions and pay runs.

**Self-imposed rules:** no SMS / email / push to real people (test clients and test team members carry no real contact details;
client notifications off where a toggle exists), no billing / bank / card details entered, no marketing sends, every created or changed
record is logged below so it can be reviewed or removed.

| # | Time (local) | Record created / changed | Where | Purpose | Cleaned up? |
| - | ------------ | ------------------------ | ----- | ------- | ----------- |
| 1 | 2026-09-27 ~07:10 | Location created: public name "Baber Shop Branch B (Test)", internal "Branch B", address Orchard Boulevard, Singapore (autocomplete is limited to workspace country), phone +65 9123 4567 (placeholder; SG mobile format enforced), email = owner email, hours Mon 09:00-19:00, Tue-Fri 10-19, Sat 10-17, Sun 10-16 | Settings > Business setup > Locations > Add | Multi-branch tests | Keep until research done |
| 2 | 2026-09-27 ~07:25 | Team member "Aung Test Barber" (aung.testbarber@example.com, non-deliverable), role Basic, works at Baber Shop + Branch B, services Haircut + Blow Dry, wages Hourly SGD 5, pay runs on (defaults) — list shows "Pending invitation" | Team > Team members > Add | Multi-branch barber tests | Keep until research done |
| 3 | 2026-09-27 ~07:30 | Team member "Min Test Barber" (min.testbarber@example.com), role Basic, works at Branch B only, service Haircut only, no wages | Team > Team members > Add | Single-branch barber tests | Keep until research done |
| 4 | 2026-09-27 ~07:45 | Repeating shifts for Aung from 2026-09-28 (Ends: Never): Baber Shop Mon 09:00-13:00 (Tue-Fri 10-19, Sat 10-17 unchanged); Branch B Mon 14:00-18:00 (Tue-Fri 10-19, Sat 10-17, Sun 10-16 unchanged — overlapping with Baber Shop, saved without warning) | Team > Scheduled shifts > Edit > Set repeating shifts | Monday split-branch scenario + cross-branch overlap test | Keep until research done |
| 5 | 2026-09-27 ~07:55 | Client "ZZTest Client A" (zztest.clienta@example.com, no phone; notification toggles left at defaults) | Calendar > Add > Appointment > Add client > Add new client | Booking tests | Keep until research done |
| 6 | 2026-09-27 ~08:00 | Appointment: ZZTest Client A, Haircut 45m, Aung, Branch B, Mon 2026-09-28 14:00 (flow: Add > Appointment > View available times) | Calendar | Booking flow / split-shift availability | To cancel/complete during tests |
| 7 | 2026-09-27 ~08:10 | Appointment: ZZTest Client A, Haircut 45m, Aung, Branch B, Tue 2026-09-29 10:00 (flow: click slot in Aung column > Add appointment) — 2nd active booking for same client, no warning | Calendar | Staff-first flow; cross-branch double-booking test | To cancel during tests |
| 8 | 2026-09-27 ~08:20 | Appointment: Walk-in (no client), Haircut 45m, Aung, **Baber Shop**, Tue 2026-09-29 10:15 — overlaps Aung Branch B booking 10:00-10:45; drawer showed inline "Team member is not available", Save still succeeded | Calendar | Cross-branch double-booking test | To cancel during tests |
| 9 | 2026-09-27 ~08:30 | Custom checkout method "KBZPay" added (only field: Name) | Settings > Sales > Custom checkout methods > Add | Cash + KBZPay checkout tests | Keep until research done |
| 10 | 2026-09-27 15:59 SGT | Sale #1 (Baber Shop) completed from walk-in appointment #8: Haircut SGD 40 + tip SGD 4 (to Aung); split payment Cash SGD 20 (received by Aung) + KBZPay SGD 24 | Calendar > appointment > Checkout | Checkout / split payment / tips | Refund/void test pending |
| 11 | 2026-09-27 ~16:05 SGT | Commission plan for Aung: Fixed rate 40% on all services + all products, every day, all locations, effective 2026-09-27, workspace default rules | Team > Aung > Edit > Commissions > Set up now | Commission calc / pay run tests | Keep until research done |
| 12 | 2026-09-27 16:07 SGT | Refund #2 against Sale #1: Haircut SGD 40 refunded (Cash SGD 20 + KBZPay SGD 20), tip not refunded, reason "Client's request" | Sales > Sales list > Sale #1 > Refund sale | Refund + commission reversal test | Done |
| 13 | 2026-09-27 ~16:20 SGT | Appointment #D7C048A9 rescheduled Mon 28 14:00 → Mon 28 15:15 (Branch B, Aung; slot click snapped to 15:15) via Options > Reschedule; "Notify client" left ON (example.com) | Calendar | Reschedule flow | — |
| 14 | 2026-09-27 ~16:25 SGT | Appointment #867B2E43 (Tue 29 10:00 Branch B, Client A) cancelled, reason "Client not available", cancellation notification left ON (example.com); no fee (no policy) | Appointments list > appointment > Options > Cancel | Cancellation flow | — |
| 15 | 2026-09-27 ~16:28 SGT | Demo appointment #53B52046 (John Doe, 27 Sep 09:00, Baber Shop) marked No-show (notification default ON → john@example.com) | Appointments list > Options > No-show | No-show flow | — |
| 16 | 2026-09-27 ~16:40 SGT | Client "ZZTest Duplicate Email" created with SAME email as ZZTest Client A (inline duplicate warning shown, save allowed) | Clients > Add | Duplicate detection test | To merge/delete |
| 17 | 2026-09-27 ~16:43 SGT | Merged duplicates (Clients > Options > Merge clients): survivor profile = "ZZTest Duplicate Email" (newer); "ZZTest Client A" name no longer listed | Clients | Merge behaviour | Done (irreversible) |
| 18 | 2026-09-27 ~16:55 SGT | Product "ZZTest Pomade" 100 g, supply SGD 5, retail SGD 15 (markup 200%), commission on, stock Branch B 10 / Baber Shop 20, low-stock level 3 + reorder 10 per location, low-stock notifications on | Catalog > Products > Start now / Add | Inventory tests | Keep until research done |
| 19 | 2026-09-27 ~16:41-16:44 SGT | ZZTest Pomade stock ops: Branch B −1 "Internal use"; Branch B +2 reason "Transfer"; Baber Shop −2 reason "Other" + description "Transfer to Branch B (test)" (manual adjustments; NOTE: a native transfer feature exists under Catalog > Stock orders > Add new transfer — see row 21) → Branch B 11 / Baber Shop 18 | Product > Actions > Add/Remove stock | Stock adjustment & manual transfer test | — |
| 20 | 2026-09-27 16:46 SGT | Supplier "ZZTest Supplier" (name only) | Catalog > Suppliers > Add | Stock order test | Keep until research done |
| 21 | 2026-09-27 16:48 SGT | Stock transfer T1: 3 × ZZTest Pomade, Baber Shop → Branch B, status Ordered | Catalog > Stock orders > Add > Add new transfer | Native transfer test | Receive pending |
| 22 | 2026-09-27 ~16:50 SGT | Transfer T1 partially received: 2 of 3 received at Branch B ("Mark order as partially received") | Stock orders > T1 > Actions > Receive stock | Partial receipt test | 1 unit outstanding |
| 23 | 2026-09-27 16:52 SGT | Stocktake "ZZTest count Baber Shop": Pomade expected 16, counted 15 (−1, −SGD 5), completed | Catalog > Stocktakes > Start now | Stock count test | Done (irreversible) |
| 24 | 2026-09-27 16:55 SGT | Sale #3 (Baber Shop, Walk-In quick sale via Calendar > Add > Sale): Haircut (Aung) SGD 40 + ZZTest Pomade (Aung) SGD 15, Cash SGD 55 | Calendar > Add > Sale | Service+product sale, product commission, stock deduction | — |
| 25 | 2026-09-27 ~17:00 SGT | Timesheet for Aung, Sun 27 Sep, Branch B, 10:00–16:00 (manual entry by owner) | Team > Timesheets > Add | Attendance→wages test | — |
| 26 | 2026-09-27 17:01 SGT | Timesheet edited: Aung clock-in 10:00 → 10:10 | Timesheets > entry > Actions > Edit | Attendance correction audit | — |
| 27 | 2026-09-27 ~17:05 SGT | Time off: Min, Annual leave, Mon 2026-09-28 09:00–13:00, "Approved" unchecked, description "ZZTest half-day leave" | Team > Scheduled shifts > Add > Time off | Leave → availability test | — |
| 28 | 2026-09-27 ~17:10 SGT | Cash register "ZZTest Register B" created at Branch B (default: "Require register to be opened to start taking sales" = ON) | Sales > Register > Start now | Daily closing test | Keep until research done |
| 29 | 2026-09-27 17:11 SGT | Register "ZZTest Register B" opened with float SGD 50 (note "ZZTest float") | Sales > Register > Open register | Daily closing test | To close |
| 30 | 2026-09-27 17:12 SGT | Register cash out SGD 5, reason "Petty cash for purchases", note "ZZTest petty cash - towels" | Sales > Register > Cash out | Petty cash / expense test | — |
| 31 | 2026-09-27 17:13 SGT | Register "ZZTest Register B" closed: cash expected 45, counted 44 (diff −1), closing float 40, cash to bank 4, note "ZZTest close: 1 short" | Sales > Register > View > Close register | Daily closing test | Done |
| 32 | 2026-09-27 ~17:18 SGT | Haircut advanced pricing: Branch B = 50 min / SGD 45; Aung @ Branch B = SGD 50 (duration inherits 50); Baber Shop unchanged (45 min / SGD 40); "update already-scheduled appointments" left at default | Catalog > Service menu > Haircut > Options > Advanced pricing and duration | Branch+Barber price/duration test | Keep until research done |
| 33 | 2026-09-27 17:55 SGT | Sale #4 (Baber Shop): checkout of demo appointment Jane Doe 27 Sep 11:00 (Hair Color SGD 57, Naing) paid by KBZPay (single tap = full amount) | Appointments list > appointment > Checkout | Same-day checkout completion test | — |
| 34 | 2026-09-27 ~18:00 SGT | Appointment (walk-in, Branch B, Tue 29 Sep): Haircut 10:15 Min (50m, SGD 45) + Blow Dry 11:05 Aung (35m, SGD 35), total 1h25 SGD 80 | Calendar > Add > Appointment > View available times | Multi-service / multi-barber test | To cancel |
| 35 | 2026-09-27 18:01 SGT | Sale #5 (Baber Shop, walk-in quick sale): Haircut (Aung) 40 + Pomade (Aung) 15, cart discount 10% (−5.50) → 49.50 KBZPay | Calendar > Add > Sale | Discount→commission, then void test | To void |
| 36 | 2026-09-27 ~18:05 SGT | Sale #5 VOIDED (modal: payments deleted, 1 Pomade returned to Baber Shop; no reason field) | Sales > sale > Open options > Void sale | Void vs refund test | Done (irreversible) |
| 37 | 2026-09-27 ~18:12 SGT | Demo team member "Wendy Smith (Demo)" ARCHIVED (restorable) | Team > Team members > Actions > Archive | Deactivation behaviour | Restore if needed |

## State left in the sandbox (end of research, 2026-09-27)

No clean-up was performed: the workspace is the user's own test sandbox and the records are the evidence. To reset, remove or reverse:

| Still present | How to remove / reverse |
| --- | --- |
| Location "Branch B" | Settings → Business setup → Locations → Branch B → Options → Delete location |
| Team members "Aung Test Barber", "Min Test Barber" (pending invitations to @example.com), Aung's hourly wage + 40% commission plan | Team → Team members → Actions → Archive |
| "Wendy Smith (Demo)" **archived** | Team → Team members → Filters (archived) → restore if wanted |
| Repeating shifts for Aung (Mon split) and Min's time off (Mon 28 Sep 09–13) | Team → Scheduled shifts |
| Client "ZZTest Duplicate Email" (merged with "ZZTest Client A"; **merge irreversible**) | Clients → profile → Actions → Delete client |
| Appointments: Aung Mon 28 Sep 15:15 (Branch B, booked); cancelled Tue 29 10:00; completed walk-in Tue 29 10:15; multi-service walk-in Tue 29 10:15 (Min + Aung, booked); demo John Doe no-show; demo Jane Doe completed | Calendar / Sales → Appointments (cancel remaining future ones) |
| Sales #1 (refunded by Refund #2), #3, #4, #5 (**voided**) | Sales cannot be deleted; refunds / voids are the reversal mechanism |
| Custom payment method "KBZPay" | Settings → Sales → Custom checkout methods |
| Product "ZZTest Pomade", supplier "ZZTest Supplier", transfer T1 (**partially received**, 1 outstanding), stocktake (**completed, irreversible**) | Catalog → Products / Suppliers / Stock orders (cancel T1) |
| Register "ZZTest Register B" (closed), cash-out record | Settings → Sales → Registers |
| Haircut advanced pricing (Branch B 50 min / SGD 45; Aung @ Branch B SGD 50) | Catalog → Service menu → Haircut → Options → Advanced pricing and duration → Reset all |
| Timesheet for Aung (27 Sep, Branch B) | Team → Timesheets → Actions → Delete timesheet |
| Unfinished pay run (left without completing; verification code not entered) | Team → Pay runs |

Nothing was published to the Fresha marketplace and no billing or bank details were entered. Messages: automated client emails went to
`@example.com` (status "Error"), team invitations went to `@example.com`, and pressing "Complete" on the pay run caused Fresha to email a
4-digit verification code to the **owner's own address** (the code was not requested or used). Any Fresha system emails to the owner (e.g.
about the new location) were not checked.
