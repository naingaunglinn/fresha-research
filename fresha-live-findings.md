# Fresha live account: read-only research findings

- **Account:** "Point barbershop", the live Fresha production account (USER-PROVIDED: real production account).
- **Date:** 2026-09-28.
- **Method:** Claude connected to the user's existing logged-in Windows Chrome through Chrome DevTools MCP, in its own tab.
  - Read-only: navigation, filters and search only.
  - Nothing was created, edited, deleted, submitted or sent.
- **Label:** every finding is **OBSERVED (live)** unless marked otherwise. The evidence is the page path on `partners.fresha.com`.
- **Privacy:**
  - No customer names, phone numbers or other personal details are recorded here.
  - Team members are counted or described by role, not named.
  - Business addresses and contact details are summarised.
- **Companion:** the sandbox study in `fresha-research/` (Singapore test workspace). This file records what the **live Myanmar account** actually looks like and how it is used.

## At a glance

- **How Fresha is really used:** as an end-of-day log. Each barber's walk-ins are keyed in afterwards as nameless "Walk-In" services, often hours later and often via the shared "RC Team" login. Then **one cash sale per barber per day** is checked out after closing.
- **Volume:** ≈ 90 services/day across 3 branches (Branch 3.0 ≈ 37, Branch 2.0 ≈ 34, Branch 1.0 ≈ 19). September to date: MMK 20.3M. All time: MMK 258.5M across 5,490 payments.
- **Payments:** Cash in 5,487 of 5,490 payments. The "K pay" method has been used 2 times. **Zero refunds ever.**
- **Customers:** only 99 client profiles, with duplicates. **0% online bookings** and 0% requested barber in September.
- **Pricing:** three branch price tiers via duplicated services, and one barber-named premium service.
- **Staff time:** no clock-ins, no Fresha time off. **Lateness and leave are tracked as 10 custom blocked-time types** (paid/unpaid).
- **Unused Fresha features:** registers, tips, products/stock, packages, gift cards, resources, integrations. Only the Client Connect add-on is active.
- **Not visible to this login:** commission, pay and payment-method settings (section 13).

## 1. Workspace basics

| Item | Live value | Page |
| --- | --- | --- |
| Business name | Point barbershop | `/setup/business-setup/business-details` |
| Country | Myanmar | same |
| Currency | MMK | same |
| Tax calculation | "Retail prices exclude tax" | same |
| Team default language | English (US) | same |
| Client default language | English (US) | same |
| External links (Facebook, X, Instagram, website) | None set | same |
| Setup checklist | A "Continue setup" button shows in the header, so Fresha's onboarding checklist isn't finished | every page |

## 2. Locations (branches)

Three locations, all in Yangon (`/setup/business-setup/location-details`):

| Location name (as in Fresha) | Public marketplace profile | Opening hours | Reviews |
| --- | --- | --- | --- |
| POINT ( South Dagon ) - Branch 1.0 | No "View on Fresha" link | Mon–Sun 8:30am–8:00pm | No reviews yet |
| POINT (North Dagon) - Branch 2.0 | Yes ("View on Fresha") | Mon–Sun 8:30am–8:00pm | No reviews yet |
| POINT (South Dagon) - Branch 3.0 | Yes ("View on Fresha") | Mon–Sun 8:30am–8:00pm | No reviews yet |

- **Phone format:** Branch 1.0's phone is stored as **+95 9 …**, so the Myanmar workspace accepts Myanmar mobile numbers. The Singapore sandbox rejected +95.
- **Business type:** "Barber" (main), with no additional types.
- **Time display:** 12-hour ("Open until 8:00pm").
- **Location settings menu** (all three branches): Business details, Business location, Opening hours, Marketplace profile settings, Manage billing profiles.
  - **No per-location "Sales" section** (receipt sequencing, tax defaults, tipping), although the sandbox had one.
  - Each location page shows the error toast **"Could not fetch receipt sequencing settings"**. The cause is NOT VERIFIED; it may be a permission or plan difference.
- **Naming:** Branch 1.0 has spaces inside the brackets ("( South Dagon )") and Branch 3.0 doesn't. The names aren't consistent.

## 3. Scheduling settings (`/setup/scheduling/…`)

| Setting | Live value | Page |
| --- | --- | --- |
| Time zone | (GMT +06:30) Yangon | `time-and-calendar` |
| Time format | 12 hours (e.g. 9:00pm) | same |
| First day of week | Monday | same |
| **Online booking window** | Clients can book from **1 month** in advance until **immediately** before the start | `availability` |
| Online cancel / reschedule | Clients may cancel or reschedule **anytime** (no cut-off) | same |
| Time slot increments | 15 minutes; clients can book any available time (no gap optimisation) | same |
| **"Any" assignment (new bookings)** | "Assign the team member with **most availability on the day booked**"; **1 team member is excluded** from automatic assignment | `dynamic-assignment` |
| Reassignment of booked appointments | Online-booked appointments **can be reassigned** up to **30 minutes** before start | same |
| Online choice of barber | Clients can book specific team members, see profiles, portfolio images and star ratings; booking by gender is off | `booking-options` |
| Group booking | **Clients can book group appointments** (enabled) | same |
| Upselling | Suggest additional services during booking; packages suggested | same |
| Staff emails on online bookings | Sent to booked team members **and** one extra address | same |
| Cancellation reasons | Only the 3 defaults: Duplicate appointment · Appointment made by mistake · Client not available | `cancellation-reasons` |
| Appointment statuses | Defaults only: Booked, Confirmed, Arrived, Started, Completed, Canceled, No-show | `appointment-statuses` |
| Closed periods | None upcoming | `closed-periods` |
| Resources (rooms/equipment) | Not set up ("Start now") | `resources` |
| Waitlist | **Active** for online bookings; type "Automatically book"; priority "First in line"; "Request any preferred time" | `waitlist` |

### Blocked time types: used as attendance and leave categories (`blocked-time-types`)

The business has defined **10 custom blocked-time types**, each with a default length and a **Paid / Unpaid** flag:

| Type (as named) | Default length | Paid? |
| --- | --- | --- |
| Late to work | 30 min | Unpaid |
| DAY OFF | 8 hr 55 min | Paid |
| Training | 1 hr | Paid |
| Meeting | 1 hr | Paid |
| FAMILY CASE | 8 hr 55 min | Unpaid |
| block time | 1 hr | Unpaid |
| SICK LEAVE | 8 hr | Unpaid |
| SHOP CLOSED | 8 hr | Paid |
| LEAVE | 1 hr | Paid |
| VILLAGE | 8 hr | Paid |

**INFERRED:** the shop records **lateness, leave (sick, family, village, day off) and closures on the calendar as blocked time**, using the paid or unpaid flag to feed pay. This is real-world input for owner decisions **OD-4** (payroll deductions for lateness or absence) and **OD-13** (leave types and approval). It's also a sign that the planned attendance and leave features must cover these categories. It isn't yet verified whether the Time-off feature is also used (see Team).

## 4. Sales settings visible to this login (`/setup/sales/…`)

| Setting | Live value |
| --- | --- |
| Menu items visible | **Only "Tipping" and "Gift cards"**. Payment methods, taxes, receipts and service charges (named on the Settings page) are **not shown** to this login. |
| Tip screen at Point of Sale | **On** ("Display a tip option screen at the Point of Sale" ticked) |
| Default tip values | 10% · 18% · 25% · 35% · 45% |
| Tip calculation | All items included |
| Gift cards | **"Gift cards inactive"** (not used) |

## 5. Team (`/team/team-members`)

**Logged-in account for this research:** **"RC Team"**, permission role **High**, not the workspace owner. This matters:
- Owner-only areas are **NOT VISIBLE** from this login: payment methods, taxes, receipt sequencing, and probably pay runs, timesheets and commission.
- The Team sidebar shows only "Team members" and "Scheduled shifts".
- Findings on pay, commission and payment methods therefore need the owner's login (see "Still to check").

**Team members: 14 active**

| Job title (as entered) | Count | Permission roles |
| --- | --- | --- |
| Barber | 10 | Basic ×3, Low ×4, Medium ×3 |
| BARBER (upper-case variant) | 1 | Low |
| Master Barber | 2 | **Workspace owner** ×1, custom role **"MASTER"** ×1 |
| (no title): "RC Team" | 1 | **High** |

- **13 bookable barbers**, including the owner, who is also a Master Barber. The brief's "15+ barbers" may count archived or former staff; NOT VERIFIED.
- **"RC Team" is a shared, non-personal account** (it uses the business email) with the **High** role, the one used for daily operations on this browser.
  - **INFERRED:** actions taken through it in Fresha can't be attributed to a person.
  - This is real input for the planned passwordless per-person staff login and for audit design.
- **A custom permission role "MASTER"** exists alongside Fresha's defaults (Basic, Low, Medium, High).
- **Permission levels differ between barbers with the same title** (Basic, Low, Medium).
- Every member has an email address and a +95 mobile number on file.
- **Data quality:** job titles are inconsistent ("Barber" vs "BARBER").

### Rosters (`/team/scheduled-shifts`)

- **This login can see only its own roster.** The team-member picker offers just "RC Team", so barbers' shifts are **NOT VERIFIED** from this login.
- "RC Team" itself is rostered at **all three branches at the same time**, 8:30 AM–8 PM every day (80 hr 30 min per branch per week, 34 hr 30 min per day in total). These are overlapping cross-branch shifts, the same pattern Fresha auto-created in the sandbox.

## 6. Service menu and pricing (`/catalogue/services`)

**31 services in 4 categories** (All locations): CUT & STYLE 16, Color 5, Shampoo 7, PERM 3. Per branch: Branch 1.0 **17**, Branch 2.0 **17**, Branch 3.0 **18**.

**MMK display format:** "MMK 6,000". The code comes first, with a comma thousands separator and no decimals.

**Branch-specific prices are implemented by duplicating services**, not with Fresha's per-location price override. Each branch sees its own copy of the same-named service:

| Service (as named per branch) | Branch 1.0 (South Dagon) | Branch 2.0 (North Dagon) | Branch 3.0 (South Dagon) |
| --- | --- | --- | --- |
| Fade Cut | MMK 6,000 · 40 min | MMK 8,000 · **45 min** | MMK 7,000 · 40 min |
| Normal / Normal Cut / Normal cut | MMK 6,000 · **30 min** ("Normal") | MMK 8,000 · **25 min** ("Normal Cut") | MMK 7,000 · **20 min** ("Normal cut") |
| POINT DELUXE (1 hr) | MMK 18,000 | MMK 24,000 | MMK 21,000 |
| Shampoo (25 min) | MMK 6,000 | MMK 8,000 | MMK 7,000 |
| Facial | MMK 6,000 · 25 min ("facial") | MMK 8,000 · **40 min** | MMK 7,000 · 25 min |
| Ear piercing (10 min) | MMK 6,000 **and** MMK 7,000 (two entries) | MMK 7,000 **and** MMK 8,000 (two entries) | MMK 7,000 |
| Black (color, 20 min) | MMK 10,000 | MMK 12,000 | MMK 10,000 |
| Beard Trim (30 min) | MMK 8,000 | MMK 8,000 | MMK 8,000 |
| Home Service (1 hr) | MMK 20,000 | MMK 20,000 | MMK 20,000 |
| Hot Shave (40 min) | – | – | MMK 7,000 |
| "MASTER CUT (named after one barber)" (1 hr) | – | – | MMK 10,000 |
| Crazy Color 2 hr / Light Color 1 hr / Brown 1 hr | 75,000 / 50,000 / 35,000 | same | same |
| Hair (rebound) 1 hr / Perm (clip) 1 hr / Curly Perm 1 hr 40 min | 30,000 / 35,000 / 55,000 | same | same |
| Facial Mask (45 min) | MMK 35,000 | same | same |

**What this tells us:**
- **Three price tiers by branch:** Branch 1.0 is the cheapest (6,000), Branch 3.0 the middle (7,000) and Branch 2.0 the most expensive (8,000) for the core services. **Durations also differ by branch** for the same service (Normal cut 30 / 25 / 20 min; Facial 25 / 40 min; Fade Cut 40 / 45 min). This supports the locked "branch-specific price/duration" rule with real data.
- **Barber-level pricing exists in practice.** A premium "MASTER CUT" named after one barber is sold as its own service (MMK 10,000, 1 hr, Branch 3.0 only). This is direct input for **OD-8** (barber-level pricing); today it is handled by a separate service.
- **Duplicates and naming inconsistencies** will matter for migration and reporting:
  - Normal / Normal cut / Normal Cut; Facial / facial.
  - Two Ear piercing prices inside the same branch.
  - "Ear piercing" filed under CUT & STYLE.
  - Reports by service name will split the same service across branch copies. **INFERRED:** a migration will need a mapping from duplicated services to one service with branch prices.
- A **Home Service** (at-home haircut, 1 hr, MMK 20,000) is offered at all branches. It isn't mentioned in the brief.
- No "from" prices appear in the list, so there's **no sign of per-team-member price overrides**. NOT VERIFIED: the service edit forms weren't opened.
- The catalogue sidebar for this login shows Service menu, Packages, Products, Stocktakes, Stock orders and Suppliers. **Memberships aren't listed.**

## 7. Packages and products

| Area | Live state | Page |
| --- | --- | --- |
| Packages | **Not used.** Only Fresha's "Start now" promo with a sample package, although "Packages will be suggested during online booking" is switched on. | `/catalogue/packages` |
| Products / inventory | **Not used.** Empty product list ("Start now"), so stock, stocktakes, orders and transfers aren't used in Fresha today. | `/catalogue/products` |
| Gift cards | Inactive (section 4) | `/setup/sales/gift-cards` |

**INFERRED:** branch-level stock and stock transfers (locked decisions) will be **new processes** for the business, not a migration of existing Fresha data.

## 8. Appointments: how the calendar is actually used (`/sales/appointments-list`)

- **Volume:** "Viewing results 1 to 100 of **2535**" for **Month to date** (1–28 Sep 2026), about **90 appointments per day** across the three branches. The brief estimated ~70 customers/day.
- **Columns:** Ref #, Client, Service, Created by, Created Date, Scheduled Date, Duration, Location, Team member, Price, Status.
- **Date format in lists:** "27 Sep 2026, 7:32pm" (DD MMM YYYY, 12-hour).

**The 100 most recent appointments** (all scheduled on Sun 27 Sep 2026; counts only):

| Measure | Result |
| --- | --- |
| Client | **100 of 100 are "Walk-In"** (no named customer) |
| Status | **All "Completed"** |
| Created by | "RC Team" **44** · the barber who did the service **21** · another team member **35** |
| **Created after the scheduled start** | **100 of 100**. Delay: min **17 min**, median **~7 h (418 min)**, max **~9.5 h (567 min)** |
| Location | Branch 2.0: 46 · Branch 3.0: 44 · Branch 1.0: 10 |
| Services | Normal cut / Normal Cut / Normal: 68 · Shampoo 13 · Fade Cut 9 · Black 5 · Facial 2 · Curly Perm 2 · Brown 1 |
| Prices | MMK 8,000 ×43 · 7,000 ×40 · 6,000 ×9 · 10,000 ×4 · **60,000 ×2 · 40,000 ×1 · 13,000 ×1** |
| Durations | 20 min ×42 · 25 min ×35 · 45 min ×9 · 30 min ×9 · other ×5 |
| Team members that day | 11 |

**What this tells us** (INFERRED from the numbers above):
- **Fresha is used as an after-the-fact service log, not a live booking tool.** Every appointment is keyed in after the service, often hours later and often by the shared "RC Team" account. This matches the calendar view, where walk-ins sit back-to-back from 8:30am in fixed 20-minute blocks.
  - The recorded times are therefore **probably not the real service times.** Any report on hourly load, punctuality or barber utilisation built on them would be unreliable.
  - It also means per-barber attribution depends on whoever enters the record.
- **Prices are overridden per appointment** for colour and perm work, charged above the menu price:
  - Curly Perm: menu 55,000, charged **60,000**.
  - Brown: menu 35,000, charged **40,000**.
  - Black: menu 12,000, charged **13,000**.
  - This is real input for price-override permissions and reasons (**OD-12**).
- **For the planned "simple walk-in flow":** today's real flow is "serve first, record later". Whether the new system should record walk-ins **at the start** (queue or check-in) or **at payment** is a design point to confirm with the owner.

## 9. Payments and sales: how money is recorded (`/sales/payment-transactions`)

- **Last 30 days** (Aug 29 – Sep 28, 2026): **349 payment transactions, total MMK 22,763,500.**
  - About **MMK 759,000 per day**, 11–12 payments per day across 3 branches.
- **Columns:** Payment date, Location, Ref #, Client, Team member, Type, Method, Amount.
- **The 100 most recent payments** (19–27 Sep; counts only):

| Measure | Result |
| --- | --- |
| Method | **Cash 100 of 100** |
| Type | Sale 100 (no refunds in view) |
| Client | Walk-In 100 |
| Taken by | "RC Team" 39 · two other people 61 (3 distinct in total) |
| Location | Branch 2.0: 38 · Branch 3.0: 35 · Branch 1.0: 27 |
| Amount | min MMK 2,000 · **median MMK 66,000** · max MMK 208,000 |
| Payments per day | 7–15 |

- **Sorting by Method, in both directions, still shows only "Cash".** **KBZPay (or any non-cash method) doesn't appear** among the 349 payments of the last 30 days.
  - **INFERRED:** KBZPay payments, if customers pay that way, are recorded as Cash or not separately.
  - The payment-method settings aren't visible to this login (section 4), so whether a "KBZPay" method exists at all is **NOT VERIFIED**.
- The payments **Filters** panel offers Location, Team member, Type, amount range, gift-card and deposit redemptions. There's **no payment-method filter** on this page.

**Anatomy of one sale** (Sale #1048, Branch 3.0, Sun 27 Sep 2026, client "Walk-In", status Completed):
- **14 line items, all by the same barber:** 8 × Normal cut and 6 × Shampoo at MMK 7,000 each, timed **8:30am → 1:20pm** in back-to-back 20/25-minute slots.
- Subtotal **MMK 98,000**, Total **MMK 98,000**.
- Payment **Cash, "Sun 27 Sep 2026 at 9:00pm"**, an hour **after** closing time.
- Drawer tabs: Summary, Notes, Activity. Actions shown: "Rebook" and an options menu (not opened).

**INFERRED: the real daily routine in Fresha:**
1. Customers are served as walk-ins without being registered.
2. During or after the day, each service is keyed in as a nameless "Walk-In" appointment for the barber, in sequential slots from opening time.
3. At the end of the day, **one sale per barber** is checked out for the day's services and paid as **Cash**.

This has direct consequences for the new system:
- **Daily closing (OD-6):** the "sale" is a per-barber day total, not a customer transaction.
- **Cash + KBZPay:** the method split isn't captured today.
- **One active booking per customer, customer history, preferred barber (OD-3, OD-10, OD-11):** there are practically **no customer records in use** (see Clients).
- **KPI and commission (OD-1, OD-2):** per-barber counts exist, but times and customer data don't.
- **Receipts:** no per-customer receipt is produced from Fresha.

**Receipt/MMK format:** amounts show as "MMK 7,000" and "MMK 98,000"; payment time as "Sun 27 Sep 2026 at 9:00pm".

## 10. Clients (`/clients/list`)

- **99 client profiles in total.** Fresha shows a banner: *"We found duplicated client profiles. Use smart merging to combine all data into one profile."*
- **Columns:** Client name, Mobile number, Reviews, Sales, Created at.
- **New client records are rare.** The newest were created 7 Aug 2026, 17 Jul, 28 Jun, 19 Jun and 2 May 2026; the first page reaches back to Nov 2025. That compares with ~2,500 services a month, almost all as nameless "Walk-In".
- Mobile numbers are stored in **+95** format.
- **Some client names are written in Burmese script.** The new system must store, display and search Myanmar Unicode names.
- A couple of profiles carry an email and avatar, which suggests Fresha marketplace (online) accounts.
- **INFERRED:** customers are generally **not identified** today. The planned one-active-booking rule, customer history and preferred-barber logic (OD-3, OD-10, OD-11) have no existing data to build on. A client import would be tiny (99 records, with duplicates).

## 11. Reports (`/reports`)

- This login sees **48 standard reports + 3 dashboards**. No Premium reports are listed, and **Favourites: 0** (no one has favourited a report).
- Report data is labelled "Data from 19–26 mins ago" (not real-time), as in the sandbox.

| Report (range) | Result |
| --- | --- |
| **Payments summary**, month to date (1–28 Sep) | 313 payments · MMK 20,303,000 · 0 refunds · **Cash only** |
| **Payments summary**, all time | **5,490 payments · MMK 258,496,500 · 0 refunds** · Cash **5,487** (MMK 258,430,500) · **"K pay" 2** (MMK 60,000) · "Other" 1 (MMK 6,000) |
| **Appointments summary**, month to date | **315 appointments / 2,535 services** · total value MMK 20,513,000 · avg MMK 65,121 per appointment · **% online 0%** · % requested 0% · % cancelled 0.6% · % no-show 0% · total clients 0 · new clients 0 |
| … Branch 2.0 (North Dagon) | 100 appts · 946 services · **MMK 8,537,000** · avg MMK 85,370 · 0% cancelled |
| … Branch 3.0 (South Dagon) | 114 appts · 1,044 services · **MMK 8,345,000** · avg MMK 73,202 · 1.8% cancelled |
| … Branch 1.0 (South Dagon) | 101 appts · 545 services · **MMK 3,631,000** · avg MMK 35,951 · 0% cancelled |
| **Tips summary**, month to date | "No results found" (**no tips recorded**, although the tip screen is on) |
| **Attendance summary**, month to date | "No results found" (**no clock-ins or timesheets used**) |
| **Team time off report**, last 30 days | "No results found" (**Fresha "time off" not used**; leave is recorded as blocked time, see section 3) |
| **Commission summary**, all time and today | **"Report data can't be fetched"**: not available to this login. Commission settings and data are **NOT VERIFIED**. |

**What the numbers say:**
- **KBZPay:** a custom payment method named **"K pay"** exists, but it has been used **twice in the account's whole history**. Everything else is Cash, which answers part of **OD-6**: today KBZPay is effectively not recorded in Fresha.
- **"Appointment" in Fresha here = one barber's day.** 315 appointments hold 2,535 services (about 8 services each), with about one payment per appointment (313 payments). This confirms the end-of-day, per-barber batch recording in sections 8 and 9.
- **Online booking is configured but unused:** 0% online in September, and 0% "requested" (no customer chose a specific barber).
- **Branch volume:** Branch 3.0 ≈ 37 services/day, Branch 2.0 ≈ 34/day, Branch 1.0 ≈ 19/day (month to date ÷ 28 days). Total ≈ 90 services/day.
- **Refunds: zero, ever.** Voids, discounts and cash differences weren't checked (discount and cash-register reports not opened).

## 12. Cash registers, discounts, messaging and add-ons

| Area (range) | Live state | Page |
| --- | --- | --- |
| **Cash register summary** (month to date) | "No results found": **registers (opening float, counted cash, closing) are not used** in Fresha | `/reports/table/cash-register-summary` |
| **Discount summary** (month to date) | **30 items** discounted, category **"Manual"** only · gross MMK 632,000 · item discounts **−MMK 117,000** (18.5% on those items) · cart discounts MMK 0 | `/reports/table/discount-summary` |
| Reminders | "3 hours upcoming appointment reminder" **Enabled**; "1 hour …" Disabled | `/marketing/automated-messages` |
| Appointment updates | New appointment **Disabled** · Rescheduled Disabled · Canceled **Enabled** · Did not show up Disabled · Thank you for visiting (review link) **Enabled** | same |
| Waitlist messages | Joined the waitlist **Enabled** · Time slot available **Enabled** | same |
| Marketing automations | Reminder to rebook **Enabled** · Birthdays, win-back lapsed, reward loyal, welcome new clients: **not enabled** | same |
| Client messages | New chat message **Enabled** · Message received **Enabled** | same |
| Message channels (email / SMS / WhatsApp) | **NOT VERIFIED**: per-automation settings weren't opened | – |
| Add-ons | **Client Connect: Active** (two-way messaging). Smart Website, Bookable Resources: not active | `/add-ons` |
| Integrations | Xero, QuickBooks (View disabled), Facebook/Instagram bookings, Meta Pixel, Google Analytics, Google Ads: **none connected** | same |

**INFERRED:**
- Daily cash closing (OD-6) happens **outside Fresha**; there's no register data to migrate.
- **Manual discounts are used** (about 1 in 85 services this month), so discount permissions and reasons (**OD-12**) and commission on discounted prices (**OD-1**) are practical questions.
- Customer messaging exists but has **almost no one to reach**, because walk-ins carry no client record.

## 13. What couldn't be seen from this login (needs the owner's login)

This research used the shared **"RC Team" (High role)** login. These remain **NOT VERIFIED** and need the **workspace owner** to look, or to open the pages for us:

1. **Payment-method settings**: whether "K pay" is set up with any details, and any other custom methods.
2. **Taxes, receipt numbering and service charges** (Settings → Sales). Also the cause of the "Could not fetch receipt sequencing settings" error.
3. **Commission settings and commission data**: the Commission summary returned "Report data can't be fetched" for this login.
4. **Wages, pay runs and pay settings per barber** (salary type, rates). The Pay summary and Wages reports weren't opened.
5. **Barbers' rosters and which branches each barber is assigned to**: this login sees only its own roster.
6. **Role permissions**, including what the custom "MASTER" role allows.
7. **Automation channels** (SMS, email, WhatsApp) and messaging balance.

## 14. Summary for the gap analysis (all INFERRED from the observations above)

| Planned decision or owner question | What the live account shows |
| --- | --- |
| Branch-specific price / duration (locked) | **Confirmed in practice.** Three price tiers (6,000 / 7,000 / 8,000 for core services) and different durations per branch, implemented by duplicating services. |
| OD-8 barber-level pricing | **Exists in practice**: a premium "MASTER CUT" named after one barber (MMK 10,000, 1 hr, Branch 3.0). |
| Simple walk-in flow (locked) | Walk-ins are **~100% of volume** and are logged **after the fact**, often hours later, as nameless "Walk-In" appointments. |
| One active booking per customer (locked) · OD-10 · OD-11 | Customers are **practically never identified**: 99 client profiles in total, with duplicates, against ~2,500 services a month. Online booking share is **0%**. |
| Any Barber (locked) · OD-9 | The current rule is "most availability on the day", with 1 member excluded. Customers requested a specific barber in **0%** of September appointments. |
| 14-day booking window (locked) | Live setting is **1 month**, Fresha's minimum. Online booking is effectively unused. |
| Cash + KBZPay (locked) · OD-6 | **Cash only in practice.** "K pay" has been used twice ever. Sales are one per barber per day, checked out after closing. **No register or closing data.** |
| Daily closing · OD-6 | Done outside Fresha (no registers). The new system's closing flow will be new behaviour, not a copy. |
| QR + location attendance (locked) · OD-4 · OD-13 | No clock-ins and no Fresha time-off. Lateness and leave are recorded as **10 custom blocked-time types** with paid/unpaid flags. |
| Passwordless per-person staff login (locked) | Daily operations run through a **shared "RC Team" account** (High role). Moving to per-person logins is a real process change. |
| Tips · OD-4 | Tip screen on, but **no tips recorded**. |
| Discounts · OD-12 | **Manual item discounts used** (30 items / MMK 117,000 this month). |
| Branch-level stock, transfers (locked) | **Not used in Fresha** (no products), so these are new processes. |
| Myanmar + English (locked) | Team and client language is English (US). **Client names include Burmese script.** |
| MMK / 12-hour / dates | "MMK 7,000"; 12-hour time; lists show "27 Sep 2026, 7:32pm". |
| Scope: gift cards, packages, memberships, resources, marketplace | Gift cards inactive · packages none · products none · resources none · online booking 0% · no reviews. **These can stay out of the initial scope** (supports gap rows B-20, B-21, B-22). |

## 15. Research log notes

- One **stray keystroke**: a single space was sent to the Reports list page while nothing was focused. Checked straight afterwards: the page was unchanged and Favourites was still 0. **No data changed.**
- Tabs: all research was done in one tab opened for this purpose; the user's own tabs were not used. Non-Fresha tabs were not read.
- Screenshots of background tabs hang in this setup, so text snapshots were used throughout. Several full-page loads came up blank until the tab was brought to the front and reloaded.
- Raw page snapshots of lists that contain customer names were saved only by Claude Code in its local session folder. **No customer names or numbers were copied into this file.**
