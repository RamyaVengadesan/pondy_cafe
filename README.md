# Pondy Café POS

A café point-of-sale (POS) and operations management system built with **PHP, MySQL, HTML, CSS, and vanilla JavaScript**. Designed for day-to-day café counter workflows, it brings order taking, GST billing, kitchen tickets, inventory, staff permissions, cash shifts, customer loyalty, and reporting into one application.

The project can run locally with XAMPP and does not require a frontend build step.

## Features

### Point of sale and orders
- Searchable, touch-friendly menu for counter billing.
- Dine-in, takeaway, and delivery order types.
- Hold and resume open orders.
- Table/floor view with table transfers.
- Item notes for preparation instructions.
- Kitchen Order Tickets (KOT) issued in rounds and grouped by preparation station.
- Manager approval for cancelling items that have already been sent to the kitchen.

### Billing, GST, and payments
- Item-level GST rates with CGST and SGST calculations.
- GST-inclusive or GST-exclusive menu pricing.
- Percentage and fixed-value discounts with reasons and approval limits.
- Cash payments with change calculation, UPI, card, and split payments.
- UPI QR support for the exact amount due.
- Financial-year-based invoice numbering.
- Invoice void workflow and GST/sales summaries.
- Optional service charge and bill round-off.

> **Important:** Tax rules and invoice requirements depend on the business and applicable regulations. Configure the café's details and GST settings correctly, and confirm the setup with your accountant before using the system for real transactions.

### Inventory and stock
- Ingredient and ready-to-sell item tracking.
- Recipes that deduct ingredient quantities when an order is billed.
- Stock purchases, waste records, stock counts, and stock history.
- Automatic stock checks for tracked items and sold-out handling for piece-counted products.

### Staff, shifts, and security
- Cashier, manager, and owner roles.
- PIN-based sign-in and first-login PIN change.
- Failed-login lockout.
- Manager approvals for restricted actions.
- Cash-drawer shifts with opening cash, expenses/petty cash, closing cash, and variance.
- Activity log for operational traceability.

### Customers and loyalty
- Customer lookup by phone number.
- Visit and spending history.
- Loyalty points earned and redeemed.
- Favourite-item information where recorded.

### Reports and exports
- Dashboard and sales summaries.
- Sales by time period, payment method, category, and staff.
- Best-selling items and estimated food-cost reporting.
- GST summary by tax rate and voided invoice checks.
- CSV exports for further analysis and accounting workflows.
- X and Z shift reports.

### Devices and printing
- Responsive interface for counter PCs, tablets, and phones.
- Browser-based receipt and kitchen-ticket printing.
- Locally bundled fonts so the interface can work without fetching fonts from the internet.

## Technology stack

- **Frontend:** HTML, CSS, vanilla JavaScript
- **Backend:** PHP
- **Database:** MySQL / MariaDB
- **Local development:** XAMPP (Apache and MySQL)
- **Testing:** Python, Node.js, PHP, and shell scripts

## Project structure

```text
pondy_cafe/
├── index.html                 # Main application shell
├── config.php                 # Database and application configuration
├── api/
│   ├── index.php              # JSON API entry point
│   ├── handlers/              # Authentication, orders, billing, stock, reports, etc.
│   └── lib/                   # Shared API and billing logic
├── assets/
│   ├── css/                   # Application styles and local font styles
│   ├── fonts/                 # Locally bundled font files
│   └── js/
│       ├── app.js             # Frontend application/router
│       ├── api.js              # API client
│       ├── calc.js             # Browser-side bill calculations
│       ├── views/              # Individual application screens
│       ├── pay.js              # Payment interface
│       └── print.js            # Receipt and ticket printing
├── database/
│   ├── schema.sql              # Database schema
│   ├── seed.sql                # Sample data
│   ├── backup.bat              # Windows database backup helper
│   └── backup.sh               # Linux/macOS database backup helper
└── tests/
    ├── api_test.py             # API workflow tests
    ├── parity_test.sh          # JavaScript/PHP calculation parity checks
    └── run_all.sh              # Test runner
```

## Requirements

For the recommended local Windows setup:

- Windows
- XAMPP with Apache, PHP, and MySQL/MariaDB
- A modern browser such as Chrome or Edge

For running the automated test suite, you also need Python 3, Node.js, PHP, MySQL/MariaDB, and a Bash-compatible shell.

## Installation on Windows with XAMPP

1. Install XAMPP.
2. Start **Apache** and **MySQL** in the XAMPP Control Panel.
3. Copy the `pondy_cafe` folder into the XAMPP web root:

   ```text
   C:\xampp\htdocs\pondy_cafe\
   ```

4. Open phpMyAdmin:

   ```text
   http://localhost/phpmyadmin
   ```

5. Import `database/schema.sql`, then import `database/seed.sql`.
6. Check the database values in `config.php`. The default configuration expects a local database named `pondy_cafe` and the standard XAMPP `root` account with an empty password.
7. Open the application:

   ```text
   http://localhost/pondy_cafe/
   ```

### Linux or macOS

From the project directory, with PHP and MySQL/MariaDB installed, create the database using the SQL files:

```bash
mysql -u root < database/schema.sql
mysql -u root < database/seed.sql
```

Then configure Apache/Nginx with PHP, or use PHP's built-in server for local development:

```bash
php -S localhost:8080
```

Open `http://localhost:8080/`. Use a suitable web-server configuration for any deployment beyond local development.

## Sample sign-in accounts

The seed database is intended for initial setup and testing. The documented starting accounts are:

| Account | Initial PIN | Role |
|---|---:|---|
| Owner | `1234` | Full access |
| Manager | `2222` | Management tasks and approvals |
| Counter | `0000` | Billing, tables, and customer workflows |

Users are prompted to change their PIN on first sign-in. These are **sample credentials only**. Replace or disable sample accounts before using the application with real business data, and never publish real credentials.

## First-time setup checklist

1. In **Settings → Café & bill**, configure the café name, address, phone, FSSAI details, and GSTIN as applicable.
2. In **Settings → GST & pricing**, choose whether menu prices include GST.
3. In **Settings → UPI & loyalty**, configure the café's UPI ID and loyalty options.
4. Replace sample menu items and prices with the actual menu.
5. Add recipes for ingredients that should be deducted from stock.
6. Enter accurate opening stock.
7. Configure receipt and kitchen-ticket printing, then print test copies.
8. Open a cash-drawer shift with the actual opening cash.
9. Complete a test order and verify the bill, payment, stock movement, and reports before going live.

## Typical daily workflow

1. A cashier signs in and opens a shift with the counted opening cash.
2. For dine-in, select a table, add items, and send the order to the kitchen.
3. For takeaway or counter sales, create an order from the billing screen.
4. Review the bill, apply any permitted discount, record payment, and print the receipt.
5. At the end of the shift, resolve open orders, count the drawer, close the shift, and review the closing report.

## Printing

Printing uses the browser's print functionality. A thermal printer with an installed operating-system driver can be configured for the supported paper width in Settings.

For a dedicated kitchen printer, the kitchen can use a separate browser/device connected to the same application, subject to the local network and printer setup. Silent printing depends on browser configuration; for example, Chrome or Edge kiosk-printing mode may be suitable for a dedicated counter machine.

## Configuration

The database connection and application settings are defined in `config.php`. The application supports the following environment variables for database configuration:

- `PONDY_DB_HOST`
- `PONDY_DB_NAME`
- `PONDY_DB_USER`
- `PONDY_DB_PASS`

The configured timezone is `Asia/Kolkata`.

For any non-local deployment, use a dedicated database user with a strong password, keep debug output disabled, use HTTPS, and configure the web server to prevent access to configuration files and internal directories.

## Running tests

**Warning:** The test runner recreates the `pondy_cafe` database and imports the schema and seed data. Run it only against a disposable test database/environment. Do not run it against a live café database.

The test runner requires PHP, MySQL/MariaDB, Python 3, Node.js, and a Bash-compatible shell. From the project directory:

```bash
tests/run_all.sh
```

The test suite covers API workflows such as authentication, lockout, orders, KOT, GST calculations, split payments, stock, loyalty, invoice voiding, shift closing, reports, and exports. The calculation parity test compares the JavaScript and PHP billing calculators across **5,000 generated test bills**.

## Backups

Back up the database regularly and store copies somewhere other than the till computer.

- Windows: run `database/backup.bat`.
- Linux/macOS: run `database/backup.sh`.

Review the scripts and database credentials for your environment before scheduling them. Periodically test that a backup can be restored.

## Security notes

- Keep the application on a trusted local network unless it has been properly hardened for remote access.
- Use HTTPS whenever traffic leaves the local machine/network.
- Configure a dedicated database account rather than using the MySQL root account on a production server.
- Replace sample staff accounts and PINs.
- Keep backups protected and test restoration.
- Review web-server access rules when using a server other than Apache.
- Do not commit production credentials, real customer data, database backups, or secrets to GitHub.

## Limitations and deployment notes

- The project is designed for local café operations; internet-facing production use requires an appropriate security and deployment review.
- Browser-based printing and device-specific printer behavior must be tested with the actual hardware.
- GST configuration and reports are operational aids and should be reviewed against the café's actual tax obligations.
- Test the workflows and backup/restore process with sample data before using the system for real sales.

## License

No license is specified here. Add a `LICENSE` file before presenting the project as open source, and choose a license that matches how you want others to use, modify, and distribute it.

## Acknowledgements

- Fraunces and DM Sans fonts are bundled locally and distributed under the SIL Open Font License.
- Icons use Lucide (ISC).
- QR-code functionality uses qrcode-generator by Kazuhiko Arase (MIT).
