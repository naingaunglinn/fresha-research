# Services: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. The demo catalogue had one category "Hair &
> styling" with Haircut 45 min SGD 40, Hair Color 1 h 15 min SGD 57, Blow Dry 35 min SGD 35, Balayage 2 h 30 min SGD 150.
> Evidence: `evidence/services/service-menu-01.aria.txt`.

## Navigation

- `Catalog → Service menu` (`/catalogue/services`); edit a service: click it → full-screen "Edit service" dialog
  (`/catalogue/services/service/edit/<id>`)

## OBSERVED

### Service list

- Categories panel (All categories, per category counts, "Add category"); search; **location filter** (appears once there are
  2+ locations); Filters; Manage order. Evidence: `evidence/services/service-menu-01.png`
- List **Options**: Quick booking link, Set menu order, **Set booking sequence**, **Bulk edit services**, Settings,
  **Download PDF / Excel / CSV**. There's no service import. (Text capture, `research-log.md` §17.)
- After per-location pricing was set, the row read **"Haircut 45 min – 50 min, from SGD 40"**.
  Evidence: `evidence/services/service-menu-after-advanced-pricing.png`

### Edit service: sections

| Section | Observed content | Evidence |
| --- | --- | --- |
| Basic details | Service name (≤255), Menu category, **Treatment type** (marketplace taxonomy), Description (≤1000, "Generate with AI"), Price type **Free / From / Fixed**, Price, Duration (5 min … 12 h), **Add extra time**, **Options → Add variant / Advanced pricing and duration** | `evidence/services/service-edit-haircut-01.aria.txt`, `evidence/services/service-options-menu.png` |
| Extra time | **Processing time** (member available during it; included in client-facing duration), **Blocked time** (member occupied; excluded from client-facing duration, e.g. clean-up), **Extra servicing time** (member occupied; included) | `evidence/services/service-extra-time.png` |
| Locations | "All locations" checkbox (ticked) + per-location checkboxes | `evidence/services/service-edit-haircut-tab-locations.aria.txt` |
| Team members | "All team members" + per-member checkboxes (eligibility) | `evidence/services/service-edit-haircut-tab-team-members.aria.txt` |
| Resources | "No resources set up… to enable bookings without a team member" | `evidence/services/service-edit-haircut-tab-resources.aria.txt` |
| Service add-ons | "Allow clients to add customizations and extras to their booking" → Add group | `evidence/services/service-edit-haircut-tab-service-add-ons.aria.txt` |
| Online booking | Enable online booking; Available for All genders / Female only / Male only; upselling (service / membership / package); **limit availability between specific dates**; **limit to specific days of week and time of day** | `evidence/services/service-edit-haircut-tab-online-booking.aria.txt` |
| Portfolio images | jpg/png/avif/webp ≤45 MB | `evidence/services/service-edit-haircut-tab-portfolio-images.aria.txt` |
| Forms | Consultation forms per service (frequency "Every time they book an appointment") | `evidence/services/service-edit-haircut-tab-forms.aria.txt` |
| Commissions | "Calculate team member commission when the service is sold" (on/off per service); lists members' commission plans | `evidence/services/service-edit-haircut-tab-commissions.aria.txt` |
| Settings | Require patch test; aftercare instructions; **Reminder to rebook** (N days/weeks after); **Sales tax per location** ("Configure sales tax settings for each of your locations"); **Cost of service** (SGD or %); SKU (≤20) | `evidence/services/service-edit-haircut-tab-settings.aria.txt` |

### Branch + Service + Barber + Duration + Price (tested end to end)

**Advanced pricing and duration** ("Set specific pricing by location and team member"):

- Rows per **location**, and nested under each location one row per **team member working there**. Each row has Duration,
  Price type and Price overrides. Filter: All locations / Assigned locations / specific location.
  Evidence: `evidence/services/advanced-pricing-01.png`, `evidence/services/advanced-pricing-all-locations.aria.txt`
- Form field names are `locationOverrides.<locationId>.duration|priceType|price` and
  `employeeOverrides.<locationId>.<teamMemberId>.duration|priceType|price`. So **a barber's override is per branch**.
- **Cascade:** after Branch B was set to 50 min, Aung's Branch B row showed "50 min (Default)" and a price placeholder of "45"
  (inherits from the location override, which inherits from the service default). Evidence: `evidence/services/advanced-pricing-set.png`
- Saving showed: "Update price and duration for Haircut — You currently have 1 upcoming appointment for this service —
  ☐ Update already-scheduled appointments to the new price and duration (**unchecked by default**) — Clients will not be
  notified about this change". Evidence: `evidence/services/confirm-update-service-modal.png`

Test configuration and result in the staff booking drawer:

| Booking context | Duration | Price shown | Evidence |
| --- | --- | --- | --- |
| Baber Shop, Aung (no override) | 45 min | SGD 40 | `research-log.md` §16 |
| Branch B, Min (location override 50 min / SGD 45) | 50 min | SGD 45 | `evidence/services/booking-price-state.png` |
| Branch B, Aung (member override SGD 50) | 50 min | SGD 50 | `evidence/services/booking-price-branchB-aung.png` |
| Branch B, "Any team member" | 50 min | **"from SGD 45"** | `research-log.md` §16 |

### Service eligibility and availability

- Eligibility is defined both ways: service → team members, and team member → services. In the booking drawer, a service a
  member doesn't do is still listed, marked **"Team member doesn't provide this service"**; in the member picker a
  non-eligible member is labelled "Doesn't provide this service". Evidence: `evidence/booking/slot-new-appt-01.png`,
  `evidence/booking/multi-service-02-times.png`
- The team-member picker only offers members who work at the booking location (Branch B: Min, Aung; Baber Shop: Aung,
  Naing, Wendy). Evidence: `evidence/booking/new-appt-team-member-picker.png`
- Available times are computed from location + member shifts + existing bookings (including bookings at **other**
  branches) + service duration (see `booking.md`).

### Multiple services

- One appointment can hold several services, each with its own team member. Services are **chained back-to-back**:
  Haircut 10:15 (Min, 50 min) then Blow Dry 11:05 (Aung, 35 min), total 1 h 25 min.
  Evidence: `evidence/booking/multi-service-03-summary.png`
- Dynamic-assignment setting "**Allow splitting multi-service appointments across team members**" is ON by default.
  Evidence: `evidence/settings/scheduling-dynamic-assignment-edit-0.aria.txt`

### Packages / memberships / add-ons

- Catalog navigation contains **Packages** and **Memberships** (not opened in detail). Reports catalogue has Packages list /
  summary / benefits consumption and Membership list. Evidence: `evidence/_nav/nav-d-catalog.png`,
  `evidence/reports/reports-index-01.aria.txt`
- On a third-party public venue page, choosing a service opened an **add-ons picker** (e.g. "+SGD 30 … 20 min").
  Evidence: `evidence/booking/public-04b-addons.png`, `evidence/booking/public-04c-after-plus.png`

### Service reporting

- Reports can be filtered or grouped by service category / item (Sales summary "Group by → Category / Item"). The dashboard shows
  "Top services" (this month vs last month). Evidence: `evidence/reports/sales-summary-groupby.png`, `evidence/_setup/01-after-login.png`

## USER-PROVIDED

- Planned: **branch-specific service eligibility** and **branch-specific price/duration** (brief §26).

## INFERRED

- Because "Any team member" shows a "from" price, the final price is only known once a barber is assigned when barbers
  at a branch have different prices.

## NOT VERIFIED

- "Add variant" (service variants) was not explored.
- Service add-ons configuration in our own workspace (only seen on a third-party public page).
- Packages / memberships creation and redemption.
- Service history per client beyond the client profile "Items" tab (which listed services sold).
- "Set booking sequence" and "Bulk edit services" screens.
- Tax behaviour (no tax rate was configured).

## Notes for the gap analysis

- Fresha supports our planned branch-specific eligibility, price and duration, **and additionally barber-level price and
  duration per branch**. Whether the business needs barber-level pricing is an owner question.
- Changing a price doesn't update existing bookings unless the owner ticks the option.
