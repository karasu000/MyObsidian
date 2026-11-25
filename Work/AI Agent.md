### Exact(export .xlsx table - working):
Role: Autonomous browser agent for Nalog.nl.
Goal: Log into Exact Online, switch to Nalog.nl administration, download the open items Excel report, and upload it to Easy CRM.

Inputs:
- Exact Login URL: https://start.exactonline.nl/
- Direct URL to Nalog.nl Administration: https://start.exactonline.nl/docs/MenuPortal.aspx?_Division_=139623
- Exact Login / Email: ict@nalog.nl
- Exact Password: Herenstraat100)
- Endpoint to retrieve the 2FA code (HTTP GET): https://fiscaal-api.nalog.nl/api/code
- CRM API Key: 6f4473c0644d5e8c12bfdbc341cafb0bf479a341
- Output File: /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx

Steps:
0. Browser Visibility: Run the browser in visible (headed, non-headless) mode in the foreground, performing real UI clicks and typing with a brief pause (~0.5–1s) between actions so the process is visually observable on screen.
1. Open Exact Login URL and sign in with Exact Login and Exact Password.
2. If prompted for 2FA, send an HTTP GET request to 2FA Endpoint, extract the 6-digit code, and submit it. If an account/workspace selector appears, choose Nalog.nl.
3. Check the active company name in the top bar. If it is not Nalog.nl B.V., open Nalog.nl Admin URL and wait for full load.
4. Navigate via the top menu: Verkoop -> Openstaande posten overzicht. Do not use direct URLs for this report.
5. Click the three-dots actions icon (...) in the top-right corner of the report frame -> Export: Excel -> select "Alle pagina's".
6. Wait 5 seconds for the download to finish. Playwright saves the exported file with a UUID filename (without an extension) inside /Users/admin/.openclaw/tmp/playwright-artifacts-*/.
7. Run a shell command to copy the newest file from /Users/admin/.openclaw/tmp/playwright-artifacts-* (modified within the last 2 minutes, size > 0) to /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx:
   cp "$(ls -t /Users/admin/.openclaw/tmp/playwright-artifacts-*/* 2>/dev/null | head -n 1)" /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx
8. Upload the saved Excel file to Easy CRM exactly once by running:
   python3 /Users/admin/.openclaw/workspace/upload_debtors.py /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx "6f4473c0644d5e8c12bfdbc341cafb0bf479a341"

Rules & Output:
- Never modify data, delete records, or send emails in Exact Online.
- Upload the file to CRM only ONCE per run (each successful upload creates a new report).
- Verify /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx exists and size > 0 bytes before uploading.
- Return: local .xlsx path, file size, CRM upload response (upload ID and full report URL), timestamp, and step statuses.
  
  
  
  
  
  
  
mkdir -p /Users/admin/.openclaw/worker /Users/admin/.openclaw/workspace/exports

cat << 'EOF' > /Users/admin/.openclaw/worker/.env
# --- Worker & OpenClaw ---
WORKER_ID=mac-mini-5
POLL_INTERVAL_SEC=10
OPENCLAW_AGENT_ID=fiscaal-auto
SCREEN_INDEX=1

# --- PostgreSQL Database ---
DB_HOST=167.235.114.245 
DB_PORT=54320
DB_NAME=postgres
DB_USER=nalog
DB_PASSWORD=Herenstraat100)

# --- Wasabi S3 (Докази виконання) ---
S3_ENDPOINT=https://s3.eu-central-1.wasabisys.com
S3_BUCKET=agent-steps-record
S3_ACCESS_KEY=847K8VDHLH3LBZKO9QFM
S3_SECRET_KEY=2b1zeeTZCQhez0HP8gcFJPmMkvMEB6Kz1gCcpEP5

# --- Задача 1: Exact Online + Easy CRM ---
EXACT_LOGIN_URL= https://start.exactonline.nl/docs/Login.aspx
EXACT_ADMIN_URL= https://start.exactonline.nl/docs/MenuPortal.aspx?_Division_=139623
EXACT_LOGIN=ict@nalog.nl
EXACT_PASSWORD=Herenstraat100)
EXACT_2FA_URL=https://fiscaal-api.nalog.nl/api/code
CRM_API_KEY=6f4473c0644d5e8c12bfdbc341cafb0bf479a341

# --- Задача 2: Fiscaal (Machtiging) ---
FISCAAL_URL=https://start.fiscaalgemak.nl/
FISCAAL_LOGIN=ict@nalog.nl
FISCAAL_PASSWORD=Herenstraat100)
EOF

chmod 600 /Users/admin/.openclaw/worker/.env




INSERT INTO public."tasks-query" (task_type, payload)
VALUES (
    'fiscaal_machtiging_activate',
    '{"bsn": "123456789", "activation_code": "XXXX-XXXX", "client_name": "Ім''я Клієнта", "machtiging_type": "VIA doorlopend", "year": ""}'::jsonb
);