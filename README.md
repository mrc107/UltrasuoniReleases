# 🎛️ Ultrasuoni → Google Sheets Importer

Automatically imports releases from **Ultrasuoni emails in Gmail** into a **Google Sheets** file.  
It extracts release titles, links, prices, and release dates — and even detects which ones you’ve confirmed buying from your **email replies**.

---

## 📦 Repository contents

| File | Description |
|------|--------------|
| `Code.gs` | The complete Google Apps Script code to run in your account |
| `README.md` | This instruction guide |

👉 Repo link: [https://github.com/mrc107/UltrasuoniReleases](https://github.com/mrc107/UltrasuoniReleases)

---

## 🧩 What this script does

- Reads all emails under a specific **Gmail label** (e.g. `ultrasuoni`)
- Extracts:
  - ✅ Clean release titles (from text or URLs)
  - 🔗 All relevant shop/clip links (Bandcamp, Hardwax, Clone, etc.)
  - 💶 Price and 🗓️ release date
- Infers if you’ve **ordered the release** from your **email replies** (e.g. “lo prendo”, “yes”, “ok per me”)
- Marks confirmed releases with an `x` in the sheet
- Calculates **shipping batches** (every 20 records = one shipment) and total cost

---

## 🚀 Setup Instructions

### 1️⃣ Gmail — Create the label & auto-label rules

1. In Gmail, click **More → Create new label** → name it **`ultrasuoni`**.  
2. Create filters for Ultrasuoni emails:
   - In the Gmail search bar, click the **sliders icon** (Show search options).
   - In **From**, enter `ultrasuonirecord@gmail.com` or similar senders.
   - Click **Create filter** → check:
     - ✅ *Apply the label:* → `ultrasuoni`
     - ✅ *Also apply to existing conversations* (optional)
   - Save.

This ensures all Ultrasuoni emails (and replies) stay grouped.

---

### 2️⃣ Google Sheets — Create the destination file

1. Go to [Google Drive](https://drive.google.com).  
2. Click **New → Google Sheets**.  
3. Rename it to something like **Ultrasuoni Releases**.  
4. (Optional) Rename the sheet tab to **Releases**.

> The script can also create the sheet tab automatically if missing.

---

### 3️⃣ Apps Script — Add the importer code

You have two ways to add the script:

#### 🧠 Option A — Inside the Google Sheet (recommended)
1. Open your spreadsheet.  
2. Click **Extensions → Apps Script**.  
3. Delete any placeholder code.  
4. Copy all from [`Code.gs`](https://github.com/mrc107/UltrasuoniReleases/blob/main/Code.gs) in this repo and **paste it** into `Code.gs`.  
5. Save the project (e.g. “Ultrasuoni Importer”).  
6. Close and **refresh the sheet** — you’ll now see a new menu called **“Releases”** at the top.

#### ⚙️ Option B — As a standalone Apps Script project
1. Go to [script.google.com](https://script.google.com).  
2. Create a new project.  
3. Copy-paste the contents of [`Code.gs`](https://github.com/mrc107/UltrasuoniReleases/blob/main/Code.gs).  
4. Save the project.  
5. The first time you run it, it will ask you to choose a Google Sheet destination.

---

### 4️⃣ First run: authorize and pick the destination sheet

- On first run, the script will ask to **authorize** (Gmail read, Sheets write, UrlFetch).  
- It will also prompt you to **choose or confirm** your destination spreadsheet.  
  - If installed directly in a Sheet → it uses the **current spreadsheet**.
  - If running standalone → paste your **Sheet link or ID**.

You’ll then see a custom menu in the sheet:
