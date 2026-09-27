# Products / Inventory: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27, 2 locations. Test product **ZZTest Pomade** (100 g, supply
> SGD 5, retail SGD 15), supplier **ZZTest Supplier**, transfer **T1**, stocktake **"ZZTest count Baber Shop"**. See
> `test-data-log.md` rows 18–23, 24, 35, 36.

## Navigation

- `Catalog → Products`; `Catalog → Inventory: Stocktakes | Stock orders | Suppliers`; product drawer `Actions`;
  `Settings → Sales` (tax); reports: Stock on hand, Stock movement summary / log, Product list, Ordered stock.

## OBSERVED

### Products

- First visit shows onboarding "Free to use — Manage your inventory with Fresha product list… Start now".
  Evidence: `evidence/inventory/products-list-01.png`
- **Add product form**: Product name, barcode (optional), brand, **measure** (ml / l / fl oz / g / kg / gal / oz / lb / cm / ft / in /
  "A whole product") + amount, short description (≤100), description (≤1000), category; **Pricing**: supply price, **Enable retail
  sales** (ON; "Allow sales of this product at checkout"), retail price, **markup %** (auto-calculated, 200% for 5→15), tax
  (default), **Enable team member commission** (ON); **Inventory**: SKU (auto-generate / add another), supplier, **Track stock
  quantity** (ON) with **"Current stock quantity" per location**; **Low stock and reordering per location**: low stock level,
  reorder quantity, "Receive low stock notifications" (OFF by default; low stock level becomes required when ON); photos.
  Evidence: `evidence/inventory/products-start-01.aria.txt`, `evidence/inventory/product-add-filled.png`
- After Save, a blank "Add new product" form reopened (repeat-entry pattern). Evidence: `evidence/inventory/state-after-save.png`
- **Product list**: Product name, Category, Supplier, **Quantity (sum of all locations)**, Retail price; Filters; sort.
  **Options:** Manage my brands, Manage my categories, **Import products**, Export CSV / Excel. Evidence: list `evidence/inventory/product-after-save.png`; Options menu text capture (`research-log.md` §17)
- **Product drawer**: "N in stock"; tabs Product details / Stock orders / Sales / **Stock history**; stock info: SKU, stock on hand,
  retail value, supply value, **average cost**, total cost, **stock on hand per location**. **Actions:** Add stock, Remove stock,
  Order stock, Sell product, Edit product, Delete product. Evidence: `evidence/inventory/product-detail-01.png`,
  `evidence/inventory/product-actions.png`

### Stock adjustments

| Action | Flow | Reasons | Evidence |
| --- | --- | --- | --- |
| Remove stock | Actions → Remove stock → **select location** → quantity → reason → Save | **Internal use** (default), Damaged, Out of date, Adjustment, Lost, Other (**Other → required "Description"**) | `evidence/inventory/remove-stock-01.png`, `evidence/inventory/remove-stock-02.aria.txt`, `evidence/inventory/remove-stock-other.aria.txt` |
| Add stock | Actions → Add stock → select location → quantity → **supply price** (☑ save price for next time) → reason → Save | **New Stock** (default), Return, **Transfer**, Adjustment, Other | `evidence/inventory/add-stock-02.aria.txt` |

- Stock usage in services ("Internal use") is a **manual removal**. No automatic consumption of products by services was observed.

### Stock history (audit)

- List entries: "<user> adjusted stock (±n) • date • location", "received a product transfer", "**made a sale (−1)**" (attributed to the
  team member on the sale line), "**made a return (+1)**" (created by a void); "Load more" pagination.
  Evidence: `evidence/inventory/product-stock-history-after-transfer.png`, `research-log.md` §17
- Entry detail: **date, team member, location, action/reason text (e.g. "Transfer to Branch B (test)"), quantity adjusted, cost price,
  stock on hand after adjustment**. Evidence: "Stock history details" text capture (`research-log.md` §12); history list `evidence/inventory/product-stock-history-03.png`
- History export: Excel / CSV / PDF (Options).

### Stock transfers between branches (native)

- `Catalog → Stock orders → Add → **Add new transfer**` → select **source location** → "Manage products for order" (auto-saved draft:
  "Last saved …") → Deliver from / **Deliver to** (editable) → Add products (product picker shows stock) → order quantity (**defaults
  to the product's reorder quantity, 10**) → Expected by (date), Fees → **Create order** → "Stock transfer created — 3 products
  transferred — SGD 15" (Download PDF) → list row **"T1 … Deliver to Branch B, Deliver from Baber Shop, SGD 15, Ordered"**.
  Evidence: `evidence/inventory/stock-transfer-01.png`, `evidence/inventory/stock-transfer-02.png`, `evidence/inventory/stock-transfer-05.png`,
  `evidence/inventory/stock-transfer-06-created.png`, `evidence/inventory/stock-orders-list-after-transfer.png`
- Transfer actions: **Receive stock**, Download PDF, Download CSV, Edit, Cancel order. Evidence: `evidence/inventory/stock-transfer-T1-actions.png`
- Receive: Ordered vs **Received** quantity (auto-fill), fees → receiving less than ordered asks **"Mark order as partially received"**
  (receive rest later) or **"Mark order as completed"** (close with shortfall) → status **"Partial"**.
  Evidence: `evidence/inventory/stock-transfer-T1-receive.png`, `evidence/inventory/stock-transfer-T1-after-receive.png`
- **Stock moved only on receipt and only by the received quantity:** both "received a product transfer" entries (source −2, destination
  +2) are timestamped at receipt (16:50), not creation (16:47). So there's **no "in transit" state**; the source keeps the stock until
  the destination receives. Evidence: `evidence/inventory/product-stock-history-after-transfer.png`
- Manual alternative (also tested): Remove at source (reason Other + description) and Add at destination (reason "Transfer"), which
  creates **two unlinked adjustments**. Evidence: `evidence/inventory/product-stock-history-03.png`

### Purchases and suppliers

- Suppliers: name, description, contact first/last name, 2 phones, email, website, physical and postal address.
  Evidence: `evidence/inventory/supplier-add.aria.txt`
- `Stock orders → Add → **Add new order**` (purchase order) requires a supplier ("No suppliers created yet"). A purchase order was
  **not** placed. The receive flow for transfers is the same screen family. Evidence: `evidence/inventory/stock-orders-01.png`

### Stock counts (stocktake)

`Stocktakes → Start now` → select location → name/description → **Count products** (Expected vs Counted, quick-scan counting with
barcode scanner, **Pause**, progress %, activity feed) → **Review** (tabs All / Uncounted / **Unmatched** / Matched / Excluded;
Difference, Cost) → **Complete** ("This action cannot be undone", optional note) → summary (started/completed, **counted by, reviewed
by**, location, differences). Tested: expected 16, counted 15 → −1 (−SGD 5).
Evidence: `evidence/inventory/stocktake-01.png`, `evidence/inventory/stocktake-03-counting.png`, `evidence/inventory/stocktake-04-review.png`,
`evidence/inventory/stocktake-05-complete.png`

### Product sales

- Products sold in the POS (Products tab shows stock at the sale's location). Selling reduced stock at that location ("Aung made a
  sale (−1)"), and **voiding returned it** ("made a return (+1)"). Product commission was calculated (40% × 15 = SGD 6).
  Evidence: `evidence/walk-in/quick-sale-03-cart.png`, `evidence/payroll/pay-run-breakdown-after-product-sale.png`

### Low-stock alerts

- Per-location low stock level and "Receive low stock notifications". Staff notification preferences include **Low stock alerts** and
  a **weekly Low stock summary** (push / in-app). Evidence: `evidence/inventory/product-add-filled.png`, `evidence/notifications/notification-settings.png`

### Inventory reports (catalogue)

- Stock on hand, Stock movement summary, Stock movement log, Product list, Ordered stock (see `reports.md`).

## USER-PROVIDED

- Planned: **branch-level stock** and **stock transfers** (brief §26).

## INFERRED

- Because the source stock only drops at receipt, stock "in transit" is counted at the source until received.

## NOT VERIFIED

- A low-stock alert actually firing (stock never reached the threshold of 3).
- Purchase orders from a supplier (no order placed); supplier invoices / costs.
- Product import (template observed, no import run). See `import-export.md`.
- Online product store / shop orders.

## Notes for the gap analysis

- Fresha matches our planned branch-level stock and transfers, and adds partial receipt, stocktakes with review, supplier
  purchase orders and per-location reorder levels.
- Stock usage by barbers during services is manual in Fresha.
