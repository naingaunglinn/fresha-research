# Fresha Commission Research

- **Account:** "Point barbershop", the live Fresha production account (Myanmar, MMK, 3 branches in Yangon). USER-PROVIDED: real production account.
- **Date:** 2026-09-28.
- **Login used:** the shared **"RC Team"** account. Its permission role is **High**; it is not the workspace owner. It was already signed in on the user's Chrome.
- **Method:** read-only browsing through Chrome DevTools MCP, in one research tab.
  - Pages were read as text snapshots of the accessibility tree.
  - **Nothing was created, edited, saved, submitted or deleted.**
- **Labels:**
  - **OBSERVED:** seen on screen in the live account on 2026-09-28.
  - **INFERRED:** reasoning from observations; never presented as fact.
  - **NOT VERIFIED:** could not be checked. The reason is given in §7.
  - **SANDBOX (not live):** taken from the earlier test-workspace study (`module-research/commission.md`, `module-research/payroll.md`). It is kept for reference only.
- **Privacy:**
  - No customer data appears here.
  - Team members are described by role only.
  - Team-member IDs, plan IDs, email addresses, phone numbers and street addresses are left out. URLs use `<member-id>` and `<plan-id>`.
- **Companion:** `fresha-live-findings.md`, the general live study from the same day. Its section numbers are cited as "live findings §n".

## Research Scope

**Question:** how does the live workspace set up, attribute, report and pay staff commission?

**What was examined** (all read-only):

| Area | What was done |
| --- | --- |
| Commission settings of all **14** team members | Opened each member's edit panel at **Pay → Commissions**. Closed it with "Close". "Save" was never pressed. |
| The **3** active commission plans | Opened each plan's detail screen. Fresha showed every field **disabled** (plans older than 6 months are locked). Opened its read-only "View" sub-dialogs: per-service rates, commission type, commission rules, locations and days. Closed with "Close". "Continue" was never pressed. |
| Plan history | Expanded "N deactivated commissions" on all 3 plans. Opened 2 deactivated versions' read-only summaries. |
| Reports | Read the Reports list (48 reports). Opened **Commission summary** for three date ranges earlier the same day. |
| Attribution data | Re-used the same-day aggregated counts from live findings §8, §9 and §11: the appointments list, the payments list and one sale's line items. |

**What was not examined** (full list in §7):
- **Commission report data.** Fresha returned "Report data can't be fetched" for this login.
- **The plan menu's "View report" item.** Claude Code's own safety check blocked it during this session; Fresha did not. The Escape key, used to close that menu, was blocked too. Browsing stopped there. The remaining items were not opened.
- **Pay runs, wages and the pay reports.** Pay runs and timesheets are not in this login's navigation. The pay reports were not opened.
- **Screenshots:** none were taken. Screenshots of a background tab hang in this setup, so text snapshots were used. No screenshot or snapshot files were added to this repository.

## 1. Commission Configuration

### 1.1 Where commission is configured

| Screen | Navigation (exact UI labels) | URL (IDs removed) | Status |
| --- | --- | --- | --- |
| A team member's commissions | Team → Team members → row **Actions** → **Edit** → left menu **Pay** → **Commissions** | `/team/team-members/edit/<member-id>?section=commissions` | OBSERVED |
| Active plan detail | Click the plan card in Commissions | `…/edit/<member-id>/campaign-wizard/modify/set-up-commission?section=commissions&campaignId=<plan-id>` | OBSERVED (all fields disabled) |
| Rate per service | Plan detail → Services → **View** → dialog "Commission per service" | `…/set-up-commission/override/services?…` | OBSERVED |
| Commission type, rules, locations, days | Plan detail → **Advanced options** → **View** on each row | `…/set-up-commission/commission-type/`, `…/commission-rules/`, `…/applicable-locations/`, `…/applicable-days/` | OBSERVED |
| Plan history | Commissions → "**N deactivated commissions**" → click a card | `…/campaign-wizard/summary/view-summary?…` | OBSERVED |
| Plan actions | Plan card → **Actions** | (menu) | OBSERVED labels only; see §1.7 |
| Workspace commission defaults page | SANDBOX path: Settings → Team → Commissions | – | NOT VERIFIED live (not opened). The live values are visible in each plan's "Commission rules" dialog (§1.5). |
| Per-service commission switch on the service form | SANDBOX: service edit form → "Commissions" section | – | NOT VERIFIED live (service forms not opened) |

- **Fresha's internal word for a plan is "campaign"** (OBSERVED in the URLs `campaign-wizard` and `campaignId`, and in the message "campaigns active longer than 6 months").
- **Left menu of the team-member edit panel for this login** (OBSERVED):
  - **Personal**: Profile, Addresses, Emergency contacts.
  - **Workspace**: Services, Locations, Settings.
  - **Pay**: **Commissions only**.
  - SANDBOX (not live): the owner's panel also had "Wages and timesheets" and "Pay runs" under Pay.

### 1.2 Who has a commission plan (OBSERVED)

- The Commissions section of all **14** team members was opened. **3 have an active plan; 11 have none.**
- A member without a plan sees "Add a commission". Some also see "Set up commissions quickly, using settings from another team member" and a **"Copy commission"** button. How many show it wasn't counted.
- Of the **13 bookable barbers**, **3** have a plan. The shared "RC Team" login has none.
- The 11 without a plan are **10 barbers** (job title "Barber"; roles Basic, Low and Medium) and **"RC Team"**.

| Plan | Holder (by role) | Branches the holder is assigned to | Services on the holder's profile | Active version | Deactivated versions |
| --- | --- | --- | --- | --- | --- |
| **A** | Workspace owner, job title "Master Barber" | 3 | 29 | Effective from **Feb 4, 2026** | 7 |
| **B** | Job title "Master Barber", custom permission role "MASTER" | 2 (Branch 3.0, Branch 2.0) | 30 | Effective from **Mar 2, 2026** | 14 |
| **C** | Job title "BARBER", permission role Low | 1 (Branch 3.0) | 29 | Effective from **Mar 2, 2026** | 7 |

The branch assignments of B and C come from the plan's Locations dialog, which flags each branch where the holder isn't assigned (§3).

### 1.3 The live plan: the same rates in all three (OBSERVED)

| Setting (UI label) | Value in all 3 active plans | Options Fresha offers |
| --- | --- | --- |
| Plan card | "Tiered rate" · "15%, 20%" | SANDBOX: plan type "Fixed rate" or "Tiered". Live: only tiered plans exist. |
| Detail screen title | "Set tiered rate commission": "Set how commission is calculated using sales tiers" | – |
| Sales period | **Monthly** | Daily, Weekly, Every 2 weeks, Every 4 weeks, Monthly, Quarterly |
| Sales period text | A: "First sales period is Feb 1, 2026 - Feb 28, 2026" · "Next sales period will be Mar 1, 2026 - Mar 31, 2026". B and C: "First sales period is Mar 1, 2026 - Mar 31, 2026" · "Next sales period will be Apr 1, 2026 - Apr 30, 2026" | – |
| Rate type | **"Percentage of sale amount (%)"** | Also "Fixed value on sale amount (MMK)" |
| Tier 1 | Min threshold **MMK 0** to Max threshold **MMK 2,250,000** earns **15%**. The field's text value is 2249999.99. | Tiers: "Set the amount and earning for each tier" |
| Tier 2 | Min threshold **MMK 2,250,000** "and above" earns **20%** | – |
| Commission applies to | **Services ✓** · **Service add-ons ✓** ("All service add-ons included") · Products ✗ · Packages ✗ · Memberships ✗ · Gift cards ✗ | These six item types |
| Services scope | A: "All services included" · B: "Custom overrides applied" (card: "23 services on default rate, 1 on custom override") · C: "All services included" | – |
| Commission type | "Higher commission applies only to sales above each threshold" (= **Progressive**) | Progressive or Retroactive (§1.6) |
| Commission rules | "Discounts, taxes, service costs, and product costs will be deducted from sale prices prior to calculating commission." | "Apply rules from": Workspace defaults or Custom (§1.5) |
| Locations | "All locations" (3). Row text: "This commission will be applied to sales at these locations" | All locations, or chosen branches |
| Days | Every day (card: "Applies every day"). Row text: "Commission is earned only on scheduled shifts that fall on the selected days" | Mondays … Sundays |
| Edit lock | "Editing is disabled for campaigns active longer than 6 months. To make changes, create a new campaign. You can still end, archive, or delete this one." | – |

### 1.4 Can commission differ by staff, branch, service or product?

| Differ by … | Fresha capability (OBSERVED in the plan screens) | What the live workspace does (OBSERVED) |
| --- | --- | --- |
| **Staff** | Each plan belongs to one member ("Set up how much this team member earns as a commission on sales."). "Copy commission" copies another member's plan. "Add" allows another plan; SANDBOX: several plans per member. | 3 members have a plan, all with the **same rates and threshold** |
| **Branch** | Locations: "Choose which locations to apply this commission to" (all, or chosen branches) | All 3 plans: **"All locations"**. None is branch-specific. |
| **Service** | Dialog "Commission per service": each service is set to **"Tiered" or "No commission"**, the only two options in a tiered plan. | Plan B: **1 of 24 services is "No commission"**: Color "Black", 20 min, **MMK 10,000**. The other "Black" (MMK 12,000) stays "Tiered". Plans A and C cover all services. |
| **Product** | "Products" item type | Not ticked in any plan. The product list is empty (live findings §7). |
| **Item type** | Services, Service add-ons, Products, Packages, Memberships, Gift cards | Services and service add-ons only |
| **Weekday** | "Days this commission applies to" | Every day |

**Plan B's "Commission per service" list** (OBSERVED):
- **Controls and columns:** filter "All commission types"; "Expand all" / "Collapse all"; columns "All services", "Price", "Commission rate".
- **Groups:** "CUT & STYLE group" 11, "Color group" 5, "Shampoo group" 5, "PERM group" 3. That is **24 services**.
- **Price points:** the list has the MMK 7,000 and MMK 8,000 versions of the core services and no MMK 6,000 versions.
- **Mismatch:** the holder's profile shows **30** services. The difference between 24 and 30 is NOT VERIFIED.

### 1.5 What commission is calculated on

**"Commission rules" dialog** (OBSERVED on plan B):
- Intro text: "Customize how commissions are calculated for this team member."
- Apply rules from: **"Workspace defaults"** (other option "Custom").
- All toggles are shown disabled.

| Toggle (exact label) | Description (exact) | State |
| --- | --- | --- |
| Deduct discounts | Deduct discounts from sale price prior to calculating commission | **On** |
| Deduct taxes | Deduct taxes from sale price prior to calculating commission | **On** |
| Deduct service cost | Deduct service cost from sale price prior to calculating commission | **On** |
| Deduct product cost | Deduct product cost from sale price prior to calculating commission | **On** |
| Earn commission on services paid for with a package | Commission is earned on services paid for with a package | Off |
| Earn commission on services paid for with a membership | Commission is earned on services paid for with a membership | **On** |
| Earn full commission when loyalty points are redeemed | Commission is calculated on the sale amount before loyalty points are deducted | Off |
| Earn commissions on fully paid invoices | Commission is only applied on invoices once they are marked as fully paid | **On** |
| Earn commission even if it exceeds the amount paid | Commission can be earned even if it's higher than the amount paid for the service | Off |

- **Plans A and C:** they show the same one-line rules summary (OBSERVED). Every deactivated version opened says "Commission rules: Default workspace settings" (OBSERVED). INFERRED: all three plans use these workspace values.
- **Source of these values:** they were read in the plan's dialog under "Workspace defaults", not on the workspace Settings page. That page is NOT VERIFIED.

**Answers to the configuration questions:**

| Question | Answer | Label |
| --- | --- | --- |
| Base: service price, sale amount or collected payment? | Rate type is "Percentage of sale amount (%)". Payment is a **condition**, not the base: "Commission is only applied on invoices once they are marked as fully paid" is On. | Labels OBSERVED; reading INFERRED |
| Before or after discount? | **After.** "Deduct discounts" is On. SANDBOX: a 10% cart discount was split pro rata across the lines and deducted before commission. | Setting OBSERVED; behaviour SANDBOX |
| Tax | "Deduct taxes" is On. The workspace is set to "Retail prices exclude tax" (live findings §1). Whether any tax rate exists is NOT VERIFIED; tax settings are hidden from this login. | OBSERVED / NOT VERIFIED |
| Service charge | "Commission rules" has **no service-charge toggle**. A "Service charges" report exists. Whether service charges are set up, or affect commission, is NOT VERIFIED. | OBSERVED absence / NOT VERIFIED |
| Costs | "Deduct service cost" and "Deduct product cost" are On. Whether any service has a cost set is NOT VERIFIED. | OBSERVED / NOT VERIFIED |
| Tips | Tips are **not an item type** under "Commission applies to". No tips were recorded this month: Tips summary, month to date, shows "No results found" (live findings §11). Earlier periods weren't checked. SANDBOX: tips are a separate earnings line in pay runs. | OBSERVED / SANDBOX |
| Refunds | Live: **0 refunds ever** (Payments summary, all time). SANDBOX: a refund removed the commission ("Commission deleted — Deleted because the sale was refunded by …"). | OBSERVED (no live cases) / SANDBOX |
| Cancelled or no-show | The live plans list **no cancellation or no-show fee** item type. SANDBOX: the wizard offered "Late cancellation and no-show fees". Live month to date: 0.6% cancelled, 0% no-show. | OBSERVED / SANDBOX |
| Voided or adjusted sales | NOT VERIFIED live. SANDBOX: a void removed the commission lines with no "deleted" entry. "Edit sale details" can change the team member ("Changes will be reflected in all reports"). | NOT VERIFIED / SANDBOX |
| Paid by package, membership or loyalty points | **Package-paid services earn no commission. Membership-paid services earn commission.** "Earn full commission when loyalty points are redeemed" is Off. Packages aren't used live, and memberships don't appear in this login's catalogue menu (live findings §6–§7). | OBSERVED |
| Price changed at checkout | Live appointments are charged above the menu price for some services, e.g. Curly Perm MMK 60,000 against a menu price of MMK 55,000 (live findings §8). INFERRED: with "Percentage of sale amount", commission follows the charged amount. NOT VERIFIED. | INFERRED |

### 1.6 How the tiers work (OBSERVED)

- **"Commission type" dialog:** "Choose how tiered commission rates are applied when sales thresholds are reached."
  - **Progressive**: "Higher commission applies only to sales above each threshold". **All live plans use Progressive.**
  - **Retroactive**: "Higher commission applies to all sales in the period once a threshold is reached".
- **Worked example:** the dialog shows one, built from the live thresholds (§6, Example B).
- **Sales periods are calendar months.**
  - Plan A is effective from Feb 4, 2026, but its "First sales period is Feb 1, 2026 - Feb 28, 2026".
  - Plans B and C are effective from Mar 2, 2026; their first period is Mar 1 – Mar 31, 2026.
  - How sales made before the effective date, but inside that first period, are treated is NOT VERIFIED.
- **INFERRED:** the rate steps up at MMK 2,250,000 within a month. The commission on any one sale therefore depends on the barber's total for that month so far.

### 1.7 Plan lifecycle and history

- **Active plan "Actions" menu** (OBSERVED labels; none selected): Edit commission · Schedule change · Customize name · Duplicate · View report · Deactivate commission.
- **Edit lock:** plans active for more than 6 months can't be edited, only replaced (message in §1.3).
- **History:** each plan keeps its earlier versions as "deactivated commissions" (OBSERVED).
  - The date ranges don't overlap; each version ends the day before the next one starts.
  - Plan A has had **8 versions**, plan B **15** and plan C **8**, all since **Jul 1, 2025** (§6, Example E).
- **Every version card shows "Tiered rate · 15%, 20%"** (OBSERVED).
  - The deactivated summary shows item scope, commission type, rules, locations and days, but **not the thresholds**.
  - Whether the MMK 2,250,000 threshold changed between versions is NOT VERIFIED.
- **Shared change dates:** five dates appear in all three plans' histories: **Sep 29, 2025; Nov 1, 2025; Nov 5, 2025; Jan 8, 2026; Feb 4, 2026**. Plans B and C also share Mar 2, 2026.
  - INFERRED: the plans were re-issued together, in batches.
  - The screens show **no reason and no author** for any change (OBSERVED absence). Both are NOT VERIFIED.
- **"Schedule change":** INFERRED to be how one version is ended and the next started on a chosen date. It was not opened.

## 2. Commission Attribution

| Concept | Where it appears in live Fresha | Observation | Label |
| --- | --- | --- | --- |
| Service provider | Appointments list column **"Team member"**. Each sale line shows "time • duration • team member". | Sale #1048 (Branch 3.0): 14 lines, all by one barber | OBSERVED |
| Who keyed the record | Appointments list column **"Created by"** | 100 most recent appointments (27 Sep 2026): "RC Team" 44 · the barber who did the service 21 · another team member 35 | OBSERVED (aggregated) |
| Who took the payment | Payment transactions column **"Team member"** | The 100 most recent payments (19–27 Sep 2026) show only **3 distinct names** ("RC Team" 39, two others 61). The appointments sample for 27 Sep alone shows 11 barbers serving. | Counts OBSERVED; meaning INFERRED (the checkout operator, not the provider) |
| Barber requested by the client | Appointments summary metric **"% requested"** | 0% month to date | OBSERVED |
| Who earns the commission | The plan belongs to a team member ("Set up how much this team member earns as a commission on sales.") | Which field Fresha credits commission from: NOT VERIFIED live (reports blocked). SANDBOX: the team member on each sale line. | NOT VERIFIED / SANDBOX |

- **Booked barber vs actual provider:**
  - No separate "performed by" field was seen in the appointments list or on sale lines (OBSERVED absence).
  - INFERRED: Fresha keeps **one team member per service line**. The booked barber is also the provider unless someone changes the line.
  - The only sign of booking intent seen is the "requested" metric, which is 0%.
- **Logged-in staff vs sale owner:**
  - "Created by" records who keyed the appointment, often the shared "RC Team". This is kept separate from the service's team member (OBSERVED).
  - "RC Team" has no services and no commission plan (OBSERVED).
  - SANDBOX: quick-sale lines default to the logged-in user unless changed.
- **Cross-branch commission:**
  - A plan set to "All locations" still requires the barber to be assigned to each branch. The Locations dialog shows: **"… is not assigned to this location. The commission won't apply there until they're added."** (OBSERVED on plans B and C).
  - INFERRED: under current settings, plan A earns at all three branches, plan B at Branches 3.0 and 2.0, and plan C at Branch 3.0 only. This was not checked against sales data.
- **Days rule:** "Commission is earned only on scheduled shifts that fall on the selected days" (OBSERVED).
  - Barbers' rosters are hidden from this login.
  - Services are keyed in after the fact (live findings §8).
  - Whether an after-the-fact entry that falls outside a scheduled shift earns commission is NOT VERIFIED.

## 3. Multi-Branch Behavior

- **Rules by location:**
  - Each plan has a location scope, either "All locations" or chosen branches (OBSERVED).
  - All three live plans use **all locations**.
- **Same barber, different rules at different branches:**
  - The Commissions section has an "Add" button for another plan (OBSERVED; SANDBOX: several plans per member).
  - INFERRED: different rules per branch would need one plan per branch.
  - This isn't used live; each holder has one active plan.
  - How Fresha handles two plans that cover the same sale is NOT VERIFIED.
- **Branch assignment gates commission:** see the quoted message in §2. Plan holders are assigned to 3, 2 and 1 branches (§1.2).
- **Branch prices feed the commission base:**
  - Same-named services carry branch prices, e.g. Normal cut MMK 6,000 / 7,000 / 8,000 at Branches 1.0 / 3.0 / 2.0 (live findings §6).
  - INFERRED: with "Percentage of sale amount", the same haircut earns a different commission at each branch.
- **Threshold across branches:**
  - Whether the monthly MMK 2,250,000 is counted across all branches together, or per branch, is NOT VERIFIED.
  - SANDBOX: pay runs show one row per team member **per location**.
- **Branch revenue attribution:**
  - Appointments, sales and payments each carry a **"Location"** (OBSERVED columns).
  - Month-to-date value by branch (Appointments summary, live findings §11): Branch 2.0 MMK 8,537,000 · Branch 3.0 MMK 8,345,000 · Branch 1.0 MMK 3,631,000.
  - INFERRED: commission follows the sale's location. This could not be checked live because the commission reports don't load.

## 4. Commission Reports

### 4.1 Reports in the list (OBSERVED: Reports → All reports, 48 standard + 3 dashboards)

| Report (exact name) | Description (exact) | Opened? |
| --- | --- | --- |
| **Commission summary** | Overview of commission earned by team members, locations and sale items. | Yes: data can't be fetched (§4.2) |
| **Commission activity** | Full list of all sales with commissions payable. | No (NOT VERIFIED) |
| **Pay summary** | Overview of team member compensation | No (NOT VERIFIED) |
| Wages summary | Overview of wages earned by team members | No |
| Wages detail | Detailed view of wages earned by team members across locations | No |
| Fee deduction summary | Overview of fees applied to earnings by team member, locations and sale items | No |
| Fee deduction activity | Complete list of fees applied to team member earnings | No |
| Tips summary | Analysis of gratuity income. | Yes, month to date (live findings §11): "No results found" |
| Tips detail | Comprehensive breakdown of all tips received. | No |
| Working hours summary | Overview of operational hours and productivity | No |
| Working hours activity | Detailed view of team members worked hours, shifts, and timesheets | No |
| Attendance summary | Overview of team members' punctuality and attendance for their shifts | Yes, month to date (live findings §11): "No results found" |
| Sales summary | Sales quantities and value, excluding tips and gift card sales. | No |
| Sales log detail | In-depth view into each sale transaction. | No |
| Discount summary | Overview of discounts granted and their impact on sales. | Yes (live findings §12) |

### 4.2 Commission summary (OBSERVED)

- **Path:** Reports → "Commission summary" (`/reports/table/commission-summary`).
- **Controls on the page:** "Back", "Add to favorites", a date-range button, "Advanced filters" and "Refresh page".
- **Result:** the page shows **"Report data can't be fetched"** for all three ranges tried:
  - today (the button showed "28 Sep 2026");
  - custom "19 Sep - 27 Sep 2026";
  - all time (from 2015-01-01 to 2026-09-28).
- "Advanced filters" was not opened, so the report's live filters are NOT VERIFIED.
- The cause is NOT VERIFIED. It could be a permission of the High role, or a plan or server limitation. The same login can open other reports, such as Payments summary and Appointments summary.

### 4.3 Other commission views

- **Commission activity:** listed but not opened (NOT VERIFIED).
- **Plan-level "View report"** (in a plan's Actions menu): Claude Code's safety check blocked opening it during this session (NOT VERIFIED).

### 4.4 Columns, calculation and date basis

- **Live:** NOT VERIFIED. No commission report data could be displayed.
- **SANDBOX (not live) reference:**
  - Commission summary columns: Sales qty, Items sold, Gross sales, Refunds, Tax, Discounts, Costs, **Commission base**, Commission, % Commission.
  - Filters: Team member, Location, Type, Service category, Item.
  - Export: CSV, Excel and PDF.
  - Commission was created **when the sale was checked out**, so it is dated by the sale date, not the appointment date.
- **Live context (live findings §9 and §11):**
  - OBSERVED: Sale #1048 was paid at 9:00pm, after closing, on the day of its services.
  - INFERRED there: sales are checked out once per barber per day, after closing. The evidence is 315 appointments against 313 payments month to date, plus that example.
  - INFERRED: in this business the service date and the sale date are normally the same day.
  - Checkouts after midnight are NOT VERIFIED.
- **Gross, discount and net context (OBSERVED, Discount summary, month to date):** 30 items discounted · gross MMK 632,000 · item discounts −MMK 117,000 · cart discounts MMK 0.

## 5. Pay Run / Payroll

**OBSERVED for this login:**
- The Team menu shows only **"Team members"** and **"Scheduled shifts"**. There is no Pay runs and no Timesheets entry.
- In the team-member edit panel, **Pay** contains only **"Commissions"**.
- Attendance summary and Team time off report both show "No results found" for the month (live findings §11). **No clock-ins were recorded this month.**

**INFERRED:**
- Timesheets probably aren't used either. The Working hours reports, which would show them, were not opened, so this is NOT VERIFIED.
- If there are no timesheets, Fresha has no hours to calculate hourly wages from.
- Whether wages are paid outside Fresha is NOT VERIFIED.

**NOT VERIFIED (live):**
- How commission flows into pay runs.
- Review before payroll, locking, adjustments and audit.
- The pay-run page (`/team/payrun/overview` in the sandbox) was not opened.
- The pay reports (Pay summary, Wages summary, Wages detail) were not opened.

**SANDBOX (not live) reference**, from `module-research/payroll.md`:
- **Inputs:** commission, wages and tips flow into pay runs automatically. The overview has **one row per team member per location**.
- **Breakdown:** commissions are split into Service, Service add-ons, Product, Gift card, Voucher, Membership, Package, No-show and Cancellation.
- **Activity tab:** lists each earning event, e.g. "Commission created…" and "Commission deleted… refunded".
- **Adjustments:** "Add adjustment" has tabs Wages / Commissions / Tips / Other, with **+ Add / − Deduct** and a note.
- **Review:** each location is marked **Needs review / Approved / Skip**. "Complete" is blocked until every location is Approved or Skipped.
- **Completing:** "Complete" asks for a **4-digit code sent by email**. It was not entered, so **locking after payment is NOT VERIFIED even in the sandbox**.

**Audit trail seen live (OBSERVED):**
- Commission plans keep dated versions (§1.7).
- No author or change time is shown in the plan views.
- Nothing else about commission history could be seen from this login.

## 6. Observed Examples

**Example A: the live plan as the card shows it** (OBSERVED, plan C)
> Tiered rate · 15%, 20% · All services included · All service add-ons included · Applies every day · Applies to all locations · Effective from Mar 2, 2026 · 7 deactivated commissions

**Example B: Fresha's worked example** (OBSERVED text in the "Commission type" dialog, built from the live thresholds)
> Progressive commission example. Example: 15% on the first MMK 2,249,999.99 · 20% on anything above MMK 2,249,999.99 · If team member sells MMK 4,499,999.98, they get: MMK 337,500.00 commission on 15% · MMK 450,000.00 commission on 20%

Total for that example: MMK 787,500.00 (INFERRED arithmetic; Fresha did not show a total).

**Example C: illustrative arithmetic using the live settings** (INFERRED; Fresha did not produce these figures)

| Monthly net service sales (after discounts) | Commission under the live **Progressive** setting | For comparison: under Retroactive (not used) |
| --- | --- | --- |
| MMK 1,500,000 | 15% × 1,500,000 = **MMK 225,000** | same, MMK 225,000 |
| MMK 3,000,000 | 15% × 2,249,999.99 + 20% × 750,000.01 = 337,500 + 150,000 = **MMK 487,500** | 20% × 3,000,000 = MMK 600,000 |
| One MMK 7,000 service with a MMK 1,000 manual discount, in tier 1. Assumes no service cost and no tax apply; both are NOT VERIFIED. | base MMK 6,000 × 15% = **MMK 900** | – |

**Example D: exclusion of one service** (OBSERVED, plan B)
- "Black" (Color group, 20 min, MMK 10,000): **"No commission"**.
- "Black" (Color group, 20 min, MMK 12,000): "Tiered".
- The other 22 services in the list: "Tiered".

**Example E: plan version start dates** (OBSERVED; ● = a version started that day)

| Effective from | Plan A | Plan B | Plan C |
| --- | --- | --- | --- |
| Jul 1, 2025 | ● | ● | ● |
| Jul 20, 2025 | | ● | |
| Aug 30, 2025 | ● | | |
| Sep 2, 2025 | | | ● |
| Sep 26, 2025 | ● | | |
| Sep 29, 2025 | ● | ● | ● |
| Oct 2, 2025 | | ● | |
| Oct 20, 2025 | | ● | |
| Oct 29, 2025 | | ● | |
| Nov 1, 2025 | ● | ● | ● |
| Nov 5, 2025 | ● | ● | ● |
| Dec 29, 2025 | | ● | |
| Jan 8, 2026 | ● | ● | ● |
| Feb 4, 2026 | ● **active** | ● | ● |
| Feb 9, 2026 | | ● | |
| Feb 13, 2026 | | ● | |
| Feb 17, 2026 | | ● | |
| Mar 2, 2026 | | ● **active** | ● **active** |

- **Short versions:** several lasted only 3–5 days, e.g. plan A Sep 26 – Sep 28, 2025; plan B Feb 9 – Feb 12, 2026 and Feb 13 – Feb 16, 2026.
- **Two old versions opened** (OBSERVED): plan A's Jan 8 – Feb 3, 2026 and plan B's Jul 1 – Jul 19, 2025. Both summaries show Progressive, "Default workspace settings", All locations and Every day.

**Example F: typical monthly volume against the threshold** (aggregated; INFERRED arithmetic)
- Month to date (1–28 Sep 2026), appointments were worth **MMK 20,513,000** (live findings §11).
- Divided by 11–13 barbers, that is about **MMK 1.6–1.9 million per barber**.
- Individual barbers' monthly totals were not visible. Whether any plan holder passes the MMK 2,250,000 threshold is **NOT VERIFIED**.

**Example G: attribution counts** (OBSERVED, aggregated; see §2)
- **Created by** (100 appointments): "RC Team" 44 · the provider 21 · another team member 35.
- **Payment "Team member"** (100 payments): 3 distinct names.

## 7. NOT VERIFIED

Reason codes:
- **F:** Fresha returned an error for this login.
- **P:** not shown to this login.
- **S:** blocked by Claude Code's safety check in this session.
- **N:** not opened, either because it would need a write-type control, it was out of scope, or browsing had stopped after the S blocks.
- **D:** no live data exists to observe.

| Item | Reason | What would verify it |
| --- | --- | --- |
| Commission amounts for any barber or period | F, S | Owner opens Commission summary / activity, or allows the per-plan "View report" |
| Live Commission summary columns, filters ("Advanced filters") and date basis | F | Same |
| Commission activity report | N (same outcome as the blocked report view) | Same |
| Per-plan "View report" | S | The user allows this read in a later session |
| Pay summary, Wages summary / detail, Fee deduction reports | N | Open them read-only |
| Whether timesheets exist | N (Working hours reports not opened) | Open Working hours summary / activity read-only |
| Pay runs page, pay periods, pay-run settings, review / lock / adjustment flow | P, N | Owner login |
| Wage or salary settings per barber | P (Pay shows only "Commissions") | Owner login |
| Workspace commission settings page itself | N (values seen only in the plan dialog) | Open Settings → Team → Commissions |
| Per-service commission switch on service forms | N | Open a service form read-only |
| Live "Fixed rate" plan screens | N (would need "Add") | – |
| Thresholds of old plan versions | Not shown in the deactivated summary | Owner memory or Fresha support |
| Reason for, and author of, each plan change | Not shown | Owner |
| Monthly threshold counted across branches or per branch | N | Commission report, or owner |
| Two overlapping plans for one barber | N (none exist) | – |
| Effect of the "scheduled shifts" days rule on after-the-fact entries | P (rosters hidden), N | Owner login and commission report |
| Handling of sales before the effective date inside the first sales period | N | Commission report |
| Refund effect live | D (0 refunds ever) | SANDBOX shows commission deleted |
| Void or edit effect live | N, D | – |
| Commission on cancellation / no-show fees | N (not an item type in live plans) | – |
| Commission on price overrides | N | Commission activity report |
| Tax rates and service charges configured | P | Owner login |
| Service and product costs configured | N | Service forms |
| 24 services in plan B's list vs 30 on the profile | N | – |
| Meaning of the payment "Team member" column | INFERRED only | Open a payment's detail |
| Whether barbers can see their own commission (e.g. the custom "MASTER" role) | P (no barber login) | Owner or a barber login |
| How the 10 barbers without a plan are paid | Outside what Fresha shows | Owner |

## 8. Implications for Our System

As requested, this section **does not recommend a design**. It lists facts from the live account that a replacement will have to deal with, and questions only the owner can answer.

**Facts from the live account** (OBSERVED unless marked):

1. **Only 3 of 13 bookable barbers** have a commission plan in Fresha: the owner, the barber with the custom "MASTER" role, and one barber with the Low role. Fresha shows nothing about how the other 10 are paid.
2. **One scheme is in use:**
   - monthly and progressive;
   - **15% up to MMK 2,249,999.99, then 20%**;
   - on services and service add-ons;
   - net of discounts, taxes and costs;
   - on fully paid invoices only;
   - including membership-paid services and excluding package-paid ones.
3. The scheme is **identical for all three holders**. It applies at every branch the holder is assigned to, on every day.
4. **Branch assignment gates commission** even when a plan says "All locations".
5. **Branch price tiers (6,000 / 7,000 / 8,000) change the commission base** for the same service (INFERRED from observed prices and the "% of sale amount" setting).
6. **One per-service exclusion exists:** a MMK 10,000 colour service carries no commission for one barber.
7. **The scheme has been re-issued often**: 8, 15 and 8 versions in about 15 months, mostly on shared dates, some lasting only 3–5 days. The screens don't show what changed or who changed it.
8. **Fresha locks plans after 6 months.** Changes then require a new version.
9. **Attribution rests on the team member on each service line**:
   - lines are keyed in after the service, often through the shared "RC Team" login;
   - the payment's "Team member" is a separate field (INFERRED to be the checkout operator);
   - customers requested a specific barber in 0% of appointments.
10. **Commission data isn't reachable from the daily login.** Pay runs and wages aren't visible, and no clock-ins were recorded this month. Whether timesheets exist is NOT VERIFIED.
11. **No refunds have ever been recorded.** Voids and edits after checkout weren't observable.

**Questions for the owner:**

1. How are the 10 barbers without a Fresha plan paid (salary, day rate, commission calculated elsewhere)?
2. For the three plan holders, is Fresha's commission figure paid as it is, or recalculated outside Fresha?
3. What changed at each re-issue (threshold, services, something else), and why on those dates?
4. Is the MMK 2,250,000 threshold meant per barber across all branches, or per branch?
5. Why is the MMK 10,000 "Black" excluded for one barber, while the MMK 12,000 "Black" is not?
6. When a different barber performs the service than the one booked, who receives the commission today, and how is that recorded?
7. Are the current Fresha rules the intended business rules? They are: discounts deducted, package-paid services excluded, membership-paid services included, and fully paid invoices only.
8. Who is allowed to see commission figures today: the owner only, each barber, or the "RC Team" login?
9. Is commission paid monthly, matching the monthly sales period, and together with any salary?

## 9. Raw Evidence / UI Labels

### 9.1 URLs visited (IDs removed)

- `/team/team-members` (list; row "Actions" menu: "Edit", "View calendar", and "Archive" on most members)
- `/team/team-members/edit/<member-id>?section=commissions`
- `/team/team-members/edit/<member-id>/campaign-wizard/modify/set-up-commission?section=commissions&campaignId=<plan-id>`
- `…/set-up-commission/override/services?section=commissions&campaignId=<plan-id>`
- `…/set-up-commission/commission-type/?…` · `…/commission-rules/?…` · `…/applicable-locations/?…` · `…/applicable-days/?…`
- `/team/team-members/edit/<member-id>/campaign-wizard/summary/view-summary?section=commissions&campaignId=<plan-id>`
- `/reports/report-group/1?category=all` (Reports list)
- `/reports/table/commission-summary` (with `?shortcut=all_time&dateFrom=2015-01-01&dateTo=2026-09-28` and `?shortcut=custom&dateFrom=2026-09-19&dateTo=2026-09-27`)

### 9.2 Exact labels by screen

- **Commissions section (member with a plan):**
  - "Commissions" · "Set up how much this team member earns as a commission on sales." · "Learn more" · "Options" · "Add".
  - Plan card: "Tiered rate" · "15%, 20%" · "All services included" / "23 services on default rate, 1 on custom override" · "All service add-ons included" · "Applies every day" · "Applies to all locations" · "Actions" · "Effective from Mar 2, 2026" · "14 deactivated commissions".
- **Commissions section (member without a plan):**
  - "Set up commissions quickly, using settings from another team member" · "Copy commission" · "Add a commission" · "Add".
  - The "RC Team" member shows no "Copy commission".
- **Deactivated card:** "Tiered rate" · "15%, 20%" · … · "Effective from Feb 17, 2026 - Mar 1, 2026".
- **Deactivated summary:**
  - Heading "Tiered rate" · "Deactivated" · "Effective from Jan 8, 2026 - Feb 3, 2026".
  - "Commission applies to" · "Services" · "All services included" / "Custom overrides applied" · "View".
  - "Advanced options" · "Commission type" "Progressive" · "Commission rules" "Default workspace settings" · "Locations" "All locations" · "Days this commission applies to" "Every day".
- **Plan detail (disabled):**
  - "Set tiered rate commission" · "Set how commission is calculated using sales tiers".
  - "Editing is disabled for campaigns active longer than 6 months. To make changes, create a new campaign. You can still end, archive, or delete this one."
  - "Sales period" · "Rate type" · "Tiers" · "Set the amount and earning for each tier" · "Min threshold" · "Max threshold" · "and above" · "earns" · "Commission value".
  - "Commission applies to" · "Select the items this commission covers" · "Services" · "Service add-ons" · "Products" · "Packages" · "Memberships" · "Gift cards".
  - "Advanced options" · "Close" · "Continue".
- **Commission per service:**
  - "Commission per service" · "Search" · "All commission types" · "Expand all" / "Collapse all" · "All services" · "Price" · "Commission rate".
  - "Choose commission type": options "Tiered" / "No commission".
- **Commission type:**
  - "Choose how tiered commission rates are applied when sales thresholds are reached."
  - "Progressive" · "Retroactive" · "Progressive commission example".
- **Commission rules:**
  - "Customize how commissions are calculated for this team member." · "Apply rules from": "Workspace defaults" / "Custom".
  - The nine toggles and their descriptions are in §1.5.
- **Locations:**
  - "Choose which locations to apply this commission to" · "Select the locations where this commission will apply" · "All locations" · "3" · "Locations".
  - For each branch the holder isn't assigned to: "… is not assigned to this location. The commission won't apply there until they're added."
  - Branch names: POINT (South Dagon) - Branch 3.0 · POINT (North Dagon) - Branch 2.0 · POINT ( South Dagon ) - Branch 1.0.
- **Days:** "Choose the days this commission is earned, based on scheduled shifts" · Mondays · Tuesdays · Wednesdays · Thursdays · Fridays · Saturdays · Sundays.
- **Plan "Actions" menu:** Edit commission · Schedule change · Customize name · Duplicate · View report · Deactivate commission.
- **Team member edit panel, left menu:** Personal (Profile, Addresses, Emergency contacts) · Workspace (Services, Locations, Settings) · Pay (Commissions).

### 9.3 Messages

- Commission summary: **"Report data can't be fetched"**, with a "Refresh page" button.
- Plan lock: "Editing is disabled for campaigns active longer than 6 months. …"
- Location gate: "… is not assigned to this location. The commission won't apply there until they're added."

### 9.4 Session log

- **Controls used:**
  - Used: navigation, row "Actions" → "Edit", "View", "Expand all", "Advanced options", and "Close".
  - Never pressed: "Save", "Continue", "Add", "Copy commission", and any plan-menu item.
- **Blocked by Claude Code's safety check** (not by Fresha):
  1. "View report" in plan C's Actions menu.
  2. The Escape key to close that menu.
  - **That Actions menu was left open in the research tab.** Nothing in it was selected, and nothing was changed.
- **Display artifact:** while a plan dialog was closing, the hidden Sales period value briefly read "Daily". The visible value before and after was "Monthly", and "Monthly" is what this report records.
- **Personal data:** the Team members list page shows staff emails and phone numbers. None were copied into this file.
