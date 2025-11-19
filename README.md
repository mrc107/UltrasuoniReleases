Ultrasuoni Email Tracker for Google Sheets

A simple automation tool for music collectors. This script connects your Gmail to a Google Sheet to automatically track your vinyl orders and newsletter updates from Ultrasuoni.

It is designed for music lovers who want to organize their collection and incoming releases without manually copying and pasting links from emails.

🎵 What does it do?

Scans your Gmail for specific labels (Orders and News).

Creates a tidy Spreadsheet with tabs for Orders and News.

Extracts Links: Automatically pulls links for Deejay.de, Bandcamp, or other music stores found in your emails.

Finds Release Dates: Reads the subject line of your order emails (e.g., "Coming in November") and fills in the expected release date automatically.

Prevents Duplicates: You can run it as often as you like; it won't add the same link twice.

🛠️ Prerequisites

Before installing, make sure you have the following labels set up in your Gmail.

For Orders: ultrasuoni/ordini/sent

For News: ultrasuoni/news

(See the section below on how to automate this with Gmail Rules)

📧 Setting Up Gmail Filters (Automation)

To make this tool work seamlessly, you should set up "Filters" in Gmail so emails are labeled automatically.

1. Automate "News" Labeling (Incoming)

Use this rule to automatically label newsletters received from the record store.

Open Gmail and click the Search options icon (the sliders to the right of the search bar).

In the From field, enter the store's email address (e.g., ultrasuonirecord@gmail.com).

Click Create filter.

Check the box Apply the label and select ultrasuoni/news (create it if it doesn't exist).

Click Create filter.

2. Automate "Orders" Labeling (Outgoing)

Use this rule to automatically label order emails you send that contain the word "ordino".

Click the Search options icon again.

In the To field, enter the store's email address (e.g., ultrasuonirecord@gmail.com).

In the Has the words field, enter: ordino

Click Create filter.

Check the box Apply the label and select ultrasuoni/ordini/sent (create it if it doesn't exist).

Click Create filter.

Note: Gmail filters are primarily for incoming mail. If the outgoing filter doesn't catch every sent email instantly, you can simply go to your "Sent" folder, search for "ordino", select all, and apply the label manually in bulk.

🚀 How to Install (No Coding Required)

You don't need to download any files or install software on your computer. Everything lives inside your Google Sheet.

Create a new Google Sheet (or open a blank one).

You can type sheets.new in your browser address bar to create one instantly.

In the top menu, click on Extensions > Apps Script.

A new tab will open with a code editor.

Delete any code that is currently there (usually just function myFunction() {...}).

Copy the code from the Code.gs file in this repository.

Paste the code into the script editor window.

Click the Save icon (💾) in the toolbar. Name the project "Ultrasuoni Sync" (or whatever you like).

Refresh your Google Sheet tab (press F5).

You should now see a new menu item called "Ultrasuoni Tools" appear next to "Help" at the top of your sheet.

🖱️ How to Use

Once installed, you control everything from the Ultrasuoni Tools menu.

1. Full Sync (Recommended)

Click: Ultrasuoni Tools > 1. Full Sync (Setup + Orders & News)

What it does:

Checks if the "Orders" and "News" tabs exist (and creates them if missing).

Scans your Gmail for Orders and adds them to the Orders tab.

Scans your Gmail for News and adds them to the News tab.

Note: If you have hundreds of emails, the script might stop after ~4.5 minutes to save progress. Just run it again to continue where it left off.

2. Update Release Dates

Click: Ultrasuoni Tools > 4. Update Release Dates (Orders Only)

What it does:

Goes through your Orders tab.

Reads the email subject associated with that order.

If it finds text like "Coming in January" or "Release: 30 Nov", it writes that date into the MANUAL: Release date column.

3. Sync Orders / News Only

Use these buttons if you only want to update one specific tab to save time.

⚠️ First Run Authorization

The first time you run the script, Google will ask for permission to access your Gmail and Sheets. This is normal.

Click Review Permissions.

Select your Google Account.

You will likely see a scary-looking screen saying "Google hasn't verified this app" (because you just created it!).

Click Advanced (small text on the left).

Click Go to Ultrasuoni Sync (unsafe) at the bottom.

Click Allow.

📝 Notes on Links

The script prioritizes music links in this order:

Bandcamp links

Deejay.de links

Other links (It tries to guess the relevant link if the above two are missing, ignoring generic links like Facebook or Instagram).

Enjoy your organized collection!
