# Deploy to Render — Step by Step

**Repo:** https://github.com/SURYAS1306/Startup-Opportunity-Aggregator-project

---

## 1. Sign in to Render

1. Open [https://render.com](https://render.com)
2. Click **Get Started** → sign in with **GitHub**

---

## 2. Create Web Service

1. Dashboard → **New +** → **Web Service**
2. Connect **GitHub** if asked
3. Find and select: **Startup-Opportunity-Aggregator-project**
4. Click **Connect**

---

## 3. Configure (copy these exactly)

| Field | Value |
|-------|--------|
| **Name** | `startup-opportunity-aggregator` (or any name) |
| **Region** | Singapore or closest to you |
| **Branch** | `main` |
| **Runtime** | `Python 3` |
| **Build Command** | `pip install -r requirements.txt && python scripts/run_scraper.py --keyword "AI startup"` |
| **Start Command** | `gunicorn run:app --bind 0.0.0.0:$PORT --workers 2 --timeout 120` |
| **Instance type** | Free |

---

## 4. Environment variables

Click **Advanced** → add:

| Key | Value |
|-----|--------|
| `RUN_SCRAPE_ON_START` | `1` |
| `SCRAPE_KEYWORD` | `AI startup` |
| `PYTHON_VERSION` | `3.12.3` |
| `FLASK_SECRET_KEY` | (click Generate or paste any long random string) |

---

## 5. Deploy

1. Click **Create Web Service**
2. Wait **5–15 minutes** (first build runs scraper + installs packages)
3. When status is **Live**, copy your URL from the top of the page

Example:

```text
https://startup-opportunity-aggregator.onrender.com
```

That is your **deployment link** for the assignment.

---

## 6. Verify

Open in browser:

- `https://YOUR-APP.onrender.com` — dashboard (should show opportunities)
- `https://YOUR-APP.onrender.com/health` — should show `"status": "ok"`

If the dashboard is empty, click **Run Scraper** once (first free-tier wake can be slow).

---

## 7. Add link to README

Edit `README.md` → **Live Demo** section:

```markdown
| **Live (Render)** | https://YOUR-APP.onrender.com |
```

Then:

```bash
git add README.md
git commit -m "docs: add Render deployment URL"
git push
```

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Build fails on `lxml` | Ensure `PYTHON_VERSION=3.12.3` is set |
| 502 / timeout on first visit | Free tier waking up — wait 60s, refresh |
| Empty dashboard | Run scraper from UI or redeploy with build command above |
| App sleeps | Normal on free tier — mention in submission |

---

## Alternative: Blueprint (auto from `render.yaml`)

1. **New +** → **Blueprint**
2. Connect repo **Startup-Opportunity-Aggregator-project**
3. Render reads `render.yaml` automatically
4. Approve and deploy
