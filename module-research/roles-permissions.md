# Roles / Permissions: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial), 2026-09-27, logged in as **Workspace owner**. Default role matrices for **Basic, Low,
> Medium, High** were read from the permission editor (not changed). Full matrix: `evidence/roles/permission-matrix.md` (121 permission rows).

## Navigation

- `Settings → Team → Permission roles` (`/setup/team/permissions`); role **Actions**: Edit permissions, Manage team members, Rename,
  Duplicate, Set as default, Delete, Move; page Options: Change order, **Edit default permission role**; **Add** → custom role wizard.

## OBSERVED

### Roles

| Role | Fresha description (verbatim) |
| --- | --- |
| Basic | Partial access to Calendar, Sales, and Reports. |
| Low | Partial access to Calendar, Sales, Clients, Online profile, Marketing, Team, Reports, and Workspace. |
| Medium | Partial access to Calendar, Sales, Clients, Catalog, Online profile, Marketing, Team, Reports, and Workspace. |
| High | Full access to Clients, Online profile, Marketing, and Workspace. Partial access to Calendar, Sales, Catalog, Team, Reports, and Payments and wallet. |
| Workspace owner | Full access to all areas. |
| No access | No access to workspace features. |

- New team members default to **Medium** (changeable). Evidence: `evidence/staff/add-team-member-settings.aria.txt`
- **Custom roles:** Add → wizard **Name (≤50) → Choose permissions → Choose team members**. Evidence: `evidence/roles/add-permission-role.png`
- Permission areas: **Calendar, Sales, Clients, Catalog, Online profile, Marketing, Team, Reports, Payments and wallet, Workspace**, each with an
  "Active" switch and granular checkboxes. Some checkboxes are locked by dependencies. Evidence: `evidence/roles/permission-role-basic-edit.png`

### Selected default permissions (✓ = on)

| Area | Permission | Basic | Low | Medium | High |
| --- | --- | --- | --- | --- | --- |
| Calendar | Can view other team members' calendars | ✓ | ✓ | ✓ | ✓ |
| Calendar | **Can create appointments** | – | ✓ | ✓ | ✓ |
| Calendar | Can apply discounts to appointments | – | – | ✓ | ✓ |
| Calendar | **Can book a service with team members not assigned to deliver that service** | – | ✓ | ✓ | ✓ |
| Sales | **Can check out sales** | – | ✓ | ✓ | ✓ |
| Sales | Can view all sales | – | ✓ | ✓ | ✓ |
| Sales | Can view own sales | – | – | – | – |
| Sales | **Can void a sale** / **Can refund a sale** | – | – | ✓ | ✓ |
| Sales | Can open / close the cash register | – | – | – | – |
| Clients | **Can view client's email and phone number** | – | ✓ | ✓ | ✓ |
| Clients | **Can view client notes at all locations** (vs at assigned locations) | – | ✓ | ✓ | ✓ |
| Clients | Can download client details | – | – | ✓ | ✓ |
| Catalog | Can import products to the catalog in bulk | – | – | – | ✓ |
| Team | Can view the team member list | – | – | – | ✓ |
| Team | Can manage their own / other members' timesheets | – | – | – | ✓ |
| Team | **Can run pay runs** | – | – | – | – |
| Team | Can manage team member compensation settings | – | – | – | ✓ |
| Reports | Can access reports | – | – | – | – |
| Reports | Can view all team members' data | ✓ | ✓ | ✓ | ✓ |
| Workspace | Can access business setup settings | – | – | – | ✓ |
| Workspace | **Can view and access all locations** | – | ✓ | ✓ | ✓ |

Evidence: `evidence/roles/permission-matrix.md`, per-area snapshots `evidence/roles/<role>-role-<area>.aria.txt`

### Branch scope

- A single switch, **"Can view and access all locations"** (Workspace area). It's off for Basic and on for the others. Client notes have
  "at assigned locations" vs "at all locations". There's no per-location role assignment (one role per member for the whole workspace).
  Evidence: `evidence/roles/basic-role-workspace.aria.txt`, `evidence/roles/basic-role-clients.aria.txt`

### Other permission-related behaviour

- **PIN switching**: "Quickly switch between users, without the need for emails and passwords" (off). Evidence: `evidence/staff/settings-team-pin-switching.png`
- Payroll completion needs a **step-up email verification code** even for the owner (see `payroll.md`).

## USER-PROVIDED

- Planned: passwordless staff authentication; roles/permissions details for the new system aren't specified in brief §26.

## INFERRED

- Because "Can run pay runs" and "Can access reports" are off in every default role, only the owner (or a custom role) handles payroll and reports.

## NOT VERIFIED

- What a Basic-role barber actually sees (no barber login).
- **Audit/log permissions**: no permission named for viewing activity logs was found in the 10 areas.
- Whether a member can have different roles per branch: no such option was observed.

## Notes for the gap analysis

- Fresha's model is **one workspace-wide role per member** plus an all-locations switch. It doesn't support "manager at Branch A, barber at
  Branch B".
