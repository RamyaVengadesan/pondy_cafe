# Pondy Café — Billing System

A billing and day-to-day management app for a café. It runs locally with XAMPP, so the counter can keep working without relying on a cloud service. The app uses PHP, MySQL, and plain JavaScript.

## Features

- **Billing:** Search the menu, add item notes, hold orders, and handle dine-in, takeaway, or delivery.
- **Tables:** View occupied tables and move an order to another table.
- **Kitchen tickets:** Send orders to the kitchen in rounds and print tickets by station.
- **GST bills:** Calculate CGST and SGST, with inclusive or exclusive menu pricing.
- **Payments:** Cash, UPI QR, card, or split payments.
- **Discounts:** Apply fixed or percentage discounts, with manager approval when required.
- **Staff:** Cashier, manager, and owner roles; PIN login; first-login PIN change; and lockout after repeated failed attempts.
- **Cash drawer:** Record opening cash, payouts, closing cash, and differences.
- **Stock:** Track ingredients and ready-to-sell items. Recipes can deduct ingredients when an order is billed.
- **Customers:** Look up customers by phone number and track visits, spending, and loyalty points.
- **Reports:** Review sales, payment methods, best-selling items, GST summaries, and export data to CSV.

## Built with

- PHP
- MySQL / MariaDB
- HTML, CSS, and vanilla JavaScript
- XAMPP for local development

## Run it locally (Windows)

1. Install [XAMPP](https://www.apachefriends.org/) and start **Apache** and **MySQL**.
2. Copy the `pondy_cafe` folder into `C:\xampp\htdocs\`.
3. Open `http://localhost/phpmyadmin`.
4. Import `database/schema.sql`, then import `database/seed.sql`. These files create the `pondy_cafe` database and sample data.
5. Visit `http://localhost/pondy_cafe/`.

The database settings are in `config.php`. The default setup is for a local XAMPP installation using MySQL user `root` with an empty password. For another environment, update the configuration or set the `PONDY_DB_*` environment variables.

## Sample accounts

| User | Initial PIN | Role |
|---|---:|---|
| Owner | `1234` | Full access |
| Manager | `2222` | Management tasks and approvals |
| Counter | `0000` | Billing, tables, and customers |

These are only seed-data accounts. Change the PINs and disable sample accounts before using the app for real sales.

## Before using it in a café

- Add the café's details and applicable FSSAI/GST information in Settings.
- Check the GST and menu pricing settings.
- Add your own menu items and prices.
- Set up UPI if you want to accept UPI payments using the QR screen.
- Add recipes and opening stock for items you want to track.
- Test receipt and kitchen-ticket printing.
- Make a test order and check the bill, payment, stock, and reports.

## Printing

The app uses the browser's print function, so configure the printer in the operating system first. Thermal printers should be tested with the paper width you plan to use. Chrome or Edge kiosk-printing mode can be used on a dedicated counter PC if you want to avoid the print dialog.

## GST note

The GST settings and reports need to match the café's actual tax setup. Check rates and invoice details with your accountant before using the app for real transactions. The GST report is a summary for reference; it does not file a tax return.

## Backups and security

- Back up the database regularly using `database/backup.bat` on Windows or `database/backup.sh` on Linux/macOS.
- Keep backup files somewhere other than the counter computer.
- Do not publish real credentials, customer records, or database backups on GitHub.
- The included setup is intended for local use. Before exposing it to the internet, review the server configuration, HTTPS, database permissions, and access rules.

## Project structure

```text
pondy_cafe/
├── index.html
├── config.php
├── api/
│   ├── index.php
│   ├── handlers/
│   └── lib/
├── assets/
│   ├── css/
│   ├── fonts/
│   └── js/
├── database/
│   ├── schema.sql
│   ├── seed.sql
│   └── backup scripts
└── tests/
```

## Run the tests

The test script uses a test database and resets the `pondy_cafe` database, so **do not run it against a database containing real café data**.

```bash
tests/run_all.sh
```

The tests cover API workflows and compare the JavaScript and PHP bill calculations across 5,000 generated test bills. The test runner needs the relevant PHP, MySQL, Python, Node.js, and Bash tools installed.

## Credits

- Fraunces and DM Sans fonts (SIL Open Font License)
- Lucide icons (ISC)
- qrcode-generator by Kazuhiko Arase (MIT)
