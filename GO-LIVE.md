# 🚀 Go-Live Checklist — makaproperty.co.nz

Plain-English steps to put the Maka Property site online, using the same setup as
makaprojects.co.nz. Follow them top to bottom.

**Nothing here touches your email.** Your Microsoft 365 inbox keeps working throughout —
you only *add* two website DNS records, you never edit or delete anything else.

You'll do four things:
1. Push this folder to a new GitHub repo.
2. Connect it to a new Netlify site (temporary live address).
3. Tell Netlify your domain is `makaproperty.co.nz`.
4. Add two DNS records at 1st Domains so the domain points at Netlify.

⏱️ Budget ~20 minutes, plus up to a few hours for DNS to spread worldwide.

---

## STEP 1 — Push to GitHub (new repo)

1. On GitHub (signed in as **MarkBWatkins**): **+ → New repository**.
   - Name: **`maka-property-website`**
   - Visibility: **Public**
   - **Do NOT** tick "Add a README" (this folder already has one).
   - Create repository.
2. Open a Command Prompt **in this folder** (the one containing `index.html`) and run:
   ```
   git init
   git add -A
   git commit -m "Initial Maka Property website"
   git branch -M main
   git remote add origin https://github.com/MarkBWatkins/maka-property-website.git
   git push -u origin main
   ```
   First push will ask you to sign in to GitHub — follow the browser prompt.

   > **If git reports a lock error** (`.git/index.lock` or similar):
   > ```
   > del /s /q .git*.lock
   > ```
   > then re-run `git add -A`, `git commit ...`, `git push`.

---

## STEP 2 — Put the site on Netlify

1. Go to **https://app.netlify.com** and sign in (use the **Maka Projects** team).
2. **Add new site → Import an existing project → Deploy with GitHub**.
3. Authorise GitHub if asked, then pick **`maka-property-website`**.
4. Netlify reads `netlify.toml` automatically:
   - Build command: **blank**
   - Publish directory: **`.`**
   Click **Deploy**.
5. It deploys and gives you a temporary address like `https://random-name-1234.netlify.app`.
   Open it and check the site looks right.
6. Optional but tidy: **Site configuration → Change site name** → set it to something like
   **`maka-property`** so your address becomes `maka-property.netlify.app`.
   **Note this address — you need it for the DNS step.**

➡️ From now on, **any change you commit and push goes live automatically.**

---

## STEP 3 — Tell Netlify your domain

1. In your Netlify site: **Domain management → Add a domain**.
2. Enter **`makaproperty.co.nz`** and add it.
3. When asked how to manage DNS, choose **"Add a domain you already own"** and, if offered,
   **set up records manually / use external DNS**.
   ⚠️ **Do NOT choose "Use Netlify DNS" / nameservers.** That would move ALL your DNS
   (including email) to Netlify — we don't want that.
4. Also add **`www.makaproperty.co.nz`** when prompted.

---

## STEP 4 — Add the DNS records at 1st Domains

Log in at **https://1stdomains.nz** (account 17726272) → domain **`makaproperty.co.nz`**
→ **DNS / Zone management**.

Add these **two** records:

| # | Type      | Host / Name | Value / Points to                                   | TTL          |
|---|-----------|-------------|-----------------------------------------------------|--------------|
| 1 | **A**     | `@` (blank) | `75.2.60.5`                                         | default/3600 |
| 2 | **CNAME** | `www`       | `maka-property.netlify.app`  *(your Netlify address from Step 2)* | default/3600 |

Notes:
- Record 1 (`@`) is the bare domain `makaproperty.co.nz` (some panels want the Host left blank).
- Record 2 (`www`) value is **your** `xxxx.netlify.app` address — paste your real one.
- If 1st Domains offers an **ALIAS**/**ANAME** type, you may instead point `@` to
  `apex-loadbalancer.netlify.com`. If not, the A record to `75.2.60.5` is correct.

### ⛔ DO NOT TOUCH — your email records
Leave every **MX** record as-is, plus any **TXT** records mentioning `spf`, `DKIM` or
`microsoft`, and any `autodiscover` / `enterpriseregistration` CNAMEs. **These run your
Microsoft 365 email.** You are only *adding* the two website records above.

> Sanity check before saving: your MX record(s) should still point at something like
> `makaproperty-co-nz.mail.protection.outlook.com`. If they do, email is safe.

---

## STEP 5 — Primary domain, HTTPS & the enquiry form

1. In Netlify **Domain management**, set **`makaproperty.co.nz` as the Primary domain**
   (Netlify auto-redirects `www` → apex).
2. Netlify auto-provisions a free **HTTPS certificate** once it sees the DNS — wait until it
   says **"Certificate: Active"**, then tick **"Force HTTPS"**.
3. **Enquiry form:** it's wired to **Netlify Forms** (form name `enquiry`). Go to
   **Forms → enquiry → Settings → Form notifications** and add an **email notification** to
   **`katew@makaproperty.co.nz`** so every enquiry lands in the inbox. Submissions are also
   stored in the Netlify dashboard, and submitters see the branded `thanks.html` page.

---

## STEP 6 — Verify

- Visit **https://makaproperty.co.nz** and **https://www.makaproperty.co.nz** — both should
  load with a padlock.
- Send a test enquiry through the form and confirm it appears under **Forms** (and emails you).
- Send yourself a test email to `katew@makaproperty.co.nz` to confirm email is unaffected
  (it will be — you never touched the MX records).

---

## Quick reference

| Thing | Value |
|---|---|
| Primary domain | `makaproperty.co.nz` |
| Apex A record | `75.2.60.5` |
| www CNAME target | `maka-property.netlify.app` *(your Netlify address)* |
| GitHub repo | `MarkBWatkins/maka-property-website` (public) |
| Netlify team | Maka Projects |
| Enquiry form | Netlify Forms — name `enquiry` → notify `katew@makaproperty.co.nz` |
| Email | Microsoft 365 — **MX untouched** |
| Site files | this folder (`index.html` is the page) |
