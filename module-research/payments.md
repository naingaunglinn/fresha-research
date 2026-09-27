# Payment / Checkout / Sales: Fresha research

> **Environment.** Sandbox "Baber Shop" (trial, Singapore/SGD), 2026-09-27. Sales performed: #1 (walk-in appointment, split Cash +
> KBZPay, tip) → Refund #2; #3 (quick sale service + product, cash); #4 (same-day appointment, KBZPay); #5 (quick sale with 10% cart
> discount, KBZPay) → **voided**. See `test-data-log.md` rows 9–12, 24, 33, 35, 36. Amounts are in SGD because of the sandbox.
> MMK amounts and rounding are **NOT VERIFIED**.

## Navigation

- Checkout from an appointment (**Checkout** / **Pay now**), from the calendar (**Add → Sale / Quick payment**), or `Sales → Add new`.
- `Sales → Daily sales summary | Register | Appointments | Sales | Payments | Sold items | Gift cards sold | Packages sold |
  Memberships sold | Product orders`.
- `Settings → Sales` (Pay now, Tax rates, Receipts, Registers, Tipping, Service charges, Gift cards, **Custom checkout methods**)
  and `Settings → Payments` (Payment policy, Payment methods, Card terminals).

## OBSERVED

### Checkout workflow (Cart → Tip → Payment)

1. **First use only:** point-of-sale intro "Free to use — A point of sale solution… Start now". Evidence: `evidence/payments/checkout-01.png`
2. **Cart:** client or "Leave empty for walk-ins"; items with **Edit** (price, quantity, discounts, **team member**, item total);
   "Add to cart"; **Open options → Add cart discount, Add receipt note, Add service charge, Save as draft, Cancel sale**.
   Evidence: `evidence/payments/checkout-edit-item.aria.txt`, `evidence/payments/checkout-cart-options.png`
3. **Tip:** No tip / 10% / 18% / 25% / Custom (amount or %). The line **"Tip goes to <service provider> — Edit"** appears once a tip is
   chosen. The first render showed the logged-in user ("Select an amount for Naing Aung Linn") before updating to the barber.
   Tip percentages are calculated on the **whole cart including products** (location setting "Tip calculation: All items
   included"). Evidence: `evidence/payments/checkout-02-cart-or-tip.png`, `evidence/payments/checkout-custom-tip.png`
4. **Payment:** methods **Cash, Redeem gift, Split payment, KBZPay (custom), Other**; Fresha methods **Card terminal, Self checkout,
   QR code, Manual card entry**; "**Save unpaid**" / "**Save part-paid**". Evidence: `evidence/payments/checkout-03-payment.png`
5. **Pay now** → sale "Completed", with sale number (**Sale #N**, the same sequence as refunds), payments listed with timestamps.
   Evidence: `evidence/payments/checkout-07-complete.png`

Clicks: appointment checkout with one method ~5 (Checkout, tip, Continue to payment, method, Pay now). A single custom
method (KBZPay) **adds the full amount in one tap**. Evidence: `evidence/booking/same-day-checkout-sale.png`

### Payment methods and custom methods

- Custom checkout methods: list shows Cash (built-in), **KBZPay** (added in this session), Other. **"Add payment method" has only a
  Name field.** Evidence: `evidence/payments/add-custom-payment-method.png`, `evidence/payments/custom-methods-after-kbzpay.png`
- Paying by KBZPay asks only for the amount; **there's no transaction/reference number field**. Evidence: `evidence/payments/checkout-kbzpay-modal.aria.txt`
- Cash: keypad, quick amounts (e.g. SGD 44/45/50/60/100), **"Cash received by <team member>"** (choices: members in this sale, then
  other members). Evidence: `evidence/payments/checkout-split-02-cash-amount.png`, `evidence/payments/checkout-cash-received-by.png`

### Split and partial payment (performed on Sale #1)

`Payment → Split payment → Add payment method → Cash → (received by Aung) → 20 → Add` shows "Payments −SGD 20, To pay SGD 24,
**Save part-paid**". Then `Add payment method → KBZPay → 24 → Add payment` shows "Full payment added" → **Pay now**.
Evidence: `evidence/payments/checkout-split-04-after-cash.png`, `evidence/payments/checkout-split-06-both.png`

### Discounts, service charges, taxes

- **Cart discount:** amount in SGD or %; "Taxes will be recalculated after the discount has been applied"; **no reason or approval
  field**. The sale shows "Items total (excl. discounts)", "Cart discount −SGD 5.50". Evidence: `evidence/payments/cart-discount-form.png`,
  `evidence/payments/sale-5-discount.png`
- Line-item discounts: "Discounts — None available" (needs predefined discount types; not configured).
- Service charges: Settings → Sales → Service charges ("extra charges that you can automatically or manually add during checkout");
  none configured. Evidence: `evidence/settings/sales-service-charges.png`
- Taxes: Settings → Sales → Tax rates ("tax defaults for your entire business or specific locations… groups for multiple taxes");
  none configured; the business setting "Retail prices include tax" / "exclude tax". Evidence: `evidence/settings/sales-tax-rates.png`,
  `evidence/settings/business-details-edit.png`

### Receipts

- Sale options: Refund sale, Edit sale details, Add a note, **Email**, **Print**, **Download PDF**, Void sale.
  Evidence: `evidence/payments/sale-options-menu.png`
- Receipt PDF (Sale 1): business name + address, "Sale 1", date/time, client "Walk-In", item with service time, subtotal, total,
  tips, each payment with timestamp, balance. It uses the **"$" symbol (not "SGD")** and **doesn't print the barber's name**.
  Evidence: `evidence/payments/receipt-sale-1.pdf`
- Receipt settings: show client mobile/email and address, title, 2 custom lines, footer; **receipt sequencing per location**
  (prefix + next number). Evidence: `evidence/settings/sales-receipts.png`, `evidence/branches/location-sales.png`

### Refund (performed: Refund #2 on Sale #1)

`Sale → Open options → Refund sale` → mode **Refund item / Refund amount** → tick items (Haircut 40; tip not refunded) →
Continue → **per original payment**: Payment 1 Cash (refund method Cash, amount, "SGD 20 available to refund", **"Cash refund given
by <team member>"**), Payment 2 KBZPay (refund method **KBZPay or Cash**, "SGD 24 available") → **Reason (required list):** Accidental
charge, Incorrect amount, Duplicate transaction, Item not available, Client's request, Potential fraud, Other → **Issue refund**
→ separate document **"Refund #2"**, original sale status **"Refunded"**.
Evidence: `evidence/payments/refund-01.png`, `evidence/payments/refund-02.png`, `evidence/payments/refund-04-done.png`

### Void (performed on Sale #5)

`Open options → Void sale` → "Void sale? This action is permanent and cannot be undone. Following payments will be deleted: SGD
49.50 paid by KBZPay… **Product stock will be returned to Baber Shop: 1 of ZZTest Pomade**" → **Void** (no reason field) → status
**"Voided"**, activity "Voided by …". Evidence: `evidence/payments/void-sale-modal.png`, `evidence/payments/sale-5-voided.png`

### Edit sale details

- Change **team member per line** and **"payment collected by"** per payment; "Changes will be reflected in all reports". There's no
  client field. Evidence: `evidence/walk-in/edit-sale-details.png`

### Sale records and associations

- Sales list: Sale #, Client, Status, Sale date, **Location**, Tips, Gross total; tabs Sales / Drafts; date presets; Filters;
  **Export PDF / CSV / Excel**. Evidence: `evidence/payments/sales-list-01.png`
- Each sale line carries a **team member**; each payment carries **who took it**; each sale carries its **location**; client or
  "Walk-In". Evidence: `evidence/audit/sale-activity.png`
- Sale activity (last **90 days**): "Sale N created — Completed by …", "SGD X paid by <method> — Payment taken by …",
  "Sale voided — Voided by …". Evidence: `evidence/audit/sale-activity.png`
- **The sale date is the checkout date**, even when an appointment is checked out before its scheduled day.

### Deposits, card payments, pay-later

- **Payment policy (prepayment / deposits, no-show and late-cancellation fees) requires Fresha Payments** ("Start now" onboarding for
  card processing). The cancel and no-show dialogs showed "No policy was applied to this appointment". Evidence:
  `evidence/settings/payments-settings.png`, `evidence/booking/cancel-modal.png`
- "Pay now" (one-tap payment from the appointment panel) is also tied to Fresha payments. Evidence: `evidence/settings/sales-pay-now.png`

## USER-PROVIDED

- Planned payment methods: **Cash + KBZPay** (brief §26); currency **MMK**.

## INFERRED

- KBZPay reconciliation in Fresha relies on staff typing the counted KBZPay total at register close (see `finance.md`). With no
  transaction reference per payment, disputes can't be matched to KBZPay records inside Fresha.

## NOT VERIFIED

- MMK formatting (decimals, thousands separator) and receipt currency symbol in a Myanmar workspace.
- Card terminals, Fresha QR code payments, self checkout (require Fresha Payments; not available/relevant in the sandbox).
- Gift cards, packages, memberships redemption at checkout.
- Tax calculation (no tax configured).
- Emailed receipt content (Email action not used).

## Notes for the gap analysis

- Split payment, part-paid, per-payment "taken by" and refund-by-original-method are all present in Fresha.
- Missing for KBZPay: a reference field and any reconciliation beyond a manual count.
- The receipt omits the barber and uses "$".
