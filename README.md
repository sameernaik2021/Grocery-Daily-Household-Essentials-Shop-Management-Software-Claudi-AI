# Kirana Maal — Grocery & Daily Household Essentials Shop Management

A lightweight, single-file web application for managing a किराना माल (Kirana Maal) shop. It is built with **HTML5, CSS, and vanilla JavaScript** and uses browser `localStorage` for local persistence.

## Project files

- `kirana-maal.html` — the complete application (HTML, CSS, and JavaScript in one file).
- `README.md` — this documentation.

## Requirements

- A modern browser such as Firefox, Chrome, Edge, or Chromium.
- No package manager, server, framework, API key, or internet connection is required to open the saved HTML file.

## Getting started

1. Download and extract `Kirana-Maal-Software.zip`.
2. Open `kirana-maal.html` in your browser.
3. Use the navigation menu to access Dashboard, Inventory, Sales & Billing, Purchases / Stock In, Customer Khata, Suppliers, Reports, and Data & Settings.
4. Data is saved in the current browser profile using `localStorage`.

> **Tip:** Keep the HTML file and exported backups in a safe folder. Clearing browser data may remove the application's saved records.

## Features

### Dashboard
- Summary metrics for sales and inventory.
- Low-stock alerts and expiry reminders.
- Recent bills and category-level stock information.

### Inventory
- Search and filter products.
- Add and edit products.
- Track product category, unit, purchase price, selling price, stock, reorder level, supplier ID, expiry date, and barcode.
- Import and export product data using CSV.

### Sales & Billing
- Add products to a billing cart.
- Validate requested quantities against available stock.
- Apply a discount and choose a payment method.
- Save bills, deduct stock, and print receipts.

### Purchases / Stock In
- Record incoming stock and purchase details.
- Increase inventory quantities and update recorded cost/supplier details.

### Customer Khata
- Use fictional customer records for demonstrations.
- Record credit sales and repayments and view outstanding balances.

### Suppliers
- Maintain a supplier directory using sample supplier information.

### Reports & Insights
- Review inventory valuation, sales/payment summaries, and reorder suggestions.
- Export supported sales, purchase, customer, and product data to CSV.

### Data & Settings
- Export a JSON backup and restore from a JSON backup.
- Configure the shop name and available settings.
- Reset sample data when needed. **Back up first**, because reset/restore actions can replace current browser data.

## Synthetic data

The application seeds **500 synthetic product records**, with IDs `K001`–`K500`. The first 50 follow product examples and product families in the supplied dataset where available; the additional records are generated examples.

The sample data may include fictional customers and suppliers, bills, and Khata balances to demonstrate workflows. **All synthetic prices, quantities, dates, customers, suppliers, and transactions are for testing only. They are not actual shop records or verified market prices.**

The product data model includes:

- Product ID and product name
- Category and unit
- Purchase price (INR) and selling price (INR)
- Stock quantity and reorder level
- Supplier ID and expiry date
- Barcode, where present

## Business logic and limitations

- **Reorder suggestions:** use a simple rule, `max(0, 2 × reorder level − current stock)`. This is a heuristic, not a trained AI demand forecast.
- **Estimated gross profit:** based on recorded selling price and unit cost, adjusted for bill discount. It does not account for operating expenses and may not represent final accounting profit.
- **GST:** the setting does not make this a tax-compliant billing system. Verify and implement applicable tax rules before real business use.
- **Storage:** `localStorage` is tied to the browser profile and device. It is not a shared database, is not encrypted by this app, and does not synchronize across devices or users.
- **Concurrency:** this local prototype is not designed for multiple cashiers or simultaneous multi-device updates.
- **Production readiness:** it is a prototype for demonstration and testing, not a replacement for audited accounting, compliant invoicing, or a secured production system.

## CSV import and export

Product CSV import expects a header row with at least:

- `Product_Name`
- `Selling_Price_INR`
- `Stock_Quantity`

Optional recognized columns include `Product_ID`, `Category`, `Unit`, `Purchase_Price_INR`, `Reorder_Level`, `Supplier_ID`, `Expiry_Date`, and `Barcode`.

Existing matching product IDs may be updated; new IDs may be inserted. Test imports with a backup first. Exported CSV files can be opened in spreadsheet software.

## Smoke tests

These are practical checks to perform after opening the app; they are not a claim of exhaustive automated or cross-browser testing.

1. **Diagnostics:** Open browser developer tools, select Console, and run:

   ```javascript
   KiranaMaalDiagnostics.run()
   ```

   Review the diagnostic output for seeded product count, unique IDs, non-negative inventory, sales initialization, and CSV escaping.

2. **Persistence:** Add or edit a product, reload the page, and confirm the change remains.
3. **Sale and stock:** Complete a small test sale and verify stock decreases and the bill appears in history.
4. **Insufficient stock:** Attempt to sell more than the available quantity and confirm the transaction is blocked.
5. **Purchase:** Record a stock-in purchase and confirm inventory increases.
6. **Khata:** Make a test credit sale and record a repayment.
7. **Backup/restore:** Export a JSON backup, make a test change, and restore the backup.
8. **CSV:** Export products and test importing the CSV into a test copy of the data.

Keep a backup before testing reset, import, or restore actions.

## Troubleshooting

- **Data appears missing:** Check that you opened the app in the same browser profile and have not cleared site/browser data. Restore a previously exported JSON backup if available.
- **Changes do not persist:** Ensure the browser permits local storage for local files. Browser behavior for `file://` storage can vary; if needed, test in another supported browser or run a simple local static file server.
- **A CSV import fails:** Confirm that the required column headers are present and that numeric price and quantity fields contain valid values.
- **Printing looks different:** Use the browser's print preview and adjust paper size, margins, or scale.

## Privacy and backup recommendations

Do not enter sensitive personal, financial, card, UPI, or authentication information into this prototype. Export JSON backups regularly and store them securely. For real operations, use authenticated access, role-based permissions, a transactional database, audit logging, tested backups, concurrency controls, and professionally validated tax/invoice logic.

## License and data notice

No separate software license is specified here. The included sample dataset is synthetic and intended for development, training, and testing.
