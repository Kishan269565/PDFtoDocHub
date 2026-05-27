# PDFtoDocHub — Free PDF ↔ Word Converter

No API. No login. No payment. Pure Python.

## Features
- PDF → Word (.docx)
- Word → PDF (via LibreOffice)
- Drag & drop UI
- Full Google SEO (meta tags, structured data, FAQ schema, sitemap, robots.txt)
- Files auto-deleted after 5 minutes

---

## Local Development

```bash
# 1. Install Python dependencies
pip install -r requirements.txt

# 2. Install LibreOffice (needed for Word → PDF)
# Ubuntu/Debian:
sudo apt install libreoffice

# macOS:
brew install --cask libreoffice

# 3. Run
python app.py
# Open http://localhost:5000
```

---

## Deploy FREE on Railway

1. Push this folder to a GitHub repo
2. Go to https://railway.app → New Project → Deploy from GitHub
3. Add this environment variable in Railway settings:
   ```
   PORT=5000
   ```
4. Railway detects the Procfile and runs gunicorn automatically
5. Add your custom domain in Railway → Settings → Domains

### Install LibreOffice on Railway
Add a `nixpacks.toml` file:
```toml
[phases.setup]
nixPkgs = ["libreoffice"]
```

---

## Deploy FREE on Render

1. Push to GitHub
2. Go to https://render.com → New Web Service → Connect repo
3. Build command: `pip install -r requirements.txt`
4. Start command: `gunicorn app:app --workers 4 --timeout 120`
5. Add LibreOffice via `render.yaml`:
```yaml
services:
  - type: web
    name: PDFtoDocHub
    env: python
    buildCommand: "apt-get install -y libreoffice && pip install -r requirements.txt"
    startCommand: "gunicorn app:app --workers 4 --timeout 120"
```

---

## Google SEO Checklist

After deploying:

1. **Google Search Console**
   - Go to https://search.google.com/search-console
   - Add your domain property
   - Verify ownership (HTML tag or DNS)
   - Submit sitemap: `https://yourdomain.com/static/sitemap.xml`

2. **Google Analytics** (optional but recommended)
   - Create account at https://analytics.google.com
   - Paste the GA4 script before `</head>` in `templates/index.html`

3. **PageSpeed** — check your score at https://pagespeed.web.dev

4. **Backlinks** — post your tool on:
   - Reddit (r/software, r/productivity, r/webdev)
   - ProductHunt
   - AlternativeTo.net (list as alternative to ilovepdf, smallpdf)

---

## Monetization

- **Google AdSense**: Apply at https://adsense.google.com after getting traffic
- **Affiliate**: Link to LibreOffice or PDF tools in the footer
- **Freemium**: Add a file-size cap for guests, remove for registered users

---

## Project Structure

```
docconverter/
├── app.py              ← Flask backend (all conversion logic)
├── requirements.txt    ← Python dependencies
├── Procfile            ← For Railway/Heroku deployment
├── templates/
│   └── index.html      ← Full website with SEO
└── static/
    ├── sitemap.xml     ← Google sitemap
    └── robots.txt      ← Search engine instructions
```
