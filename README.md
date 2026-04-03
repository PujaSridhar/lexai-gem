# LexAI — Contract Intelligence Platform

AI-powered contract analysis with a multi-agent pipeline. Drop in any contract and get clause-by-clause risk scoring, red flag detection, missing clause identification, and negotiation strategies in seconds.

## Architecture

```
📄 Input → § Triage → ¶ Summary → ┌ ⚖ Clauses  ┐ → ⇌ Negotiate → 📊 Report
                                   └ ⚑ Red Flags ┘
                                     (parallel)
```

5 specialist agents • 4 API calls (2 parallel) • ~15-25s total

## Features

- **PDF & text upload** — paste or upload contracts
- **5-stage AI pipeline** — classify, summarize, clause analysis, red flags, negotiation
- **Live telemetry** — token counts, timing per agent, pipeline status
- **Risk scoring** — 4 sub-scores (fairness, clarity, completeness, enforceability)
- **Export** — downloadable HTML report
- **MoJo Score** — output ÷ human time metric

## Deploy to Vercel

1. Push this repo to GitHub
2. Import to [vercel.com](https://vercel.com)
3. Add environment variable: `GEMINI_API_KEY` = your key from [aistudio.google.com](https://aistudio.google.com)
4. Deploy

The serverless function in `api/analyze.js` proxies requests to Gemini, keeping your API key server-side. Users never need to enter an API key.

## Local Development
Open `public/index.html` in a browser. Without the Vercel backend, the app will prompt for a Google AI API key (stored in memory only).

### Vercel local server

Run the Vercel local dev server to test the `api/analyze.js` function locally.

1. Install dependencies:
```bash
cd "/Users/Pujasridhar/Downloads/LexAI Contract Analysis"
npm install
```

2. Start Vercel locally (recommended):
```bash
npx vercel dev --listen 3000
```

Alternatively you can run the npm script:
```bash
npm run vercel:dev
```

3. Create a `.env` file with your Gemini API key:
```bash
echo 'GEMINI_API_KEY=your_gemini_key_here' > .env
```

4. Test the endpoint:
```bash
curl -sS -X POST http://127.0.0.1:3000/api/analyze \
  -H "Content-Type: application/json" \
  -d '{"systemPrompt":"You are a contract analyst.","userPrompt":"Summarize key obligations."}'
```

Notes: I renamed the `dev` script to `vercel:dev` in `package.json` to avoid a recursive invocation error when running `vercel dev`.

## Tech Stack

- React 18 (CDN, no build step)
- Gemini 2.5 Flash (via Google AI API)
- Vercel Serverless Functions
- Zero dependencies

## License

MIT
