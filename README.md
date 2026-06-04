# 🐍🪜 Fitness Snakes & Ladders

A group fitness challenge board game — track class attendance, roll dice weekly, and watch your team climb ladders and dodge snakes on the path to square 100!

## 📁 File Structure

All files sit at the root — no subfolders needed:

```
fitness-snl/
├── index.html            ← Public board (share this URL with members)
├── admin-login.html      ← Admin login page
├── admin-dashboard.html  ← Full admin management interface
├── config.js             ← Admin credentials (edit to change password)
├── gamestate.json        ← Game data (update this to publish changes)
├── README.md
└── .github/
    └── workflows/
        └── deploy.yml    ← Auto-deployment config (don't edit)
```

---

## 🚀 Setup Guide (GitHub Pages)

### Step 1 — Create a GitHub repo

1. Go to [github.com](https://github.com) and sign in
2. Click **"New repository"**
3. Name it something like `fitness-snl`
4. Set it to **Public** (required for free GitHub Pages)
5. Click **Create repository**

### Step 2 — Upload all files

1. In your new repo click **"uploading an existing file"**
2. Drag and drop all files from this folder — including the hidden `.github` folder
3. Commit the changes

### Step 3 — Enable GitHub Pages

1. Go to repo **Settings → Pages**
2. Under **Source**, select **GitHub Actions**
3. Save

The first deployment runs automatically. Your site goes live at:
```
https://YOUR-USERNAME.github.io/fitness-snl/
```

---

## 🔗 Two URLs to share

| Who | URL |
|-----|-----|
| Members (view-only board) | `https://YOUR-USERNAME.github.io/fitness-snl/` |
| Admin (manage the game) | `https://YOUR-USERNAME.github.io/fitness-snl/admin-login.html` |

---

## 🔐 Changing Your Admin Password

Default credentials: **username:** `admin` / **password:** `fitness2024`

To change them:

1. Go to [this SHA-256 tool](https://emn178.github.io/online-tools/sha256.html)
2. Type your new password and copy the hash
3. Open `config.js` in your GitHub repo (click the file → pencil icon to edit)
4. Update the `username` and `passwordHash` values:

```js
window.ADMIN_CONFIG = {
  username: 'yourname',        // ← change this
  passwordHash: 'abc123...'   // ← paste your SHA-256 hash here
};
```

5. Commit the change — deploys automatically

---

## 📋 How to Use (Admin)

1. Go to `admin-login.html` and sign in
2. Use the tabs to manage the game:

| Tab | What it does |
|-----|-------------|
| **Board** | Preview the live board and leaderboard |
| **Players** | Add/remove players, bulk import by name |
| **Attendance** | Log who attended which class, or import CSV |
| **Weekly Roll** | Roll the dice to move all players |
| **Settings** | Configure class types/points, snakes & ladders |
| **Export/Save** | Download `gamestate.json` to publish changes |

### Publishing changes to the live board

1. Make changes in the admin dashboard
2. Go to **Export/Save** tab → click **Download gamestate.json**
3. In your GitHub repo, open `gamestate.json` → click ✏️ Edit → paste new content → Commit
4. GitHub auto-redeploys in ~1 minute and the public board updates

---

## 📊 CSV Attendance Format

```csv
date,class_type,player_name
2025-01-06,HIIT,Alice
2025-01-06,Yoga,Bob
2025-01-07,Spin,Charlie
```

- `date` — format: YYYY-MM-DD  
- `class_type` — must match a class name in Settings (case-insensitive)  
- `player_name` — must match a player name (case-insensitive)

---

## 🎲 How the dice roll works

- Two dice (D6) rolled → total 2–12
- Players who attended ≥1 class this week move: `dice total × (1 + weekPoints/10)`, min 1 square
- Players with zero classes that week don't move
- Snakes and ladders apply automatically after each move
- Weekly points reset to zero after the roll

---

## ❓ Troubleshooting

**Board shows old data after publishing**  
→ Wait 2–3 minutes then hard-refresh (Ctrl+Shift+R / Cmd+Shift+R)

**Admin login not working**  
→ Check `config.js` — make sure the password hash matches exactly

**GitHub Actions failing**  
→ Settings → Pages → confirm Source is "GitHub Actions" not "Deploy from branch"

**`.github` folder not uploading**  
→ On Mac/Linux, hidden folders (starting with `.`) may not show in file pickers. Use the GitHub web UI drag-and-drop, or use `git` from the command line to push all files including hidden ones.
