# Nestor AI — Full-Stack Chatbot

Gemini-powered AI chatbot with Python backend on Vercel.

## Project Structure

```
nestor-ai/
├── api/
│   └── chat.py          ← Vercel Python serverless function (POST /api/chat)
├── public/
│   └── index.html       ← Frontend UI
├── vercel.json          ← Routing + security headers
├── requirements.txt     ← Python deps (stdlib only, no installs needed)
└── README.md
```

## Deploy to Vercel via GitHub

### 1. Create a GitHub repo
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/nestor-ai.git
git push -u origin main
```

### 2. Import to Vercel
1. Go to https://vercel.com/new
2. Import your GitHub repo
3. Framework preset: **Other**
4. Leave build & output settings as default
5. Click **Deploy**

### 3. Set Environment Variable (CRITICAL)
In Vercel dashboard → Your project → **Settings → Environment Variables**:

| Name | Value |
|------|-------|
| `GEMINI_API_KEY` | `your_key_here` |

Get your free key at: https://aistudio.google.com/app/apikey

Optionally restrict CORS:
| Name | Value |
|------|-------|
| `ALLOWED_ORIGINS` | `https://your-app.vercel.app` |

### 4. Redeploy
After adding the env var, go to **Deployments → Redeploy**.

---

## Security Features

- **No API key in frontend** — key lives only in Vercel env vars
- **Input sanitization** — strips control characters, enforces length limits
- **File validation** — MIME type allowlist + 5 MB size cap
- **Rate-aware payload cap** — 20 MB hard request limit
- **Safety filters** — Gemini harm categories set to BLOCK_MEDIUM_AND_ABOVE
- **Security headers** — X-Frame-Options, CSP, X-XSS-Protection, etc.
- **CORS control** — configurable via ALLOWED_ORIGINS env var
- **History trimming** — only last 40 turns sent to Gemini (prevents token abuse)
- **No persistent storage** — history lives in sessionStorage only

## Local Development

```bash
# Install Vercel CLI
npm i -g vercel

# Add your key to .env.local
echo "GEMINI_API_KEY=your_key_here" > .env.local

# Run locally
vercel dev
```

Then open http://localhost:3000
