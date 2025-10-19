# Automated ERPNext Environment Setup

This repository now ships with `automated_install.sh`, a non-interactive provisioning script that installs a fully configured
Frappe/ERPNext stack (Frappe, ERPNext, and Payments) and completes the ERPNext setup wizard automatically. The script targets
fresh Ubuntu 22.04 / 24.04 hosts and expects to be run as `root`.

## What the script does

- Installs all required system packages including MariaDB, Redis, Node.js 18, Yarn, wkhtmltopdf, Nginx, and Supervisor.
- Creates a dedicated Linux user (default `frappe`) and bootstraps a bench at `~/frappe-bench` on the specified Frappe branch
  (defaults to `version-15`).
- Fetches the ERPNext and Payments apps, creates the default site, and installs both applications.
- Runs the ERPNext setup wizard headlessly through `bench --site <site> execute erpnext.setup.install.setup_complete` so the
  environment is ready for immediate use without any browser interaction.
- Configures production services (`bench setup production`) and maps the site hostname to `127.0.0.1`.

## Usage

```bash
sudo ./automated_install.sh
```

Key parameters (override by exporting before running the script):

| Variable | Purpose | Default |
| --- | --- | --- |
| `BENCH_USER` | System user that owns the bench | `frappe` |
| `SITE_NAME` | Hostname for the default site | `erpnext.local` |
| `MYSQL_ROOT_PASSWORD` | MariaDB root password | `root` |
| `ADMIN_PASSWORD` | ERPNext Administrator password (also used for setup wizard) | `admin` |
| `COMPANY_NAME` / `COMPANY_ABBR` | Company created during wizard | `Example Corp` / `EX` |
| `FRAPPE_BRANCH`, `ERPNEXT_BRANCH`, `PAYMENTS_BRANCH` | Git branches to check out | `version-15` |
| `COMPANY_COUNTRY`, `COMPANY_TIMEZONE`, `COMPANY_CURRENCY` | Regional defaults | `United States`, `Etc/UTC`, `USD` |

After the script finishes, access the site at `http://<SITE_NAME>` (default `http://erpnext.local`). The Administrator credentials
are `Administrator` / value of `$ADMIN_PASSWORD`.
