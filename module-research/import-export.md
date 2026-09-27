# Import / Export: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. One client-import test file with deliberate errors was taken
> to the preview step and **not imported**. One client export (sandbox data only) and two templates were downloaded.

## OBSERVED: import

| Object | Available? | Format | Evidence |
| --- | --- | --- | --- |
| Clients | ✓ `Clients list → Options → Import clients` (also a banner "Start import") | **CSV only** ("Upload a CSV file") | `evidence/import-export/client-import-01.png` |
| Products | ✓ `Products → Options → Import products` | **CSV only** (file input accepts `text/csv`) | `evidence/import-export/product-import-01.png` |
| Team members | ✗ (team list Options: share link, change order, team settings, export) | – | `research-log.md` §17 |
| Services | ✗ (service menu Options: quick booking link, order, booking sequence, bulk edit, settings, downloads) | – | `research-log.md` §17 |
| Appointments / bookings | ✗ not found | – | – |
| Finance (sales, expenses) | ✗ not found | – | – |

### Client import flow (tested with errors)

**Step 1** Upload file / **Download template** (consent statement: "By choosing to import them, you confirm they have agreed to receive
messages (SMS or email) from your business…") → **Step 2** column mapping (auto-mapped "(mapped) First name…" with a dropdown per Fresha field)
→ **Step 3 Preview** — tabs **"To be imported (N)" / "Errors (N)"**; "Errors in a row will result in that row not being imported"; Options →
**Download invalid rows** → **Step 4** Start import. Leaving asks "Lost progress… Do you want to stop importing your contacts?"
Evidence: `evidence/import-export/client-import-02-uploaded.png`, `evidence/import-export/client-import-03-step2.png`,
`evidence/import-export/client-import-04-errors.png`

- **Template columns:** First name (required), Last name, Email, Mobile phone ("Please include country code"), Gender (M, F, Male, Female, Non
  binary, Prefer not to say), Birthday (YYYY-MM-DD or DD/MM/YYYY; MM/DD/YYYY for USA/Panama/Philippines), Staff alert, Tags (pipe-separated).
  Evidence: `evidence/import-export/client-import-template_client_import_template.csv`
- **Validation results** for the 5-row test file `evidence/import-export/zz_client_import_test_input.csv`:

| Row | Problem introduced | Fresha result |
| --- | --- | --- |
| ZZImport One | none (but same email as row 2) | **Duplicated — "Email: Duplicated row found in file."** (rejected) |
| ZZImport Two | same email as row 1 | **Duplicated — same message** (rejected; **both** rows rejected) |
| ZZImport Three | email of an existing client | **Duplicated — "Email: Duplicated record found in existing customers."** (rejected; no update or merge) |
| (blank first name) | missing required field | **Data Error — "First name: Can't be blank."** |
| ZZImport Five | gender "X", birthday "31/31/2000" | **Data Error — "Birthday: Has invalid format. Gender: Is invalid."** |

  "M" was accepted as Male and "01/06/1991" parsed as 1 June 1991 (DD/MM). Result: 0 to import, 5 errors.

### Product import template

Columns: Product Name, Brand, Category, Short Description, Full Description, SKU, Barcode, Supplier, Full Price, Supply Price, Retail Sales,
Measure Unit, Measure Amount, Unlimited Stock, Image URL, and **per location**: Location Quantity (<location>), Location Low Stock Level
(<location>), Location Reorder Quantity (<location>). Evidence:
`evidence/import-export/product-import-template_product_import_template_2026-09-27.csv`

## OBSERVED: export

| Screen | Formats | Evidence |
| --- | --- | --- |
| Reports (all standard reports) | CSV, Excel, PDF | `evidence/reports/sales-summary.png` |
| Sales list | PDF, CSV, Excel | `evidence/payments/sales-list-01.png` |
| Appointments list | Export (format menu not opened) | `evidence/booking/appointments-list-01.png` |
| Clients list | Excel, CSV (CSV downloaded, columns listed in `customers.md`) | `evidence/import-export/client-export-sandbox_export_customer_list_2026-09-27.csv` |
| Team members | CSV, Excel | `research-log.md` §5 |
| Products | CSV, Excel | `research-log.md` §17 |
| Service menu | PDF, Excel, CSV | `research-log.md` §17 |
| Stock history (per product) | Excel, CSV, PDF | `research-log.md` §12 |
| Stock transfer | PDF, CSV | `evidence/inventory/stock-transfer-T1-actions.png` |
| Sale receipt | PDF / Print / Email | `evidence/payments/receipt-sale-1.pdf` |
| Daily sales summary | Export | `evidence/finance/daily-sales-summary-01.png` |

## USER-PROVIDED

- Planned: **Excel/CSV import** and **Excel/CSV/PDF export** (brief §26).

## NOT VERIFIED

- Completing an import (the preview step was the last one run); how imported clients' "Imported" source and new-client fees behave.
- Product import validation.
- Excel import: not offered (CSV only) for the two importers found.
- Appointment-list export format options.

## Notes for the gap analysis

- Fresha imports **only CSV** and only clients and products. Duplicates are rejected, not merged. Preview with per-row errors and a
  downloadable error file is available.
