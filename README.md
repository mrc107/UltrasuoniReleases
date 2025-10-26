Ultrasuoni → Google Sheets importer

This README walks you through setting up the Apps Script that reads your Gmail label (e.g., ultrasuoni), parses releases + links, and fills a Google Sheet. It also infers what you’re buying from your email replies, marks purchases, and creates a shipping forecast (every 20 records).

What you’ll need

A Google account with Gmail + Drive.

A Gmail label that contains all Ultrasuoni emails.

A Google Sheets file where results will be written.

In the ZIP you received, there are two files:

code.txt → the Apps Script source you’ll paste.

README.txt → these instructions.

1) Gmail: create the label + auto-label rules

In Gmail, in the left sidebar, click More → Create new label.
Name it (e.g.) ultrasuoni.

Create filters to auto-apply this label:

In Gmail search box, click the sliders icon (Show search options).

In From, add the sender(s) you get releases from (e.g. ultrasuonirecord@gmail.com), or other rules you prefer.

Click Create filter.

Tick Apply the label → choose ultrasuoni (or your label).

(Optional) Tick Also apply filter to matching conversations to label old emails.

Click Create filter.

You can add multiple filters for different senders; just ensure they all apply the same label you’ll use in the script.

2) Drive: create the destination Google Sheet

Go to drive.google.com → New → Google Sheets.

Rename the spreadsheet (e.g. “Ultrasuoni Releases”).

(Optional) Create/rename the sheet tab to Releases.

If you skip this, the script will create/use a Releases tab automatically.

3) Apps Script: install and authorize the code

There are two easy ways to add the script. Pick A (container-bound) if you want the menu to live inside the spreadsheet; use B (standalone) if you prefer managing the script separately.

A) Add the script inside the spreadsheet (recommended)

Open your Google Sheet.

Extensions → Apps Script to open the editor.

Delete any placeholder code in Code.gs.

Open the code.txt from the ZIP, copy all, and paste into Code.gs.

Click Save (give the project a name, e.g. “Ultrasuoni Importer”).

Close the editor tab and go back to the spreadsheet (or just refresh the sheet).

You’ll now see a new menu “Releases” at the top of the spreadsheet (it appears after reloading the sheet once).

B) Add as a standalone project

Visit script.google.com → New project.

In Code.gs, paste the contents of code.txt.

Click Save (name it).

The first time you run it, the script will ask you to choose a destination spreadsheet (you can paste a Sheets link/ID).

Standalone mode works fine, but the Releases menu won’t show in your Sheet UI. You’ll run it from the Apps Script editor instead.

4) First run: pick your destination spreadsheet

On first run, the script will prompt you to paste a Google Sheets URL or ID to use as the destination.

If you installed the script inside a spreadsheet, you can just leave it empty to use the current sheet.

The choice is saved per account and can be changed later via the menu:
Releases → Choose destination…

If you’re running via a time-based trigger or without a UI, set the destination once from the spreadsheet UI first.

5) Configure (optional): label / tab names

Inside the code there are a few top constants you can change:

const LABEL = 'ultrasuoni';      // Gmail label to scan
const SHEET_NAME = 'Releases';   // Target sheet tab name
const RUN_EVERY_DAY_AT_HOUR = 9; // Daily trigger time (local)


If your Gmail label isn’t ultrasuoni, update LABEL.

If you want a different sheet tab name, update SHEET_NAME.

6) Authorize and run

In the spreadsheet, go to Releases → Setup (first-time).
This will:

Create the tab (if missing) and header row.

Prompt for destination (if not yet set).

Create a daily trigger at the hour you set.

To import right now, use Releases → Run scan now.

The first time you run any menu command, Google will ask you to authorize the script.
Accept the scopes: Gmail (read), Sheets (write), UrlFetch (to enrich titles/prices), and Triggers.

7) What the sheet will contain

The script produces a table like:

Title — Cleaned release title (prefers real release title, not email subject).

Link 1..N — Links to clips/shop pages (Bandcamp, Hardwax, Clone, etc.).

Release Date — Parsed from the email (and sometimes fetched from a product page).

Price — Parsed from email or product page (when possible).

Qty — Inferred from your replies (e.g., “2x”), or set to 1 if you said “Yes/lo prendo” without a number.

Confirmed — “YES” if your reply indicates you want it, “NO” if you declined; blank if undecided.

Email Date — Date/time of the original release email.

Shipping Date — Computed when you accumulate 20 confirmed records (see below).

Amount — Total price for that 20-record shipment batch.

Preso — An x mark if Confirmed = YES (blank Qty counts as 1).

The sheet is automatically sorted by Release Date (ascending).

8) How your replies turn into “Confirmed” & Qty

The script reads your replies to the email threads:

Positive Italian/English confirmations like “lo prendo”, “confermo”, “ok per me”, “yes” → mark Confirmed = YES.

If you include quantities like “2x”, “qty 2”, “2 copie” → Qty = 2.

If you say “lo prendo” without a number → Qty = 1 by default.

Negative phrases like “no”, “non interessa”, “lascia stare” → Confirmed = NO.

If your reply lacks a URL/title but the incoming email shows a single release, a time-proximity fallback (72h) assigns your “lo prendo” to that release automatically.

You can always edit Qty or Confirmed manually in the sheet — future runs won’t override your manual edits for those cells.

9) Shipping forecast (every 20 records)

The script collects all confirmed releases (Qty considered; blank Qty = 1).

Every 20 units becomes a shipment.

The Shipping Date is the release date of the 20th record in that batch.

The Amount is the sum of prices in that 20-record batch.

These values are written on the row of the 20th item in each batch.

Tip: If a price is missing on some rows, fill it manually and Releases → Run scan now to recompute the Amount totals.

10) Re-running and rescanning

Releases → Run scan now: parse new (unprocessed) emails and refresh the sheet.

Releases → Re-scan all (ignore history): clears the “processed” memory and rebuilds from all labeled emails again (useful if you change parsing rules).

11) Troubleshooting

No “Releases” menu?
Refresh the spreadsheet tab after saving the script. Ensure you installed the script inside the sheet (or run from the Apps Script editor if standalone).

Authorization error:
Run any menu command and follow the Google authorization prompts.

Nothing imported:
Check that the Gmail label name in the script matches your Gmail label, and that emails are labeled correctly.

Titles look odd for Hardwax/Clone:
The script derives clean titles for Hardwax from the URL path (/id/artist/title/) and fetches Clone/CloneDistribution page details when needed.

Destination not set / wrong sheet:
Use Releases → Choose destination… to set or change the spreadsheet.

12) Privacy & scopes

The script:

Reads labeled emails (Gmail read-only).

Writes to the chosen spreadsheet.

Uses UrlFetch to read product pages (for better titles/dates/prices).

Creates a time-based trigger if you run Setup.

Nothing is sent outside your Google account; all parsing runs within Apps Script.

13) Updating the script later

If you receive a new code.txt:

Open Extensions → Apps Script (or the standalone project).

Replace the entire contents of Code.gs with the new version.

Save.

Back in the sheet, refresh and use Releases → Run scan now.

That’s it!

You’re ready. Create your label and filter, paste the code into Apps Script, run Setup, and enjoy a neatly organized release list with auto-buy detection and shipping batches.
