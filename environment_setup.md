# ERPNext Environment Setup

This repository was used to provision a Frappe/ERPNext v15 development environment inside the codespace container. The following key tasks were executed:

- Ran `erpnext_install.sh` and selected ERPNext Version 15 with MariaDB root password `root`.
- Installed Node.js 20, Yarn 1.22, Bench CLI 5.25.11, and cloned Frappe/ERPNext version-15 branches.
- Created a new bench at `~/frappe-bench` and set up the default site `site1.local`.
- Installed ERPNext 15.83.2 on the site and verified with `bench --site site1.local list-apps`.
- Completed the ERPNext setup wizard via the command line (language English, timezone America/New_York, currency USD, country United States). Company configured as Example Corp (abbr. EX) with administrator Test User (`test@example.com`).
- Installed the `repair_portal` app (main branch) from `https://github.com/ArtisanClarinets/repair_portal.git` and ran its seed routines. The installer reports deferred records for optional reference data (e.g. instrument models and departments) until the `MRW Artisan Instruments` company exists; these messages are informational and do not block the app installation.
- Warmed the bench caches by re-running `bench setup requirements --node`, `bench setup requirements --python`, and `bench build`, then clearing desk caches so the desk UI loads quickly whenever the container restarts.

The Administrator login remains `Administrator` / `admin`.

Bench commands for verification:

```bash
source ~/frappe-bench/env/bin/activate
bench version
bench --site site1.local list-apps
```
