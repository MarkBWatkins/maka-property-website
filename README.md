# Maka Property — website

Single-page static marketing site for **Maka Property**, promoting our whole-house
holiday homes for big families and groups (The Home on the Hill, Piarere/Tīrau; and
2 Wagner Place, Ohiwa).

- **No build step.** The repo root is published as-is on Netlify (`publish = "."`).
- `index.html` is the whole site (inline CSS/JS). Photos live in `/img`.
- Enquiries use **Netlify Forms** (form name `enquiry`) — submissions appear in the
  Netlify dashboard under *Forms*. Add an email notification to `katew@makaproperty.co.nz`.
- Social share image: `og-image.png`. Icons: `favicon.svg` / `favicon.ico` / `apple-touch-icon.png`.

## Updating the site

Edit the files, then from this folder:

```
git add -A
git commit -m "your note"
git push
```

Netlify redeploys automatically in about a minute.

See **GO-LIVE.md** for first-time deployment and DNS.
