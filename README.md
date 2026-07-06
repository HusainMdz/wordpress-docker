# Local WordPress Development Environment

> This directory contains the development infrastructure built to mirror your production WordPress environment.

## Table of Contents

- [Infrastructure Architecture](#infrastructure-architecture)
- [Phase 1: Production Export & Spin-up](#phase-1-production-export--spin-up)
- [Phase 2: Local Import & Setup](#phase-2-local-import--setup)
- [Phase 3: Authentication & 2FA Bypass](#phase-3-authentication--2fa-bypass)

## Infrastructure Architecture

The stack matches the production environment:

- **Web Server:** Nginx `1.24-alpine` (`nginx.conf`)
- **Application Core:** WordPress on PHP `8.3-fpm-alpine` (`uploads.ini`)
- **Database Engine:** MySQL `8.0`
- **Container Orchestration:** `compose.yml`

> **Note**
>
> Match the Nginx, PHP, and MySQL versions in `compose.yml` to your production environment exactly.

---

## Phase 1: Production Export & Spin-up

### 1. Export the Production Site

1. Log in to your production WordPress dashboard.
2. Install and activate the **All-in-One WP Migration** plugin.
3. Export the site as a **File**.
4. Download the generated `.wpress` backup.
   - **All-in-One WP Migration → Export → File → Download**

### 2. Start the Local Docker Stack

From this directory, start the development environment:

```bash
docker compose up -d
```

---

## Phase 2: Local Import & Setup

### 1. Complete the Initial WordPress Setup

1. Open <http://localhost>.
2. Complete the WordPress installation using temporary administrator credentials.

### 2. Import the Production Backup

1. Log in to <http://localhost/wp-admin>.
2. Install and activate the **All-in-One WP Migration** plugin.
3. Navigate to:
   - **All-in-One WP Migration → Import → Import From → File**
4. Upload your `.wpress` backup.
5. Wait for the import to finish, then refresh the page.

---

## Phase 3: Authentication & 2FA Bypass

At this point, your local database matches production.

Use your **production WordPress username and password** to log in.

### 1. Log In Using a Backup Verification Key

1. Open <http://localhost/wp-login.php>.
2. Sign in using your production credentials.
3. When prompted for 2FA, enter one of your previously generated **Backup Verification Keys**.

### 2. Disable the 2FA Plugin

After logging in:

1. Go to **Plugins → Installed Plugins**.
2. Search for your **2FA** plugin.
3. Click **Deactivate**.

> **Tip**
>
> Disabling the 2FA plugin in your local environment prevents authentication prompts while keeping production unaffected.
