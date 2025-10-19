# ERPNext Environment Setup

This repository was used to provision a Frappe/ERPNext v15 development environment inside the codespace container. The following key tasks were executed:

- Ran `erpnext_install.sh` and selected ERPNext Version 15 with MariaDB root password `root`.
- Installed Node.js 20, Yarn 1.22, Bench CLI 5.25.11, and cloned Frappe/ERPNext version-15 branches.
- Created a new bench at `~/frappe-bench` and set up the default site `site1.local`.
- Installed ERPNext 15.83.2 on the site and verified with `bench --site site1.local list-apps`.
- Started the bench (`bench start`) and completed the ERPNext setup wizard via the browser (language English, timezone Etc/UTC, currency USD, country United States). Company configured as Example Corp (abbr. EX) with administrator Test User (`test.user@example.com`).

The Administrator login remains `Administrator` / `admin`.

Bench commands for verification:

```bash
source ~/frappe-bench/env/bin/activate
bench version
bench --site site1.local list-apps
```
