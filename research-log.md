# Research Log (chronological field notes)

Raw, evidence-linked observations captured while driving the Fresha partner web app
(`partners.fresha.com`, Chrome 152 on Linux/WSLg, desktop viewport ~1908×960) in the sandbox workspace
**"Baber Shop"** (trial, Singapore / SGD). Module files in `module-research/` are written from this log.
Labels: **OBSERVED** = seen in the UI during this session; **USER-PROVIDED** = stated by the user;
**INFERRED** = my reasoning from observations; **NOT VERIFIED** = could not be checked.

## 0. Session / environment
- OBSERVED: Partner login is passwordless — email → "We'll send you a verification code", plus "Continue with mobile",
  "Continue with Google", "Continue with Apple"; page footer "protected by reCAPTCHA". Evidence: `evidence/_setup/00-login-page.png`.
- OBSERVED: First login attempt from a browser with WebGL disabled failed with "There was a problem processing your request.
  Please try again later." (reCAPTCHA Enterprise present: `grecaptcha.enterprise`). After enabling the GPU the same login
  succeeded. INFERRED: Fresha's login is sensitive to browser trust signals. Evidence: user screenshot in conversation; `_setup/01-after-login.png`.
- USER-PROVIDED: This workspace is the user's **test account**; the barbershop's live account is separate and is set to
  **Myanmar / MMK**.
- OBSERVED: Workspace = trial ("Activate your plan … free trial ends in 7 days"), 1 location at start, 2 team members
  (owner Naing Aung Linn, "Wendy Smith (Demo)"), demo clients Jack/Jane/John Doe, 4 demo services.
  Evidence: `_nav/team_team-members.png`, `services/service-menu-01.aria.txt`.

## 1. Navigation map (OBSERVED)
Sidebar (data-qa `nav-d-*`): Home `/dashboard`, Calendar `/calendar`, Sales (Daily sales summary, Register, Appointments,
Sales, Payments, Gift cards sold, Packages sold, Memberships sold, Product orders), Clients (Clients list, Client segments,
Client loyalty, Online reputation), Catalog (Service menu, Packages, Memberships, Products, Inventory: Stocktakes,
Stock orders, Suppliers), Online presence (Marketplace profile, Reserve with Google, Facebook & Instagram bookings,
Link builder, Smart Website, Product store), Marketing (Blast campaigns, Automations, Messages history, Deals,
Smart pricing, Reviews), Team (Team members, Scheduled shifts, Timesheets, Pay runs), Reports `/reports`,
Add-ons `/add-ons`, Settings `/setup`, Help. Top bar: Continue setup, Search, Performance insights, Notifications (bell),
Fresha Connect, Wallet, user menu (My profile, Personal settings, referral, Help, language switch, Log out).
Evidence: `_nav/nav-d-*.png`, `_nav/user-menu.png`.

## 2. Settings / business (OBSERVED)
- Business details: name, Country **Singapore**, Currency **SGD** — "Your country is set to Singapore with SGD currency"
  (not editable in the edit form); Tax calculation (Retail prices exclude / include tax); Team default language; Client
  default language; external links. Evidence: `settings/business-details-edit.png`.
- Language picker: 39 languages (Arabic … Thai, Vietnamese, Malay, Indonesian, Chinese (CN/HK)); **no Burmese/Myanmar**.
  Evidence: `settings/language-picker.png`.
- Time and calendar: Time zone (GMT+08:00) Singapore, Time format **24 hours**, First day Monday; calendar colour source,
  processing/blocked time display. Evidence: `settings/setup_scheduling.png`.

## 3. Locations (OBSERVED)
- Location record: name, email, phone, business types (main + up to 3), address (Google Maps pin), opening hours
  (per weekday, 5-min steps, "+" to add several ranges/day), Sales section per location (receipt no. prefix + next
  number, tax defaults for services/products, tipping options & defaults 10/18/25%, receipt details: company name,
  address, receipt note), marketplace profile, billing profiles. Options: "Delete location". List Options: "Create a share link".
  Evidence: `branches/location-*.png`.
- Add location wizard (4 steps): 1 names (public ≤60, internal ≤60, phone **required**, email **required**) → 2 business
  categories → 3 address (autocomplete **restricted to workspace country**: "Yangon" → no results, "Orchard Road" → SG results;
  option "I don't have a business address") → 4 opening hours → Save. Phone country code locked to +65; "+95 9…" rejected
  as "Invalid mobile number". Existing onboarding location has no phone and a Yangon address.
  Evidence: `branches/add-location-0*.png|aria.txt`.
- New location automatically: included in every service with "All locations" checked; given to team members only if assigned.

## 4. Services (OBSERVED)
- Service form sections: Basic details (name ≤255, menu category, treatment type, description ≤1000 + "Generate with AI",
  price type Free/From/Fixed, price, duration 5 min–12 h, "Add extra time" = Processing time / Blocked time / Extra servicing
  time, Options = "Add variant" / "Advanced pricing and duration"), Locations (All locations / per location), Team members
  (All / per member), Resources, Service add-ons ("Add group"), Online booking (enable, gender availability, upselling,
  limit availability by dates or by weekday/time), Portfolio images, Forms, Commissions (on/off per service), Settings
  (patch test, aftercare, rebook reminder N days/weeks, sales tax per location, cost of service SGD or %, SKU).
- **Advanced pricing and duration**: "Set specific pricing by location and team member" — rows per location, nested rows
  per team member at that location, each with duration / price type / price override. Filter: All locations / Assigned
  locations / specific. Evidence: `services/advanced-pricing-01.png`.

## 5. Team (OBSERVED)
- Add team member: First name*, Last name, Email* (required), phone, additional phone, country, birthday, gender, pronouns,
  calendar colour, job title (visible online), start/end date, employment type (Employee/Self-employed), Team member ID
  ("for external systems like payroll"), notes; sections Addresses, Emergency contacts, Services, Locations ("Works at",
  at least one), Settings (calendar bookings on/off; advanced: exclude from online bookings, exclude from auto-assignment
  "Any professional"; permission role default **Medium**), Wages and timesheets (compensation None / **Hourly pay** only;
  hourly rate; overtime; proximity "Prevent manual timesheet entries when more than 50m away"; auto clock-in/out; automated
  breaks), Commissions, Pay runs (pay manually / transfer; automatic calculation; deduct Fresha processing & new-client fees;
  "Record cash payments for sales as 'paid' in pay runs").
- Saving with a role → list shows **"Pending invitation"** (email invite). Actions: Edit, Edit permission role, View calendar,
  View scheduled shifts, Add time off, **Archive**, Resend email invitation. List Options: share link, change order,
  team settings, **Export CSV / Excel**. Filters: Locations, Type, Status.
- Permission roles: Basic, Low, Medium, High, Workspace owner, No access; "Add new permission role"; role actions Edit
  permissions, Manage team members, Rename, Duplicate, Set as default, Delete, Move. Full Basic-role matrix in
  `roles/basic-role-permissions.json` (10 areas; e.g. Workspace "Can view and access all locations"; Clients "Can view
  client's email and phone number"; Sales "Can view own sales" vs "all", void/refund/edit; cash register perms).
- Team settings: Time off types (Annual leave, Sick leave, Training, Other; custom); Timesheets (location check on/off,
  auto clock-in/out, auto breaks); Pay runs (frequency Daily / Weekly / Every 2 weeks / Every 4 weeks / Semi-monthly /
  Monthly / Quarterly; restart day; start from next cycle or custom date; automatic payouts of wages/commissions/other and
  tips from business wallet); Commissions defaults (deduct discounts / taxes / service cost / product cost; earn on
  package- or membership-paid services; full commission on loyalty redemption; **earn only on fully paid invoices**;
  allow commission above amount paid); PIN switching (off; "switch between users without emails and passwords").

## 6. Schedule (OBSERVED)
- Adding a team member to a location auto-creates repeating shifts = that location's opening hours.
- Multi-location member (Aung) got **overlapping shifts at both locations** (Tue–Sat identical times) — saved with no warning.
- Roster per location (location picker), weekly, per-member weekly totals per location only. Per-member menu: Set repeating
  shifts, Unassign from location, Delete all shifts, View/Edit member. Add menu: Time off, New team member, Business closed period.
- Repeating shift editor (per location): Every 1/2/3/4 weeks, start date, ends Never / date, per-day start–end, "Add a shift"
  (multiple segments/day). Configured **Mon 09:00–13:00 Baber Shop + Mon 14:00–18:00 Branch B** successfully.

## 7. Booking (OBSERVED)
- Calendar: one location at a time (no all-branches view); views Day / 3 day / Week / Month; team selector (Scheduled team,
  All team, per-member checkboxes); filters (status, type, channel, payment status, services, creation date, requested
  team member, client segments); waitlist; Add menu: Appointment, Group appointment, Blocked time, Sale, Quick payment.
- Click empty slot → menu: Add appointment / Add group appointment / Add blocked time / Quick actions settings.
- Add > Appointment → "Select a time to book" banner (pick a slot) or "View available times".
- New-appointment drawer: Add client ("Or leave empty for walk-ins") or select existing / Add new client / Walk-In; select
  service (services the chosen member doesn't provide are listed with "Team member doesn't provide this service");
  team member default **"Any team member"**; Continue → date strip + "Available times" (15-min steps) + "Pick from calendar"
  + "Fully booked on this date … Next available date / Join the waitlist"; summary with "Doesn't repeat" (Every day/week/
  month/Custom); Options (Add a note, Add payment policy); Checkout / Save.
- Availability honoured per location shift: Mon 28 Branch B "Any" → 09:00–18:15; Aung → 14:00–17:15.
- Same client got a 2nd active future booking without any warning.
- Other-location appointment shows as hatched "Booking at Branch B" block in the member's column at the other location.
- **Staff can still save an overlapping booking**: drawer shows inline "Team member is not available" but Save succeeds
  (walk-in at Baber Shop 10:15 overlapping Branch B 10:00–10:45). Drawer time picker allows any time 00:00–23:55 (5-min).
- Existing appointment: status dropdown Booked / Confirmed / Arrived / Started / No-show / Cancel; Options: Add a note,
  Add a form, Add payment policy, View appointment activity, Set as repeating, Add to group appointment, Rebook,
  Reschedule, No-show, Cancel; buttons Pay now, Checkout. Closing with unsaved changes → confirm modal.
- Appointment activity: "Appointment created … Booked by Naing Aung, reference C145FD8C"; "Appointment status updated to
  Arrived/Started by Naing Aung" with timestamps; "Activity for this appointment in the last 12 months".

## 8. Checkout / payments (OBSERVED)
- First checkout shows POS intro ("Free to use … Start now"). Flow: Cart → Tip → Payment.
- Cart: client or walk-in; items (Edit: price, quantity, discounts, team member); Add to cart; options: Add cart discount,
  Add receipt note, Add service charge, Save as draft, Cancel sale.
- Tip: No tip / 10% / 18% / 25% / Custom (amount or %); "Tip goes to Aung Test Barber — Edit".
- Payment methods: Cash, Redeem gift, Split payment, custom methods (KBZPay, Other); Fresha: Card terminal, Self checkout,
  QR code, Manual card entry. "Save unpaid" / "Save part-paid".
- Custom checkout method = name only (added "KBZPay"). No reference / transaction-id field when paying by KBZPay.
- Cash payment: keypad, quick amounts, "Cash received by <team member>".
- Sale #1: Walk-In, Haircut SGD 40 + tip 4, Cash 20 (received by Aung) + KBZPay 24; **sale date = checkout date (27 Sep)
  although the appointment was 29 Sep**; sale options Refund sale, Edit sale details, Add a note, Email, Print, Download PDF,
  Void sale; sale activity (last 90 days) shows who took each payment. Receipt PDF uses "$" symbol and omits barber name.
  Evidence: `payments/receipt-sale-1.pdf`.
- Sales list: columns Sale #, Client, Status, Sale date, Location, Tips, Gross total; tabs Sales / Drafts; export PDF/CSV/Excel.
- Refund: Refund item / Refund amount; per original payment method (cash refund "given by" member; KBZPay refundable to
  KBZPay or Cash); reasons Accidental charge / Incorrect amount / Duplicate transaction / Item not available / Client's
  request / Potential fraud / Other → creates **Refund #2** (same numbering sequence), original sale status "Refunded".

## 9. Commission & pay runs (OBSERVED)
- Commission plan wizard: Fixed rate or Tiered; rate type % of sale or fixed SGD; applies to Services, Service add-ons,
  Products, Packages, Memberships, Gift cards, Late cancellation & no-show fees; advanced: rules (workspace defaults),
  Locations (all/specific), Days (commission only on scheduled shifts on selected days); effective from (today, future, or
  past "to recalculate data reporting"), ends never/date. Multiple plans per member ("Add").
- Pay run overview per period (Sep 21–27) **per team member per location** (Aung has two rows). Breakdown: Wages (hourly
  rate, regular/overtime hours), Commissions (Service, add-ons, Product, Gift card, Voucher, Membership, Package, No-show,
  Cancellation), Tips (At checkout, Pay by app, Terminal, After checkout), Other (processing fees, new client fees,
  adjustments), Paid, To pay. Activity tab lists each earning event with reference.
- Commission is created at checkout (sale #1 → SGD 16 = 40% of 40) and **deleted on refund** ("Deleted because the sale was
  refunded by Naing Aung Linn", −SGD 16); tip not refunded remains (SGD 4).
- Adjustments: tabs Wages / Commissions / Tips / Other, amount, + Add / − Deduct, note. No dedicated advance / loan objects.

## 10. Scheduling settings, online booking, notifications (OBSERVED)
- Scheduling settings: Time & calendar (TZ, 24h, first day; calendar colour source; display processing/blocked time;
  **display cross-location appointments**); Waitlist (auto-book, first in line, online waitlist active); Blocked time types
  (Lunch 30m unpaid, Training 1h paid, Meeting 1h paid); Resources (rooms/equipment, plan feature); Cancellation reasons
  (Duplicate appointment, Appointment made by mistake, Client not available; custom); Appointment statuses (Booked,
  Confirmed, Arrived, Started, Completed, Canceled, No-show; custom statuses can be added); Closed periods (single / multiple
  locations or whole business); Dynamic assignment ("Any professional" strategies: fill open calendars [day / prior 7 / 14
  days], take turns, fewest reviews, custom priority order; prioritise last booked team member; exclude members; **allow
  splitting multi-service appointments across team members** = ON by default; auto-reassign online-booked appointments up
  to 15 min before start); Availability (**online booking window 1–12 months only — no day-based option such as 14 days**;
  lead time immediately…14 days; cancel/reschedule cutoff anytime…72 h; show contact number; slot interval 15 min;
  intelligent slots Regular / Reduce gaps / Eliminate gaps); Booking options (book specific members, profiles, portfolio,
  ratings, gender filter, group booking, upselling, important info, **email to staff on online book/reschedule/cancel**).
  Evidence: `settings/scheduling-*.png|aria.txt`.
- Online booking not yet enabled in sandbox ("Online bookings are not enabled"). Link builder: link to everything /
  services (by services, locations or team members) / packages / memberships / gift cards + QR codes, but "To sell services
  online, publish Fresha profile" (marketplace). Add-ons: Payments, Premium Support, Insights, Google Rating Boost, Client
  Loyalty, Data Connector, AI Concierge (beta), Client Connect (active), Smart Website, Team Connect, Bookable Resources;
  integrations Xero, QuickBooks … Evidence: `booking/online-*.png`.
- Appointments list (Sales > Appointments): Ref #, Client, Service, Created by, Created date, Scheduled date, Duration,
  Location, Team member, Price, Status; date presets (Today … All time, custom range); Filters; Export.
- Reschedule (Options > Reschedule): calendar in "Select a time to book" mode, **location selector disabled** (no cross-branch
  move in this flow); outside-shift slot → "Reschedule appointment? <member> isn't scheduled to work at this time" (Go back /
  Reschedule = override); normal slot → "Update appointment — Notify <client> about reschedule" (checked by default).
  One unexplained case: warning shown for ~16:05 inside the 14:00–18:00 shift.
- Cancel: total, "No fee will be charged / No policy was applied", "Send a cancellation notification" (checked), reason
  optional (default "No reason provided"). No-show: same pattern, **no reason field**, notification checked by default.
- Checkout does NOT complete the appointment: status stayed "Started" after full payment, drawer offered "View sale" and
  "Complete now"; "Complete now" → "Completed". Appointment activity logs "Sale created — Checked out by … with sale receipt 1";
  refund not logged on the appointment.
- Client notifications log (Marketing > Messages history): time, client, appointment ref, channel, type (Confirmation,
  Cancellation, Reschedule), status (Error for example.com). Automations catalogue: reminders 3 d / 24 h / 1 h, new /
  rescheduled / canceled / no-show / thank-you (review link) / tipping, waitlist, rebook reminder, birthdays, win-back,
  loyal clients, welcome, chat, loyalty; channels Email, Text message, WhatsApp; communication balance SGD 0 (SMS/WhatsApp
  are paid).
- Staff in-app notifications (bell): tabs Appointments / Reviews / Tips / Online sales; only DEMO online-booking items shown —
  none for my own staff actions (INFERRED: actor not notified of own actions; NOT VERIFIED with 2nd user).
- Staff notification preferences (per user per workspace): locations filter; "Only my appointments" vs all team; per event
  Email / Push / In-app for client online activity, team calendar activity (new/reschedule/cancel/no-show ON; status updates
  OFF), sales & tips, reviews, messaging, **inventory low-stock alert + weekly low-stock summary**, insights daily/weekly/
  monthly email, AI concierge.

## 11. Clients (OBSERVED)
- List: name+email, mobile, reviews, sales, created; Options: Import clients, Merge clients, Export Excel/CSV; filters:
  segments, client group, blocked, Fresha verified, gender; 11 built-in segments (New 30 d, Recent 30 d, First visit, Loyal
  ≥2 sales/5 mo, Lapsed ≥3 sales/12 mo & none 2 mo, High spenders >$500/12 mo, Upcoming birthdays, Booked online, Upcoming
  appointments, With sales 30 d, Imported).
- Add client fields incl. client source (default Walk-In), referred by, preferred notification language, tags, addresses,
  emergency contacts, per-channel notification and marketing consents (Email/Text/WhatsApp all ON by default). No field required.
- **Duplicate detection = soft**: inline "An existing client has identical contact info…" but Save allowed; list banner
  "We found duplicated client profiles. Use smart merging"; Merge screen groups by identical contact info, irreversible,
  checkbox acknowledgement; **survivor kept the newer profile's name**; appointments moved; details note "profile has been
  merged with …".
- Profile: Overview (wallet balance, total sales, appointments, rating, canceled, no-show, upcoming), Appointments, Sales,
  Client details (incl. payment policy "deposit upfront or confirm with card"), Items, Records, Wallet, Loyalty, Reviews;
  Actions: Messages, Sell, Add staff alert, simple note, allergy, patch test, tag, reward, Edit, Merge profiles,
  **Block client** (reasons list; blocks online booking + marketing), **Delete client** (irreversible).
- Import (CSV only, 4 steps: upload/template → map columns → preview "To be imported / Errors" → start import); template
  columns First name*, Last name, Email, Mobile phone, Gender, Birthday, Staff alert, Tags; row errors with reasons (blank
  first name, invalid birthday/gender, **duplicated row in file → both rows rejected**, **duplicate of existing customer →
  rejected, not updated**); "Download invalid rows"; exit confirmation. Evidence: `import-export/*`.

## 12. Inventory (OBSERVED)
- Products onboarding "Free to use"; product form: name, barcode, brand, measure (ml/l/fl oz/g/kg/gal/oz/lb/cm/ft/in/whole
  product) + amount, short/long description, category, supply price, retail sales toggle (ON), retail price, markup % (auto),
  tax, team member commission toggle (ON), SKU (auto/generate/multiple), supplier, track stock (ON) with **stock quantity per
  location**, per-location low-stock level + reorder quantity + "Receive low stock notifications" (OFF by default; level
  required when ON), photos. After save the Add form re-opened blank.
- Product list: name, category, supplier, quantity (**sum of all locations**), retail price. Product drawer: "N in stock",
  tabs Product details / Stock orders / Sales / Stock history; stock info (SKU, on hand, retail value, supply value, average
  cost, total cost) + **stock on hand per location**. Actions: Add stock, Remove stock, Order stock, Sell product, Edit, Delete.
- Remove stock: choose location → qty + reason Internal use / Damaged / Out of date / Adjustment / Lost / Other ("Other"
  requires Description). Add stock: location → qty + supply price (save for next time) + reason New Stock / Return /
  Transfer / Adjustment / Other.
- Stock history list "X adjusted stock (±n) • date • location" (reason not in list); entry detail: date, team member,
  location, action/reason text, qty, cost price, stock after; history export Excel / CSV / PDF.
- **Native transfers exist** under Catalog > Stock orders > Add > "Add new transfer": source location → destination (editable)
  → add products (qty defaults to product reorder qty) → expected-by date, fees → Create order → status **Ordered** (list shows
  Order # "T1", created, expected, deliver to / from, total cost, status). Actions: Receive stock, Download PDF, Download CSV,
  Edit, Cancel order. Receive: Ordered vs Received qty, auto-fill; partial → "Mark order as partially received" or "Mark
  order as completed" → status **Partial**. **Stock moves only on receipt** (both source −2 and destination +2 logged at
  receipt time 16:50, not at creation 16:47) and only by received qty. Add new order (purchase order) requires a supplier.
- Suppliers: name, description, contact first/last name, 2 phones, email, website, physical + postal address.
- Stocktakes ("Free to use"): select location → name/description → count screen (Expected vs Counted, quick-scan counting,
  Pause, progress, activity) → Review (All / Uncounted / Unmatched / Matched / Excluded, difference, cost) → Complete
  (irreversible, optional note) → summary (started/completed, counted by, reviewed by, location, differences).
- Sale #3 (Calendar > Add > Sale, walk-in): POS grid tabs Appointments / Services / Products / Packages / Memberships / Gift
  cards / Quick sale (editable); **service and product lines default to the logged-in user as team member** — must be edited to
  credit the barber; product list shows stock at the sale's location; tip presets computed on full cart incl. products.

## 13. Pay run completion (OBSERVED)
- Pay run after sale #3: Aung Baber Shop commissions SGD 22 = Service 16 + **Product 6** (40% of 15), tips 4, total 26.
- "Pay now" wizard: 1 summary (period, members to include, wages/commissions/tips/other/total/paid/to pay, adjustments via
  Actions, Save and exit) → 2 Review pay run per location (wallet balance, total, period, date, payment method "Paid manually"
  (Edit), note, status **Needs review / Approved / Skip**; Complete blocked until all locations Approved or Skipped) →
  Complete → **"Enter verification code — A 4 digit code has been emailed to n***@gmail.com"** (step-up auth).
  I cancelled at the code prompt (brief forbids handling OTP) → paid state / period locking **NOT VERIFIED**.

## 14. Attendance / leave / closed periods (OBSERVED)
- Timesheets page lists only members with wages & timesheets enabled; Add → "Select team member" with "Expected today"
  (from shifts) → form: date + location (from shift), clock in (prefilled from shift), "Add break", clock out, hours worked,
  total paid hours → list columns member+location, date, clock in/out, breaks, hours worked, status ("Clocked out").
  Detail shows **Expected vs actual** clock in/out; Actions: Edit, Delete timesheet; Activity tab logs creation and edits with
  before/after ("Clock-in time edited from 10:00 to 10:10", who, when); no reason field observed. Timesheet hours feed pay
  run wages per location (Aung Branch B 6 h × SGD 5 = SGD 30). Web partner app: no clock-in button for the team member
  himself observed (clock-in by team member presumably via Fresha mobile app — NOT VERIFIED).
- Time off: member (location-scoped list), type (Annual / Sick / Training / Other absence reasons), start date, start & end
  time (partial days), Repeat, description (≤100), **Approved** checkbox (unchecked default), note "Online bookings cannot be
  placed during time off". Unapproved leave already shows on roster ("Annual leave 09:00–13:00", weekly hours reduced) and
  **removes availability** (Mon 28 Branch B slots start 13:00 for Any and for Min).
- Business closed period: start date, end date (whole days), description, locations (all / specific); "Online bookings cannot
  be placed when your business is closed."

## 15. Reports & finance (OBSERVED)
- Reports index: 60 reports (Dashboards 4, Standard 51, Premium 9, Custom 0; Favourites; Folders; Data connector);
  categories Sales, Finance, Appointments, Team, Clients, Inventory, Other. Full catalogue in `reports/reports-index-01.aria.txt`.
  Includes Performance/Online presence/Loyalty/AI Concierge dashboards; Sales summary, Sales list, Sales log detail, Cash
  register summary, Discount/Taxes/Finance/Payments summary, Payment transactions, Cash flow summary/statement, Service
  charges, Liability summary/activity, Prepayments, Appointments summary/list, Cancellations & no-show summary, Waitlist,
  Working hours activity, Break activity, **Attendance summary**, Wages detail/summary, Fee deduction activity/summary, Pay
  summary, Scheduled shifts, Working hours summary, Team time off, Tips summary/detail, Commission activity/summary, Client
  list, Stock on hand, Stock movement summary/log, Product list, Ordered stock. Premium (Insights add-on): Performance summary,
  Performance over time, Sales by time period, Gift card by time period, Packages benefits consumption, Prepayments by time
  period, Waitlist summary, Client summary, Client insights. **No expense, profit & loss or payroll-cost report.**
- Report UI: date range (Month to date etc.), Filters drawer (location, team member, status, channel, type, loyalty, client
  tags/segments; premium: gender, retention, supplier, brand, product/service category), Group by (type, category, item, team
  member, resource, client, loyalty, channel, location, tags, segments; **premium: source, gender, retention, hour, day,
  month, quarter, year**), Customize (premium), Options: Duplicate, Add to favorites, **Export CSV / Excel / PDF**. Every
  report header says **"Data from N mins ago"** (26–28 min observed; Sale #3 not yet included) — reports are not real-time.
- Specific reports: Sales summary cols (sales qty, items sold, gross, discounts, refunds, net, taxes, total); Payments
  summary by payment method (no., amount, refunds, net) — Cash and KBZPay shown separately; Cash register summary cols
  (register, opened by, terminals, online, redemptions, custom methods, opening float, cash payments, cash in/out, cash
  total, counted, difference, custom-method difference, balance, tips, closed by, cash to bank, closing float); Commission
  summary cols (sales qty, gross, refunds, tax, discounts, costs, commission base, commission, % commission); Attendance
  summary cols (scheduled shifts, on-time/early/late clock-ins and clock-outs, punctuality, missed shifts, attendance %).
- Sales > Daily sales summary (live, per day, prev/next, filters, export): transaction summary by item type (services, add-ons,
  products, shipping, gift cards, packages, memberships, late-cancellation fees, no-show fees, refunds) + cash movement by
  payment type (collected / refunded, of which tips).
- Registers (Sales > Register, "Included in your plan"): per location; setup options Require register open to take sales
  (**ON by default**), minimum float, midday counts, prompt if left open, auto print / email count report. Open: opening
  float (+ denomination cash counter SGD notes/coins), note. Cash in / Cash out (reasons: Petty cash for purchases, Pay team
  member tips, Deposit to bank or safe, Other adjustment; amount, count, note, **attachment**, user+date). View: expected by
  payment type (terminals, tap to pay, online, card, redemptions, custom methods incl. KBZPay, cash = float + payments + in −
  out). Close: Expected / Counted / Difference per type (custom methods + cash counted manually), closing float (carried to
  next opening), cash to bank, note → closed register record (e.g. cash 45 vs 44 = −1). No approval / reason required for
  differences.
- No expenses module anywhere in navigation (only register cash-out). No P&L.

## 16. Branch + Service + Barber pricing (OBSERVED end-to-end)
- Haircut: default 45 min / SGD 40; Branch B override 50 min / SGD 45; Aung@Branch B override SGD 50 (duration inherits
  location override). Form field names `locationOverrides.<loc>.*`, `employeeOverrides.<loc>.<member>.*`.
- Saving triggers "Update price and duration for Haircut — You currently have 1 upcoming appointment… Update already-scheduled
  appointments to the new price and duration (unchecked by default) — Clients will not be notified".
- Service list shows "45 min – 50 min, from SGD 40". Booking drawer: Branch B Min → 50 min SGD 45; Branch B Aung → 50 min
  SGD 50; Branch B "Any team member" → "50min from SGD 45"; Baber Shop Aung → 45 min SGD 40.

## 17. Late checks (OBSERVED unless stated)
- Date & time settings editor: Time zone (424 options incl. "(GMT +06:30) Yangon"), **Time format 12 hours (e.g. 9:00pm) or
  24 hours (e.g. 21:00)**, First day of week. **No date-format setting** in the editor (date display presumably follows
  language/locale — INFERRED). Global search shows times as "11:00 AM"/"5:55 PM" although the workspace is set to 24 h.
- Same-day checkout of a past appointment (Jane Doe, 27 Sep 11:00) → appointment status **Completed automatically**; paying
  with a single custom method (KBZPay) = one tap, full amount. (Early checkout of a future appointment stayed "Started".)
- Multi-service booking: Haircut (Min) + Blow Dry (Aung) in one appointment → picker marks non-eligible members "Doesn't
  provide this service"; availability for Tue 29 starts 10:15 (not 10:00) because services are chained sequentially and Aung
  is busy at Baber Shop until 11:00; saved as Haircut 10:15 Min + Blow Dry 11:05 Aung, 1 h 25 min, SGD 80.
- Cart discount: amount in SGD or %, "Taxes will be recalculated", no reason/approval; receipt shows "Items total (excl.
  discounts)", "Cart discount −SGD 5.50". Commission computed on discounted amounts pro-rated per line (service 40%×36 =
  14.40; product 40%×13.50 = 5.40) — consistent with "Deduct discounts" workspace rule.
- Void sale: modal "permanent… Following payments will be deleted… Product stock will be returned to <location>: 1 of <product>";
  no reason field; sale status "Voided"; sale activity "Voided by …"; **commission lines of the voided sale disappear from pay-run
  activity with no 'deleted' entry** (refund leaves a "Commission deleted" entry).
- Edit sale details: change team member per item and "payment collected by" per payment; "Changes will be reflected in all
  reports"; **no client field** → walk-in sale cannot be attached to a client after checkout (in this UI).
- Roles: permission matrix for Basic/Low/Medium/High in `evidence/roles/permission-matrix.md` (121 rows). "Can view and access
  all locations": Basic off, Low/Medium/High on. "Can run pay runs", "Can access reports", "Can view own sales", "Can open/close
  the cash register": off in all four default roles (owner only). Add permission role = wizard Name → Choose permissions →
  Choose team members.
- Archive team member: modal "may be viewed by adjusting your filter settings, and may be restored at any time"; no warning
  about existing bookings; archived member's appointment remains "Booked" with "Team member is not available".
- Sales settings: Pay now (requires Fresha payments), Tax rates (business or per location, tax groups), Receipts (client contact
  & address on receipt, title, custom lines, footer, sequencing per location), Registers, Tipping (POS/terminal/online, 10/18/25%,
  calc all items), Service charges (auto/manual), Gift cards (inactive). Client sources: Referral Link, Walk-In, Instagram,
  Imported, Google, Fresha Marketplace, Facebook, Book Now Link. Forms: templates. **Payment policy (deposits, no-show & late
  cancellation fees) requires Fresha Payments** (card processing) — "Start now".
- Personal settings > Login & security: password, Google/Apple connect, **Trusted devices (skip two-factor)**, active sessions
  (this Linux Chrome + user's Windows Chrome), sign out all devices, delete account. Appearance: Light/Dark/System.
- Global search (top bar): "Search anything in <workspace>", categories Clients, Appointments, Sales, Team, Navigation, Actions,
  Settings; finds clients by name, appointments by client or reference (#C145FD8C), sales; service names not found.
- Responsive web: 390 px → "Download the app" banner, single-member calendar column with team switcher, bottom nav (calendar,
  sales, +, clients, more), no horizontal scroll; 820 px → sidebar retained, condensed toolbar. Evidence `ux/*.png`.
- Import/export scope: Services Options = quick booking link, menu order, booking sequence, bulk edit, settings, Download PDF /
  Excel / CSV (no service import); Team = export CSV/Excel (no import); Products = manage brands/categories, **Import products
  (CSV only, 4 steps, template with per-location quantity / low-stock / reorder columns)**, export CSV/Excel.
- Public customer booking (third-party public venue "Good Luck Barbers – 51 Amoy Street, Singapore", anonymous, not submitted):
  venue page (services with "from" prices, team with ratings, reviews, "Book now") → choose "Book an appointment" vs "Book group
  appointment" → Select services (categories, add-on picker per service) → Select professional ("Any professional – Maximum
  availability" or named barber with rating/title) → Select date and time (date strip, time list in the venue's 12 h format,
  "Join waitlist") → **"Log in or sign up to book — We'll need to verify it's you"**: phone number + SMS verification code,
  or email / Google / Apple. Stopped here. Evidence `booking/public-0*.png`.

## 18. Final audit checks and session end
- OBSERVED: activity log of the **cancelled** appointment #867B2E43: "Appointment created — Booked by Naing Aung, reference
  867B2E43"; "Notification failed to send — Confirmation Email failed to send"; "Appointment canceled — Canceled by Naing
  Aung"; "Notification failed to send — Cancellation Email failed to send". **The chosen cancellation reason ("Client not
  available") is not shown in the activity log.** Evidence: `evidence/audit/appt-activity-cancelled.png`.
- NOT VERIFIED: activity-log content of the **rescheduled** appointment #D7C048A9 (two load attempts timed out; afterwards the
  browser session ended). Whether Fresha records before/after times for a reschedule is therefore NOT VERIFIED.
- The research browser session ended with the previous Claude Code session (2026-09-27 ~12:20 local). The scratchpad (helper
  scripts and the dedicated Chrome profile that held the Fresha login) was cleared automatically, so **no copy of the Fresha
  session remains on this machine**. A relaunch with a fresh profile was not logged in and was stopped; no further browser
  work was done.

## 19. Report finalisation (no browser work)
- Gap matrix: 9 KEEP rows in section A had a recommendation without a reason: branch-level stock, Myanmar + English UI, MMK, 12-hour
  time, DD/MMM/YYYY, 90-day notification history, weekly backup, 1-year retention and export. Reasons were added from the recorded
  observations only. The reasons for B-4, B-10, B-11a and B-15 were spelled out. Re-check: 49 rows, each with one recommendation value
  and a reason.
- Scope of "no SMS OTP": the brief lists it as its own bullet beside the staff-auth rules and doesn't say whether it also covers
  customers. Wording that had assumed it does (gap A-2, B-6 and C-1; OD-11; executive summary) now states the condition, and OD-11 asks
  the owner to confirm the scope.
- Published the executive summary, both gap tables and the owner decisions as a doc (text only, no screenshots or personal data).
- Later the same day the user deleted the doc because it couldn't be uploaded as an artifact (USER-PROVIDED). They exported its content
  to `/var/www/point/fresha-gap.md`. The export was checked: all 11 sections, 25 + 24 gap rows with the same recommendation counts, and
  16 owner decisions. The doc wasn't republished, and `README.md` points to the export.
