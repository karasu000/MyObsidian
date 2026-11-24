### Exact(export .xlsx table - working):
Role: Autonomous browser agent for Nalog.nl.
Goal: Log into Exact Online, switch to Nalog.nl administration, and download the open items Excel report.

Inputs:
- Exact Login URL: https://start.exactonline.nl/
- Direct URL to Nalog.nl Administration: https://start.exactonline.nl/docs/MenuPortal.aspx?_Division_=139623
- Login / Email: ict@nalog.nl
- Password: Herenstraat100)
- Endpoint to retrieve the 2FA code (HTTP GET): https://fiscaal-api.nalog.nl/api/code
- Output Directory: /Users/admin/.openclaw/workspace/exports

Steps:
0. Browser Visibility: Always run the browser in visible (headed, non-headless) mode with the window brought to the foreground, performing real UI clicks and typing with a brief pause (~0.5–1s) between actions so the entire process is visually observable on screen.
1. Open Login URL and sign in with Login and Password.
2. When prompted for 2FA, send an HTTP GET request to 2FA Endpoint, extract the 6-digit code, and submit it.
3. Check the active company name in the top bar. If it is not Nalog.nl, open Nalog.nl Admin URL and wait for full load.
4. Navigate via the top menu: Verkoop -> Openstaande posten -> Overzicht. Do not use direct URLs for this report.
5. Click the three-dots actions icon (...) in the top-right corner -> Export: Excel -> select "Alle pagina's".
6. Wait 5 seconds for the download to finish. Playwright saves the file with a UUID name (no .xlsx extension) inside /Users/admin/.openclaw/tmp/playwright-artifacts-*/.
7. Run a shell command to create Output Directory if needed, find the most recently modified file in /Users/admin/.openclaw/tmp/playwright-artifacts-* (modified within the last 2 minutes, size > 0), and copy it to /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx.

Rules & Output:
- Never modify data, delete records, or send emails.
- Do not look in ~/Downloads; always retrieve the newest UUID file from /Users/admin/.openclaw/tmp/playwright-artifacts-*.
- Verify /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx exists and size > 0 bytes.
- Return: final .xlsx path, file size in bytes, timestamp, and step statuses.
  
  
  
  Role: Autonomous browser agent for Nalog.nl.
Goal: Log into Exact Online, switch to Nalog.nl administration, download the open items Excel report, and upload it to Easy CRM.

Inputs:
- Exact Login URL: [ВСТАВ_ПОСИЛАННЯ_ВХОДУ_EXACT]
- Nalog.nl Admin URL: [ВСТАВ_ПРЯМЕ_ПОСИЛАННЯ_НА_АДМІНКУ_NALOG]
- Exact Login: [ВСТАВ_ЛОГІН_EXACT]
- Exact Password: [ВСТАВ_ПАРОЛЬ_EXACT]
- 2FA Endpoint (HTTP GET): [ВСТАВ_ПОСИЛАННЯ_НА_2FA_ВІД_ІВАНА]
- Easy CRM Email: [ВСТАВ_EMAIL_ВІД_EASY_CRM]
- Easy CRM Password: [ВСТАВ_ПАРОЛЬ_ВІД_EASY_CRM]
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
   python3 /Users/admin/.openclaw/workspace/upload_debtors.py /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx "[ВСТАВ_EMAIL_ВІД_EASY_CRM]" "[ВСТАВ_ПАРОЛЬ_ВІД_EASY_CRM]"

Rules & Output:
- Never modify data, delete records, or send emails in Exact Online.
- Upload the file to CRM only ONCE per run (each successful upload creates a new report).
- Verify /Users/admin/.openclaw/workspace/exports/debtors_latest.xlsx exists and size > 0 bytes before uploading.
- Return: local .xlsx path, file size, CRM upload response (upload ID and full report URL), timestamp, and step statuses.