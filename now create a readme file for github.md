# **Ultrasuoni Email Tracker for Google Sheets**

A simple automation tool for music collectors. This script connects your Gmail to a Google Sheet to automatically track your vinyl orders and newsletter updates from **Ultrasuoni**.

It is designed for music lovers who want to organize their collection and incoming releases without manually copying and pasting links from emails.

## **🎵 What does it do?**

1. **Scans your Gmail** for specific labels (Orders and News).  
2. **Creates a tidy Spreadsheet** with tabs for Orders and News.  
3. **Extracts Links:** Automatically pulls links for **Deejay.de**, **Bandcamp**, or other music stores found in your emails.  
4. **Auto-Fetches Titles:** If a link title is missing, it tries to fetch it from the website. If the website blocks the bot (like Discogs/Juno), it smartly generates a readable title from the URL itself.  
5. **Finds Release Dates:** Reads the subject line of your order emails (e.g., "Coming in November") and fills in the expected release date automatically.  
6. **Runs continuously:** If you have hundreds of emails, the script automatically saves its progress and restarts itself until the job is done.

## **🛠️ Prerequisites**

Before installing, make sure you have the following labels set up in your Gmail:

1. **For Orders:** ultrasuoni/ordini/sent  
2. **For News:** ultrasuoni/news

*(See the section below on how to automate this with Gmail Rules)*

## **📧 Setting Up Gmail Filters (Automation)**

To make this tool work seamlessly, you should set up "Filters" in Gmail so emails are labeled automatically.

### **1\. Automate "News" Labeling (Incoming)**

Use this rule to automatically label newsletters received from the record store.

1. Open Gmail and click the **Search options icon** (the sliders to the right of the search bar).  
2. In the **From** field, enter the store's email address (e.g., ultrasuonirecord@gmail.com).  
3. Click **Create filter**.  
4. Check the box **Apply the label** and select ultrasuoni/news (create it if it doesn't exist).  
5. Click **Create filter**.

### **2\. Automate "Orders" Labeling (Outgoing)**

Use this rule to automatically label order emails you send that contain the word "ordino".

1. Click the **Search options icon** again.  
2. In the **To** field, enter the store's email address (e.g., ultrasuonirecord@gmail.com).  
3. In the **Has the words** field, enter: ordino  
4. Click **Create filter**.  
5. Check the box **Apply the label** and select ultrasuoni/ordini/sent (create it if it doesn't exist).  
6. Click **Create filter**.

*Note: Gmail filters are primarily for incoming mail. If the outgoing filter doesn't catch every sent email instantly, you can simply go to your "Sent" folder, search for "ordino", select all, and apply the label manually in bulk.*

## **🚀 How to Install (No Coding Required)**

You don't need to download any files or install software on your computer. Everything lives inside your Google Sheet.

1. **Create a new Google Sheet** (or open a blank one).  
   * You can type sheets.new in your browser address bar to create one instantly.  
2. In the top menu, click on **Extensions** \> **Apps Script**.  
   * A new tab will open with a code editor.  
3. **Delete any code** that is currently there (usually just function myFunction() {...}).  
4. **Copy the code** from the Code.gs file in this repository.  
5. **Paste the code** into the script editor window.  
6. Click the **Save icon** (💾) in the toolbar. Name the project "Ultrasuoni Sync" (or whatever you like).  
7. **Refresh** your Google Sheet tab (press F5).

You should now see a new menu item called **"Ultrasuoni Tools"** appear next to "Help" at the top of your sheet.

## **🖱️ How to Use**

Once installed, you control everything from the **Ultrasuoni Tools** menu.

### **1\. Full Sync (Recommended)**

* **Click:** Ultrasuoni Tools \> 1\. Full Sync (Setup \+ Orders & News)  
* **What it does:**  
  * Checks if the "Orders" and "News" tabs exist.  
  * Scans your Gmail and populates the sheets.  
  * **Auto-Restart:** If the script takes too long (Google has a 6-minute limit), it will automatically pause, save, and schedule itself to run again in 30 seconds. You can close the sheet while it finishes in the background.

### **2\. Update Release Dates**

* **Click:** Ultrasuoni Tools \> 4\. Update Release Dates (Orders Only)  
* **What it does:**  
  * Reads the email subject associated with orders.  
  * If it finds text like "Coming in January" or "Release: 30 Nov", it writes that date into the **MANUAL: Release date** column.

### **3\. Cleanup & Fix Titles (Important\!)**

* **Click:** Ultrasuoni Tools \> 5\. 🧹 Cleanup & Fix Titles  
* **What it does:**  
  * Runs through your sheet to fix "Link Error" or missing titles.  
  * **Smart Fallback:** If a website (like Discogs) blocks the script, this tool extracts the artist/title directly from the URL text, so you always have a readable title.  
  * Hides the raw URL columns and turns the Title column into clickable hyperlinks.  
  * Resizes columns to fit content.

## **⚠️ First Run Authorization**

The first time you run the script, Google will ask for permission to access your Gmail and Sheets. This is normal.

1. Click **Review Permissions**.  
2. Select your Google Account.  
3. You will likely see a scary-looking screen saying "Google hasn't verified this app" (because you just created it\!).  
4. Click **Advanced** (small text on the left).  
5. Click **Go to Ultrasuoni Sync (unsafe)** at the bottom.  
6. Click **Allow**.

## **📝 Notes on Links**

The script prioritizes music links in this order:

1. **Bandcamp** links  
2. **Deejay.de** links  
3. **Other links** (It attempts to guess the relevant link if the above two are missing, filtering out generic links like Facebook, Instagram, Google, etc.).

*Enjoy your organized collection\!*