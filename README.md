# GearPedia — Firebase Hosting Deployment

Deploy your single-file GearPedia PWA to Firebase Hosting (free Spark plan) via GitHub Actions.

---

## 📁 Repository Structure

```
your-repo/
├── index.html                        ← Your GearPedia app
├── firebase.json                     ← Firebase hosting config
├── .firebaserc                       ← Firebase project alias
├── .gitignore
├── .github/
│   └── workflows/
│       └── firebase-deploy.yml       ← Auto-deploy on push to main
└── README.md
```

---

## 🚀 One-Time Setup (do this once)

### Step 1 — Create a Firebase Project
1. Go to [https://console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → give it a name (e.g. `gearpedia`)
3. Disable Google Analytics (not needed) → **Create project**
4. In the left sidebar, click **Hosting** → **Get started** → follow prompts
5. Note your **Project ID** (shown in Project Settings, looks like `gearpedia-abc12`)

### Step 2 — Generate a Firebase Service Account
1. In Firebase Console → ⚙️ **Project Settings** → **Service accounts**
2. Click **Generate new private key** → **Generate key**
3. A `.json` file downloads — keep it safe, you'll need its contents

### Step 3 — Add Secrets to GitHub
Go to your GitHub repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

Add these three secrets:

| Secret Name | Value |
|---|---|
| `FIREBASE_SERVICE_ACCOUNT` | Paste the **entire contents** of the downloaded `.json` file |
| `FIREBASE_PROJECT_ID` | Your Firebase Project ID (e.g. `gearpedia-abc12`) |

> `GITHUB_TOKEN` is automatic — GitHub provides it, no action needed.

### Step 4 — Update `.firebaserc`
Open `.firebaserc` and replace `YOUR_FIREBASE_PROJECT_ID` with your actual Project ID:
```json
{
  "projects": {
    "default": "gearpedia-abc12"
  }
}
```

### Step 5 — Push to GitHub
```bash
git init
git add .
git commit -m "Initial deploy: GearPedia"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

That's it! GitHub Actions will automatically deploy to Firebase Hosting. ✅

---

## 🔄 How Auto-Deploy Works

Every time you push a commit to the `main` branch:
1. GitHub Actions triggers the workflow
2. Firebase CLI deploys `index.html` to Firebase Hosting
3. Your live site updates at `https://YOUR_PROJECT_ID.web.app`

---

## 🌐 Your Live URLs

After first deploy, your site is live at:
- `https://YOUR_PROJECT_ID.web.app`
- `https://YOUR_PROJECT_ID.firebaseapp.com`

---

## 💡 Free Plan Limits (Spark — more than enough for this app)

| Resource | Free Limit |
|---|---|
| Hosting Storage | 10 GB |
| Data Transfer / month | 360 MB/day (~10 GB/month) |
| Custom Domain | ✅ Supported |
| SSL Certificate | ✅ Free & automatic |

Your `index.html` is ~1.2 MB. You'd need ~8,000 page loads/day to hit the transfer limit — well within free tier for most use cases.

---

## 🛠 Manual Deploy (optional, without GitHub Actions)

If you prefer to deploy from your local machine:
```bash
npm install -g firebase-tools
firebase login
firebase deploy
```

---

## ❓ Troubleshooting

| Problem | Fix |
|---|---|
| Build fails with "Project not found" | Check `FIREBASE_PROJECT_ID` secret matches `.firebaserc` |
| "Permission denied" error | Re-generate the service account key and update the secret |
| Site shows old version | Hard-refresh browser (Ctrl+Shift+R / Cmd+Shift+R) |
| Service worker not updating | Clear site data in DevTools → Application → Clear storage |
