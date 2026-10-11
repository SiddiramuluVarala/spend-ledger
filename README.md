# Spend Ledger — install guide

A personal expense & budget tracker that runs as an app on your iPhone (and in any
browser on Windows/Ubuntu). No Mac, Xcode or Apple developer account needed.

- **App code** → public GitHub repo, served free by GitHub Pages.
- **Your data** → `ledger.json` in a **separate private** GitHub repo, read/written by
  the app with a token that can touch only that one repo.
- **Backups** → the Backup button saves a JSON file; on iPhone choose *iCloud Drive*
  in the Files dialog. Restore reads it back.

Total time: about 15 minutes, all in a browser.

---

## 1. Create the two repositories

Sign in at https://github.com and click **+ ▸ New repository** twice:

| | Name | Visibility | Notes |
|---|---|---|---|
| App | `spend-ledger` | **Public** | GitHub Pages on a free account needs a public repo. It only holds the app's code, never your numbers. |
| Data | `spend-ledger-data` | **Private** | Tick **Add a README file** so the repo has a `main` branch. |

## 2. Upload the app files

In the `spend-ledger` repo: **Add file ▸ Upload files**, drag in all of these from this kit, then **Commit changes**:

```
index.html
manifest.webmanifest
sw.js
icon-180.png
icon-192.png
icon-512.png
```

## 3. Turn on GitHub Pages

`spend-ledger` ▸ **Settings** ▸ **Pages** ▸ under *Build and deployment* set
**Source: Deploy from a branch**, **Branch: main / (root)** ▸ **Save**.

After about a minute the page shows your address:

```
https://<your-username>.github.io/spend-ledger/
```

Open it. The app should load (saved on this device only, for now).

## 4. Create the data token

GitHub ▸ your avatar ▸ **Settings** ▸ **Developer settings** ▸
**Personal access tokens** ▸ **Fine-grained tokens** ▸ **Generate new token**.

- **Token name:** `spend-ledger`
- **Expiration:** the longest offered (you'll paste a new one when it expires; the app tells you when sync fails)
- **Repository access:** *Only select repositories* ▸ `spend-ledger-data`
- **Permissions ▸ Repository permissions ▸ Contents:** **Read and write**
  (everything else stays "No access")

Click **Generate token** and copy it (`github_pat_…`). It is shown only once.

## 5. Connect the app

In the app: **Settings ▸ GitHub sync**

- Repository: `<your-username>/spend-ledger-data`
- Token: paste it
- Branch: `main`

Tap **Connect & sync**. The home screen label changes to *Synced to GitHub*.
Your private repo now contains `ledger.json`; every change you make is committed
there within a couple of seconds, and the app re-syncs each time you open it.

Repeat step 5 on each device (iPhone, Windows, Ubuntu) using the same token.
Entries made while offline or before connecting are merged in, not lost.

## 6. Put it on the iPhone home screen

Open the Pages address in **Safari** ▸ Share button ▸ **Add to Home Screen**.
It opens full-screen, keeps its own icon, and works offline (sync resumes when online).

---

## Everyday use

- **+** adds an expense: amount, category, critical / non-critical (defaults from the category), date, payment method, note, tags.
- **Expenses** tab: day / month / year lists, search, critical filter; tap an entry to edit or delete.
- **Analysis** tab: trend chart, category breakdown vs budget, tags, payment methods, insights, monthly table (year view).
- **Budget** tab: monthly budget plus per-category budgets; add/edit categories.
- **Settings**: currency, theme, backup/restore, CSV export, sample data.

## Backups to iCloud Drive

Settings ▸ **Backup** downloads `spend-ledger-YYYY-MM-DD.json`. On iPhone Safari shows a
download; open **Files** ▸ Downloads, long-press the file ▸ **Move** ▸ *iCloud Drive*.
(Or set Safari ▸ Settings ▸ Downloads to iCloud Drive once, and every backup lands there.)
**Restore backup** merges a file back in on any device.

## Updating the app later

Upload a new `index.html` to the `spend-ledger` repo (replace the old one). Open the app
once while online and it picks up the new version; your data is untouched because it lives
in the other repo.

## Security notes

- The token is stored only in the browser of each device you paste it into (Settings ▸ Disconnect forgets it).
- It can only read/write files in `spend-ledger-data`; it cannot see your other repos.
- If a device is lost, revoke the token at GitHub ▸ Developer settings and create a new one.
