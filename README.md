# ReelTrack

A local-first, consent-based Instagram campaign link manager.

## Included
- Admin sign-in and session protection
- Create, list, pause and delete campaign links
- Unique visitor URLs and click tracking
- Visitor landing page with clear consent
- Collects only voluntarily submitted Instagram username and optional contact email
- Admin visitor table, campaign analytics and CSV export
- SQLite storage (no database service required for local testing)

## Important privacy boundary
This app does **not** ask for, capture, verify, or store Instagram passwords, one-time codes, cookies, or session tokens. It does not impersonate Instagram or provide account takeover. The visitor page clearly identifies itself as ReelTrack. Instagram profile links open public profiles only.

## Run on Windows
1. Install Python 3.11+.
2. Open PowerShell in this folder.
3. Create a virtual environment:
   ```powershell
   py -m venv .venv
   .venv\Scripts\Activate.ps1
   ```
4. Install dependencies:
   ```powershell
   pip install -r requirements.txt
   ```
5. Copy `.env.example` to `.env`, then change the admin password and session secret.
6. Start:
   ```powershell
   uvicorn main:app --reload
   ```
7. Visit http://127.0.0.1:8000

Default local login if you have not configured environment variables:
- Username: `admin`
- Password: `ChangeMe-Now-123!`

Change these immediately. For deployment, set environment variables in the hosting provider and use HTTPS.

## Meta integration
The app includes a safe integration boundary, not a fake Instagram login. To add official account connection, register a Meta developer app, configure its OAuth redirect URI and use only the permissions approved for your app and account type. Do not request passwords from visitors. Meta permissions and review requirements can change; check current Meta developer documentation before enabling OAuth.

## Production checklist
- Use HTTPS and a strong unique admin password.
- Set a long random SESSION_SECRET.
- Use a managed database with backups for multi-instance hosting.
- Add a privacy notice, retention period, consent withdrawal process and contact details.
- Restrict admin access; enable MFA at the hosting/identity layer.
- Configure rate limiting, monitoring and backups.
- Do not store access tokens unless strictly necessary; encrypt them and request minimum scopes.
