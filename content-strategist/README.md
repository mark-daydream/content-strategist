# SEO Content Strategist

AI-powered SEO tool for on-page optimizations and net new content.

## Deploying to Vercel

### 1. Push to GitHub
Push this folder (with `index.html`, `api/claude.js`, `vercel.json`) to a GitHub repo.

### 2. Import to Vercel
- Go to vercel.com → New Project → Import your GitHub repo
- No build settings needed — framework preset: **Other**
- Click Deploy

### 3. Add your Anthropic API key
After the first deploy:
- Go to your project in Vercel → **Settings** → **Environment Variables**
- Add a new variable:
  - **Name:** `ANTHROPIC_API_KEY`
  - **Value:** `sk-ant-...` (your key from console.anthropic.com)
  - **Environments:** Production, Preview, Development
- Click Save
- Go to **Deployments** → click the three dots on your latest deploy → **Redeploy**

That's it. The app is live. Users never see or enter the API key — it lives in Vercel and is used server-side by the `/api/claude` edge function.

## How It Works

```
Browser → POST /api/claude → Vercel Edge Function → Anthropic API
                              (injects API key here)
```

The edge function (`api/claude.js`) reads `ANTHROPIC_API_KEY` from Vercel's environment, forwards the request to Anthropic, and streams the response back to the browser. The API key is never exposed to the client.

## File Structure

```
├── index.html        # The entire frontend app
├── api/
│   └── claude.js     # Vercel edge function — API proxy
├── vercel.json       # Vercel config
└── README.md
```

## Usage

1. Open the app URL
2. Choose **On-Page Optimization** or **Net New Content**
3. Follow the conversational workflow:
   - Primary keyword → supporting keywords → page URL or HTML upload
   - Live SERP research with competitor analysis
   - Intent validation and keyword mapping
   - Optimization draft (Daydream-styled, renders inline)
   - Client feedback via JSON upload
