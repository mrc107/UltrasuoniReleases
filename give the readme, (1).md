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

## **📝 Installation Guide**

Follow these steps in order to get everything running.

### **Step 1: Prepare Gmail (Prerequisites)**

The script needs to know which emails to look for. You need to create two specific labels in your Gmail.

1. **For Orders:** Create a label named ultrasuoni/ordini/sent.  
2. **For News:** Create a label named ultrasuoni/news.

### **Step 2: Automate Gmail Labels (Filters)**

To make this automatic, set up "Filters" so you don't have to label emails manually.

**A. Automate "News" (Incoming)**

1. Open Gmail and click the **Search options icon** (the sliders in the search bar).  
2. In the **From** field, enter the store's email (e.g., ultrasuonirecord@gmail.com).  
3. Click **Create filter**.  
4. Check **Apply the label** and select ultrasuoni/news.  
5. Click **Create filter**.

**B. Automate "Orders" (Outgoing)**

1. Click the **Search options icon** again.  
2. In the **To** field, enter the store's email.  
3. In the **Has the words** field, enter: ordino.  
4. Click **Create filter**.  
5. Check **Apply the label** and select ultrasuoni/ordini/sent.  
6. Click **Create filter**.

*Tip: Go to your "Sent" folder, search for "ordino", select all your past orders, and apply the ultrasuoni/ordini/sent label to them so the script can find your history.*

### **Step 3: Set up the Google Sheet & Script**

You don't need to download files. The code lives inside the Google Sheet.

1. **Create a blank Google Sheet.**  
   * (Tip: Type sheets.new in your browser URL bar to create one instantly).  
2. In the top menu, go to **Extensions** \> **Apps Script**.  
   * A new browser tab will open showing a code editor.  
3. **Clear the editor:** Delete any code you see there (usually function myFunction() {...}).  
4. **Get the Code:** Copy the entire content of the Code.gs file provided in this repository.  
5. **Paste the Code:** Paste it into the script editor window.  
6. **Save:** Click the disk icon 💾 or press Ctrl+S. Name the project "Ultrasuoni Sync".  
7. **Refresh:** Go back to your Google Sheet tab and refresh the page (F5).

🎉 **Success\!** You should now see a new menu called **"Ultrasuoni Tools"** in the toolbar next to "Help".

## **🖱️ How to Use**

Control everything from the **Ultrasuoni Tools** menu.

### **1\. Full Sync (Recommended)**

* **Click:** Ultrasuoni Tools \> 1\. Full Sync (Setup \+ Orders & News)  
* **What happens:**  
  * It creates the "Orders" and "News" tabs if they don't exist.  
  * It scans your Gmail labels and pulls in all the links.  
  * **Auto-Cleanup:** At the end, it automatically fixes missing titles, converts them to hyperlinks, and formats the sheet.  
  * **Auto-Restart:** If the script runs for too long (Google limits scripts to \~6 minutes), it will pause, save, and automatically start again in 30 seconds.

### **2\. Update Release Dates**

* **Click:** Ultrasuoni Tools \> 4\. Update Release Dates (Orders Only)  
* **What happens:**  
  * It checks your order emails for subject lines like "Coming in November" and updates the "Release Date" column.

### **3\. Force Cleanup & Fix Titles (Optional)**

* **Click:** Ultrasuoni Tools \> 5\. Force Cleanup & Fix Titles  
* **What happens:**  
  * **Note:** This runs automatically after every sync, so you usually don't need to click this.  
  * Use this button manually if you want to re-check titles or if you edited links manually and want to re-format the sheet.

## **⚠️ Authorization (First Run Only)**

The first time you click a menu item, Google will ask for permission.

1. Click **Continue** / **Review Permissions**.  
2. Select your Google Account.  
3. You might see a warning screen ("Google hasn't verified this app"). **This is safe** (it's your own private script).  
4. Click **Advanced** (small link at the bottom).  
5. Click **Go to Ultrasuoni Sync (unsafe)**.  
6. Click **Allow**.

## **📝 Notes on Links**

The script prioritizes music links in this order:

1. **Bandcamp**  
2. **Deejay.de**  
3. **Other links** (It guesses the best link if the others are missing, ignoring junk like Facebook/Instagram).

*Enjoy your organized collection\!*