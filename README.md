# Personal Academic Website — Ron de Bruijn

Static personal website, built with plain HTML and CSS, hosted on GitHub Pages,
served from the custom domain **rondebruijn.eu**.

---

## 📁 What's in this folder

| File | What it is |
|---|---|
| `index.html` | The whole site (one page with About, Research, Publications, Teaching, Contact) |
| `styles.css` | All styling |
| `CNAME` | Tells GitHub Pages which custom domain to use (`rondebruijn.eu`) |
| `.nojekyll` | Tells GitHub Pages **not** to run Jekyll on this repo (we serve plain files) |
| `.gitignore` | Files git should ignore |
| `photo.jpg` | **You need to add this** — your portrait photo (~600×600 px, square) |
| `cv.pdf` | **Optional** — your CV, linked from the homepage |

---

## ✏️ How to fill in your content

Open `index.html` in any text editor (VS Code, Notepad++, Sublime Text, even Notepad).
Look for placeholders marked `[like this]` or `<em>[like this]</em>` and replace them with your own text.

You'll want to update at minimum:
- **Department, research area, bio paragraphs** (Hero section)
- **Research themes** (Research section — you can add or delete `<article class="card">` blocks)
- **Publications** (Publications section — copy/paste a `<li>...</li>` block per paper)
- **Courses & supervision** (Teaching section)
- **Office address, email, social links** (Contact section)

To change colours, fonts, or spacing, edit the `:root { ... }` block at the top of `styles.css`.

---

## 🚀 Step-by-step: publish to GitHub Pages with custom domain

These steps assume you have a GitHub account but haven't set up a repository yet.
Total time: ~20 minutes (plus DNS propagation, which can take 1–24 hours).

### Step 1 — Create the GitHub repository

1. Go to <https://github.com/new>.
2. **Repository name**: name it `<your-username>.github.io` (replace `<your-username>` with your actual GitHub username).
   Example: if your username is `rondebruijn`, the repo name must be `rondebruijn.github.io`.
   *Why this exact name?* GitHub treats a repo with this name as your "user site", which gets deployed automatically.
3. **Visibility**: Public.
4. **Do NOT** check "Add a README" — we already have files.
5. Click **Create repository**.

### Step 2 — Push the website files to GitHub

You have two options. Pick whichever feels easier.

#### Option A — Use GitHub Desktop (easiest, no command line)

1. Install [GitHub Desktop](https://desktop.github.com/) and sign in.
2. **File → Clone repository →** pick the `<your-username>.github.io` repo you just made → choose a local folder.
3. Copy all files from this `website` folder (`index.html`, `styles.css`, `CNAME`, `.nojekyll`, `.gitignore`, plus your `photo.jpg` and `cv.pdf` once you add them) into that cloned folder.
4. Back in GitHub Desktop, you'll see the changes listed.
   - In the bottom-left, type a summary: `Initial site`.
   - Click **Commit to main**.
   - Click **Push origin** (top bar).

#### Option B — Use the command line

```bash
cd "path/to/this/website/folder"

git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
git push -u origin main
```

### Step 3 — Enable GitHub Pages

1. On GitHub, open your repository.
2. Click **Settings** (top right of repo).
3. In the left sidebar, click **Pages**.
4. Under **Build and deployment → Source**, select **Deploy from a branch**.
5. Under **Branch**, choose `main` and folder `/ (root)`. Click **Save**.
6. Wait ~1 minute. Refresh the page — at the top you'll see a green message:
   *"Your site is live at `https://<your-username>.github.io/`"*.

Open that URL in a browser to confirm the site works. ✅

### Step 4 — Connect your custom domain (rondebruijn.eu) via one.com

You'll need to add DNS records on one.com so that `rondebruijn.eu` points to GitHub's servers.

#### 4a. Log in to one.com

1. Log in at <https://www.one.com/admin>.
2. Select the domain **rondebruijn.eu**.
3. Open **DNS settings** (sometimes under "Advanced settings" or "DNS records").

#### 4b. Add the GitHub Pages DNS records

You need **two sets** of records.

**For the "naked" domain `rondebruijn.eu`** — add four A records pointing to GitHub's IPs:

| Type | Hostname / Name | Value (IP) | TTL |
|---|---|---|---|
| A | @  *(or leave blank)* | `185.199.108.153` | 3600 |
| A | @ | `185.199.109.153` | 3600 |
| A | @ | `185.199.110.153` | 3600 |
| A | @ | `185.199.111.153` | 3600 |

**For the `www` subdomain** — add one CNAME record:

| Type | Hostname / Name | Value | TTL |
|---|---|---|---|
| CNAME | www | `<your-username>.github.io.` *(note the trailing dot if one.com requires it)* | 3600 |

> ⚠️ **Remove conflicting records first.** If one.com already has A records or a CNAME for `@` or `www` (often pointing to a one.com placeholder page), delete them before adding the GitHub ones — otherwise the domain will keep showing the old page.

Save the changes.

#### 4c. Tell GitHub about the custom domain

1. Back on GitHub: **Settings → Pages**.
2. Under **Custom domain**, type `rondebruijn.eu` and click **Save**.
3. GitHub will start a DNS check. This can take from a few minutes up to 24 hours.
4. Once the DNS check passes, **tick the "Enforce HTTPS" checkbox**. This may take another hour to become available — be patient.

> The `CNAME` file in this repo already contains `rondebruijn.eu`, so GitHub will pick this up automatically. Don't edit or delete that file.

#### 4d. (Optional) Forward `de-bruijn.eu` to `rondebruijn.eu`

If you want your second domain to also reach the site, the simplest path is one.com's built-in **domain forwarding** (also called "web forwarding" or "redirect"):

1. In one.com, open the **de-bruijn.eu** domain settings.
2. Find **Redirect / Forward domain**.
3. Forward to `https://rondebruijn.eu` with permanent redirect (HTTP 301).

(If you'd rather have `de-bruijn.eu` *also* serve the site directly from GitHub Pages, that requires a separate repo or a GitHub Pages organisation site — the redirect approach above is simpler and recommended.)

### Step 5 — Verify

Once DNS has propagated (try after 1 hour, then a few hours later):

- <https://rondebruijn.eu> → your site
- <https://www.rondebruijn.eu> → your site
- Padlock icon visible in the browser (HTTPS working)

You can check DNS propagation with a tool like <https://dnschecker.org/>.

---

## 🔄 How to update the site later

After your first deploy, updating is easy:

**With GitHub Desktop:**
1. Edit the files in your local folder.
2. Open GitHub Desktop, write a short summary (e.g. `Add new publication`), click **Commit to main**, then **Push origin**.
3. Within 1–2 minutes, the live site updates automatically.

**Command line:**
```bash
git add .
git commit -m "Update publications"
git push
```

---

## 🧪 Preview locally before pushing

You can just double-click `index.html` to open it in your browser — that works for most things.

For a more accurate preview (some browsers restrict local files), run a tiny local web server:

```bash
# Python (already installed on most systems):
python -m http.server 8000
# then open http://localhost:8000 in your browser
```

---

## 📝 Quick checklist before going live

- [ ] Replaced all `[placeholder]` text in `index.html`
- [ ] Added your `photo.jpg` (square, ~600×600)
- [ ] Added your `cv.pdf` (or removed the CV button if you don't want one)
- [ ] Updated all the social links (Scholar, ORCID, LinkedIn, GitHub) with your real URLs
- [ ] Updated the `<title>` and `<meta description>` tags in `<head>`
- [ ] Pushed everything to your `<username>.github.io` repository
- [ ] DNS records added on one.com
- [ ] Custom domain set + HTTPS enforced on GitHub

---

## ❓ Troubleshooting

**"My site shows a 404."**
→ Wait 1–2 minutes after the first push. Then check **Settings → Pages**: it should say "Your site is live". If the repo name is wrong (must be `<username>.github.io`), rename it.

**"My custom domain doesn't work yet."**
→ DNS can take up to 24 hours. Use <https://dnschecker.org/> to check whether `rondebruijn.eu` resolves to the GitHub IPs (`185.199.108.153` etc.) globally.

**"GitHub says HTTPS is not yet available."**
→ Normal. Wait an hour or two after the DNS check passes, then refresh the Pages settings page and tick the box.

**"My CSS isn't loading."**
→ Check that `styles.css` is at the same level as `index.html` (root of the repo), and that filenames match exactly (case-sensitive on GitHub).
