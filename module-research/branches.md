# Branches / Locations: Fresha research

> **Environment.** Fresha partner web app (`partners.fresha.com`), sandbox workspace **"Baber Shop"** (trial plan,
> country **Singapore**, currency **SGD**), observed on **2026-09-27**. Evidence paths are relative to `fresha-research/`.
> Anything country-specific (phone validation, address search, currency) reflects the **Singapore** sandbox. How the same
> screens behave in the live **Myanmar / MMK** workspace is **NOT VERIFIED**.

## Navigation

- `Settings (gear) → Business setup → Locations` (`/setup/business-setup/location-details`)
- Location detail page: `/setup/location/<id>/business-details | business-location | opening-hours | sales`

## OBSERVED

### Location record

| Section | Fields / behaviour | Evidence |
| --- | --- | --- |
| Business details | Location name, Email, Phone number; business types (Main + Additional) | `evidence/branches/location-detail-01.png` |
| Business location | Street address + Google map pin | `evidence/branches/location-business-location.png` |
| Opening hours | Per weekday open/closed, start–end in 5-min steps, "+" adds **several time ranges per day**. Text: "Opening hours are displayed on your profile and are the default working hours for your team." | `evidence/branches/location-opening-hours.png`, `evidence/branches/add-location-04.png` |
| Sales (per location) | Receipt sequencing (receipt no. prefix, next receipt number); **tax defaults per location** (services / products, "using workspace defaults"); tipping (options, default values 10% / 18% / 25%, tip calculation "All items included"); receipt details (company name, address, receipt note) | `evidence/branches/location-sales.png`, `evidence/branches/location-sales.aria.txt` |
| Other | Marketplace profile settings; Manage billing profiles | `evidence/branches/location-detail-01.png` |
| Location "Options" menu | **Delete location** (only item) | `evidence/branches/location-options-menu.png` |
| Locations list "Options" | "Create a share link" | Text capture of the Options menu (`research-log.md` §3) |

### Location creation workflow (performed: created "Branch B")

`Settings → Business setup → Locations → Add` → **Step 1/4** "Add your business details" → **Step 2/4** business
categories → **Step 3/4** address → **Step 4/4** opening hours → **Save location** → toast "Location created".

- Step 1: Location name (public, ≤60, "visible to your clients in notifications and when booking online"), **Internal
  location name** (optional, ≤60, "visible only to your team members"), Location phone number (**required**), Location
  email (**required**). Evidence: `evidence/branches/add-location-01.aria.txt`; validation messages "This field is required" captured as text (`research-log.md` §3)
- The phone country code is **locked to +65** (the workspace country). "+95 9…" was rejected with **"Invalid mobile number."** Only a
  Singapore-format mobile number was accepted. Evidence: disabled "+65" control and "Invalid mobile number." captured as text (`research-log.md` §3); the step-2 screen that followed: `evidence/branches/add-location-02.png`
- Step 2: primary + up to 3 related categories, pre-filled from the workspace (Hair Salon, Barber).
  Evidence: `evidence/branches/add-location-03.aria.txt`
- Step 3: address autocomplete (Google) is **restricted to the workspace country**. "Yangon" returned no suggestions and
  "Orchard Road" returned Singapore suggestions. There's a checkbox "I don't have a business address (mobile and online
  services only)", plus an Edit link for manual fields and a draggable map pin.
  Evidence: `evidence/branches/add-location-03-autocomplete.png`, `evidence/branches/add-location-03-autocomplete2.png`,
  `evidence/branches/add-location-03-address-selected.png`
- Step 4: opening hours pre-filled from workspace defaults; editable per day. Evidence: `evidence/branches/add-location-04-final.png`
- The onboarding-created location ("Baber Shop") has **no phone number** and a **Yangon** address, so onboarding
  accepted what "Add location" later rejects. Evidence: `evidence/branches/location-detail-01.png`
- Count: 4 wizard steps, ~5 screens, ~8 clicks + typing.

### Effects of adding a location (OBSERVED)

- Services that had **"All locations" ticked were automatically offered at the new location** (Haircut showed "Locations 2").
  Evidence: `evidence/services/service-edit-haircut-tab-locations.aria.txt`
- Team members are **not** added automatically; a member gets the location only when "Works at" includes it.
  When assigned, Fresha **auto-created repeating shifts equal to that location's opening hours**.
  Evidence: `evidence/schedule/scheduled-shifts-01.png`
- Once a second location existed, location selectors appeared in: calendar (`location-selector`), roster, service
  advanced pricing, product stock, stock orders, stocktakes, registers, reports filters, pay runs (rows per location).

### Multi-branch features touching other modules (OBSERVED, details in the module files)

| Area | Branch behaviour | Module |
| --- | --- | --- |
| Calendar | One location at a time. The location picker lists single locations only; **there's no combined all-branches view** | `booking.md` |
| Cross-branch busy time | A member's booking at another branch shows as a hatched "Booking at <branch>" block | `booking.md` |
| Staff | "Works at" multiple locations; roster per location; **overlapping shifts at two branches allowed** | `staff.md`, `schedule.md` |
| Services | Location availability; **price/duration override per location and per team member at a location** | `services.md` |
| Inventory | Stock per location; transfers between locations; stocktakes per location | `inventory.md` |
| Sales | Receipt numbering, tax defaults, tipping, receipt text per location; registers per location | `payments.md`, `finance.md` |
| Pay runs | One pay-run row **per team member per location** | `payroll.md` |
| Reports | Location filter and "Group by Location" in reports | `reports.md` |
| Permissions | "Can view and access all locations" (off for the default Basic role) | `roles-permissions.md` |
| Closed periods | Per location or whole business | `schedule.md` |

## USER-PROVIDED

- The live business has **3 branches**, 15+ barbers, barbers who work at several branches, ~70 customers/day
  (research brief §2).
- The live Fresha account is set to **Myanmar / MMK** (user answer, 2026-09-27).

## INFERRED

- Because address search and phone validation follow the workspace country, a Myanmar workspace would presumably accept
  Myanmar addresses and +95 numbers. Not tested.

## NOT VERIFIED

- Branch reports as a dedicated report type: none exists. Location is available as a filter and grouping in standard
  reports (see `reports.md`). There is no "branch P&L" report.
- What "Delete location" does to its appointments, stock, sales history and team assignments (not executed).
- Marketplace profile per location and branch-specific public booking pages (the marketplace profile was not published, by user
  decision).
- Behaviour with 3+ locations (sandbox had 2).

## Notes for the gap analysis

- Branch-scoped data is pervasive in Fresha: stock, pricing, shifts, pay-run rows, receipts, registers.
- There's **no multi-branch calendar view**, and Fresha doesn't prevent a barber being scheduled at two branches at the same time.
