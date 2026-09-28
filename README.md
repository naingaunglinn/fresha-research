# Fresha Research & Gap Analysis

Factual research on the **Fresha partner web app**, carried out to inform the specification of a replacement barbershop management system
(3 branches, 15+ barbers, Myanmar, MMK, Myanmar + English UI). **This is research only**: no application code, no schema, no architecture.

- **Start here:** `executive-summary.md` (final report: summary, strengths, pain points, differences, missing features, risks, owner decisions, next research)
- **Single-file report:** `fresha-gap.md` is the user's Markdown export of the published doc. It holds the executive summary, both gap
  tables and the owner decisions. Its evidence paths are relative to this folder.
- **Live account findings:** `fresha-live-findings.md` is a separate read-only study of the real "Point barbershop" production account
  (2026-09-28): how the three branches actually use Fresha, with volumes, payments, pricing, staff and settings. It holds counts only,
  with no customer or staff personal details.
- **Live commission research:** `fresha-commission-research.md` is a read-only study of how the live account sets up, attributes,
  reports and pays staff commission (2026-09-28). Staff are described by role only.
- **Decisions for the owner:** `owner-decisions.md`
- **Fresha vs plan matrix:** `gap-analysis.md`
- **Speed and usability:** `ux-analysis.md`
- **Per-module findings:** `module-research/*.md`
- **Coverage of every brief item:** `coverage-checklist.md` (status for all items in brief §4–§24)
- **Raw chronological notes:** `research-log.md`
- **Everything created or changed in Fresha during testing:** `test-data-log.md`
- **Evidence:** `evidence/<module>/…` (screenshots `.png`, accessibility-tree text captures `.aria.txt`, downloaded files `.csv` / `.pdf`)

## Scope and environment

| Item | Value |
| --- | --- |
| Date | 2026-09-27 |
| Product | Fresha partner web app `partners.fresha.com` (desktop Chrome 152 on Linux/WSLg, viewport ~1908×960; responsive checks at 390 px and 820 px) |
| Workspace | **"Baber Shop"**: the user's **test / sandbox** workspace (USER-PROVIDED), **trial plan**, **country Singapore, currency SGD**, time zone GMT+8, 24-hour time |
| Live account | Not accessed during this sandbox study. Later examined read-only (2026-09-28) through the shared "RC Team" login: **Myanmar / MMK** confirmed. See `fresha-live-findings.md` |
| Starting data | 1 location, owner + 1 demo team member, 3 demo clients, 4 demo services, 3 demo appointments |
| Added for testing | Location "Branch B"; test barbers Aung (2 branches) and Min (Branch B); test clients; custom payment method "KBZPay"; product, supplier, transfer, stocktake; register; commission plan; timesheet; time off; sales, refund, void (see `test-data-log.md`) |
| Customer-side booking | Observed on a **third-party public Fresha venue** (Good Luck Barbers, Singapore), anonymously, stopped before login/submit, by the user's choice |

## Labels (kept separate everywhere)

- **OBSERVED**: seen in the UI during this session, with evidence.
- **USER-PROVIDED**: stated by the user (the brief or answers during the session).
- **INFERRED**: reasoning from observations, explicitly marked, never presented as fact.
- **NOT VERIFIED**: could not be checked. The reason is given.
- **FRESHA GAP**: a planned capability that Fresha does not appear to offer (based on observed absence in the screens visited).
- "OBSERVED absence" means the screens, menus and catalogues visited didn't contain the feature. Fresha could still offer it in another plan or app.

## Method

1. The user logged in personally in a dedicated Chrome window. The researcher never saw, typed or stored credentials or codes.
2. Module-by-module exploration: navigation map, then booking and calendar, walk-in and checkout, services, schedules, commission and pay, inventory,
   reports, then the rest (brief §3–§24).
3. Behaviour was tested by **performing** workflows in the sandbox (the user authorised creating and changing test data) and recording steps,
   fields, options and outcomes.
4. Evidence was saved per step (screenshots plus accessibility-tree captures), then written up per module.

## Security and privacy handling

- No password, OTP, cookie or token was requested, read, stored or copied. The dedicated browser profile lived in a temporary scratch folder
  that was **deleted automatically** when the session ended.
- A 4-digit **pay-run verification code** prompt was cancelled (not handled), per brief §1.
- The first login attempt failed because the WSL browser had WebGL disabled (reCAPTCHA risk signal). This was fixed by enabling the real GPU,
  **not** by bypassing or spoofing anything.
- No private APIs, network interception or scraping were used. Pages were browsed at human pace.
- Test clients and staff used non-deliverable `@example.com` addresses and no real phone numbers. Automated client emails therefore show
  "Error" in Messages history.
- The public venue page was browsed anonymously. Nothing was submitted and no login was made.
- Screenshots contain sandbox data (the user chose "keep real data"). They include the owner's **name, email address, phone number and the
  Yangon street address** of the onboarding location. The address is also printed on the receipt PDF (`evidence/payments/receipt-sale-1.pdf`).
  Review before sharing outside the team.
- The sandbox trial ends around **2026-10-04**. Follow-up checks that need this workspace must happen before then (see `executive-summary.md`).

## Known limitations

- Singapore sandbox, not the live Myanmar / MMK account: currency, phone and address behaviour may differ.
- Only 2 locations and 3 bookable staff, so performance at 15+ barbers and ~70 bookings/day wasn't observed.
- No barber login was available, so the barber view and staff-to-staff notifications are NOT VERIFIED.
- Trial plan: Premium reports (Insights) and paid add-ons weren't available.
- The research browser session ended before one last check (reschedule activity log), which is marked NOT VERIFIED.

## Evidence conventions

- Paths in all documents are relative to this folder, e.g. `evidence/booking/cross-branch-conflict-before-save.png`.
- `.aria.txt` files are text snapshots of the page's accessibility tree (field names, options, states). They're often more precise than screenshots.
- Where only text was captured, the document cites the navigation path and `research-log.md` section instead of a screenshot.
