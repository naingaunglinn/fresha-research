# Customer Management: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Clients: demo Jack/Jane/John Doe
> (`@example.com`), test "ZZTest Client A" and "ZZTest Duplicate Email" (later merged). See `test-data-log.md` rows 5, 16, 17.

## Navigation

- `Clients → Clients list | Client segments | Client loyalty | Online reputation`; client profile drawer
  (`/clients/list/drawer/clients/<id>`); `Settings → Clients` (sources, tags); global **Search** (top bar).

## OBSERVED

### Client list

- Columns: Client name (+ email), Mobile number, Reviews, **Sales** (lifetime total), Created at. Sort: Created at.
  Banner: "Import your client list — prevents new client fees for existing clients who book online".
  Evidence: `evidence/customers/clients-list-01.png`
- **Options:** Import clients, **Merge clients**, Export (Excel / CSV). **Filters:** Client segments, Client group, **Blocked
  clients**, Fresha verified, Gender. (Text capture, `research-log.md` §11.)
- **Built-in segments (11):** New clients (added in last 30 days); Recent clients (appointments in last 30 days); First visit;
  **Loyal clients (2+ sales in last 5 months)**; **Lapsed clients (3+ sales in last 12 months and none in last 2 months)**;
  **High spenders (>$500 in sales in last 12 months)**; Upcoming birthdays (30 days); Clients who booked online; Clients with
  upcoming appointments; Clients with sales (last 30 days); Imported clients. Evidence: `evidence/customers/client-segments-picker.png`

### Client creation

- Form (no field marked required): First/Last name, Email, Phone (country code defaults to +65 in this SG sandbox), Birthday,
  Gender, Pronouns; Additional info: **Client source** (default "Walk-In"), Referred by, **Preferred language** (for automated
  notifications), Occupation, Country, Additional email, Additional phone, Tags; Addresses; Emergency contacts; Settings:
  **per-channel notification consent (Email / Text / WhatsApp)** and **marketing consent (Email / Text / WhatsApp)**, all ON by
  default. Evidence: `evidence/customers/quick-add-client-01.aria.txt`, `evidence/customers/quick-add-client-settings.aria.txt`
- Can be created inline from the booking drawer ("Add new client") and the new client is attached immediately.
  Evidence: `evidence/booking/new-appt-after-client-created.png`
- Client sources available: Referral Link, Walk-In, Instagram, Imported, Google, Fresha Marketplace, Facebook, Book Now Link.
  Evidence: `evidence/settings/clients-settings.png`

### Duplicate detection and matching (tested)

1. Created "ZZTest Duplicate Email" with the **same email** as an existing client. The form showed inline: **"An existing client has
   identical contact info. Review both profiles to prevent adding duplicates."** Save was **allowed**.
   Evidence: inline warning text captured before saving (`research-log.md` §11); list after save `evidence/customers/duplicate-email-attempt.png`
2. The client list then showed a banner: **"We found duplicated client profiles. Use smart merging to combine all data into one
   profile."** Evidence: `evidence/customers/clients-list-duplicate-banner.png`
3. `Options → Merge clients` → "Merge duplicates — 2 duplicate clients found. Merging combines appointments, sales and profile
   info… **This action cannot be undone.**" (grouped by identical contact info) → Merge selected → "Confirm merge" with a
   mandatory checkbox "I understand client merging cannot be undone" → Confirm → "Merge successful".
   Evidence: `evidence/customers/merge-clients-01.png`, `evidence/customers/merge-clients-02-confirm.png`
4. **Result: the surviving profile kept the *newer* duplicate's name** ("ZZTest Duplicate Email"). The original "ZZTest Client A"
   name disappeared from the list. The appointments (2, 1 cancelled) moved to the survivor, and Client details note "ZZTest's profile
   has been merged with ZZTest Client A". Evidence: `evidence/customers/merge-clients-03-after.png`,
   `evidence/customers/client-profile-tab-client-details.png`
5. Import treats duplicates differently: rows whose email already exists are **rejected** ("Duplicated record found in existing
   customers"). See `import-export.md`.

### Phone number handling

- Client phone has a country-code selector (default +65 here). **No client was created with a phone** (to avoid messaging real
  numbers), so phone-based duplicate matching and phone validation for clients are NOT VERIFIED.
- Location and team phone validation enforced the workspace country (+65), see `branches.md`.

### Client profile

- Header: name, email, Actions, Book now; Add pronouns, Add date of birth, Created date.
- Tabs: **Overview** (wallet balance, **Total sales**, **Appointments** count, Rating, **Canceled** count, **No show** count, upcoming
  appointment card with Checkout), **Appointments** (All / Booked / Confirmed / More; upcoming and past with Rebook), **Sales**
  (All / Paid / Drafts / Unpaid), **Client details**, **Items** (services / products / memberships / packages sold), Records, Wallet,
  Loyalty, Reviews. Evidence: `evidence/customers/client-profile-01.png`, `evidence/customers/client-profile-tab-appointments.png`,
  `evidence/customers/client-profile-tab-sales.png`, `evidence/customers/client-profile-tab-items.png`
- **Actions:** Messages, Sell, **Add staff alert** ("will appear on the client's profile and appointments"), Add simple note, Add
  allergy, Add patch test, Add tag, Add reward, Edit client details, Merge profiles, **Block client**, **Delete client**.
  Evidence: `evidence/customers/client-action-add-staff-alert.png`
- **Block client:** "Blocking prevents this client from booking online appointments with you, they will find no available time
  slots. Blocked clients are also automatically excluded from any marketing messages." Reason required from: Too many no-shows,
  Too many late cancellations, Too many reschedules, Rude or inappropriate to a team member, Refused to pay, Booked fake
  appointments, Other. Evidence: `evidence/customers/client-action-block-client.png`
- **Delete client:** "Are you sure? This action cannot be undone." (not executed). Evidence: `evidence/customers/client-action-delete-client.png`

### Search

- Global search "Search anything in Baber Shop" finds clients by name, appointments by client name or **reference number**, and
  sales. Categories: Clients, Appointments, Sales, Team, Navigation, Actions, Settings. Service names weren't found.
  Finding a customer takes ~2 clicks plus typing. Evidence: `evidence/customers/global-search-03.png`
- Booking drawer client search (typing "ZZTest" filtered the list). Evidence: `evidence/customers/client-search-in-appt.png`
- Clients list search box placeholder: **"Name, email or phone"**; the duplicate banner offers **"Review and merge"**.
  Evidence: `evidence/customers/clients-list-duplicate-banner.png`

### Export

- `Clients list → Options → Export → CSV` produced columns: Client ID, First/Last/Full Name, Blocked, Block Reason, Gender, Mobile
  Number, Telephone, Email, Accepts Marketing, Accepts SMS Marketing, Address fields, Date of Birth, Added, Staff alert, Referral
  Source, Tags. It has **no visit count, total spend or last-visit date**. Evidence:
  `evidence/import-export/client-export-sandbox_export_customer_list_2026-09-27.csv`

### Communications and self-service

- Automated client messages (email / text / WhatsApp) and a messages history exist (see `notifications.md`); "Messages" action on
  the profile (Client Connect add-on active).
- Customers book online with a **Fresha customer account**. The public booking flow requires "Log in or sign up to book" (phone +
  SMS code, email, Google or Apple). Evidence: `evidence/booking/public-09-after-time-continue.png`

## USER-PROVIDED

- Planned: **customer one active booking at a time** (brief §26). The brief asks for particular attention to duplicates.

## INFERRED

- Because merge keeps the newer profile's name and details, the older, possibly better profile's name can be lost after a merge.

## NOT VERIFIED

- Phone-based duplicate detection; how a customer's online Fresha account links to an existing client record created by staff.
- "Preferred staff / service / branch" fields: **none observed** on the client profile. Preferences appear only indirectly
  (appointment history; the dynamic-assignment option "Prioritize last booked team member").
- Customer deactivation other than Block / Delete; customer self-service (cancel/reschedule) in Fresha's customer app.
- Client segmentation editing (custom segments) and loyalty.

## Notes for the gap analysis

- Duplicates in Fresha are **soft-warned and fixed afterwards** by an irreversible merge.
- Fresha has **no preferred-barber / preferred-branch field** in the profile.
- Customer statistics (total sales, appointments, cancellations, no-shows) are on the profile but not in the CSV export.
