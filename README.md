# JANCH AI

**Pause. Check. Then Act.**

JANCH AI is a privacy-first investor safety prototype for the SANGYAN Hackathon. It screens suspicious investment messages, links, screenshots and browser voice input for explainable fraud and misinformation signals, then routes users to official investor-protection resources.

## What works in the prototype

- Message analysis with explainable safety signals
- Context-aware checks: payment, KYC, private groups, app installation
- URL screening: HTTP, punycode, shorteners, direct-IP and deep-subdomain signals
- Screenshot OCR through Tesseract.js (English OCR in demo)
- Browser voice transcription through Web Speech API where supported
- Safety Card with signal score, reasons, claims, next actions and trusted sources
- Copy Safety Card and Print/PDF actions
- Sample scenarios for a 3-5 minute hackathon demo
- Responsive mobile-first UI
- No database and no login required

## Product guardrails

JANCH AI intentionally does **not** provide stock tips, buy/sell/hold signals, price predictions, broker promotion or investment-product upsells. The prototype asks users to verify information rather than directing a financial decision.

## Important prototype note

The current version uses a transparent client-side screening engine for the hackathon prototype. It is not a fraud probability model and it is not a legal/compliance verdict. A production architecture can replace or augment the screening engine with an approved backend classifier + retrieval layer using official sources, while retaining the same UX and guardrails.

## Run locally

This is a static site. You can open `index.html` directly, but a local server is recommended because some browser APIs work more reliably over HTTP.

```bash
python -m http.server 8080
```

Then open `http://localhost:8080`.

## Deploy on Vercel

1. Create a **public GitHub repository**, for example `janch-ai`.
2. Upload this folder so `index.html` is at the repository root.
3. Import the repository in Vercel.
4. Framework preset: **Other**.
5. Build command: leave empty.
6. Output directory: `.` (or leave default for static site).
7. Deploy.

`vercel.json` is included as a static deployment hint.

## Deploy on Netlify

The project includes a `netlify.toml`. Drag the folder into Netlify Drop or connect the GitHub repository.

## Suggested production architecture

```text
Browser
  -> Input normalisation
  -> Local pre-checks
  -> Secure API
      -> multilingual text / OCR / ASR
      -> claim extraction
      -> scam + misinformation classifier
      -> retrieval over approved official sources
      -> evidence linker
      -> policy / guardrail layer
  -> Safety Card
      -> verify entity
      -> official guidance
      -> complaint/report route
```

## Demo scenario

Use the **Guaranteed returns** sample in the app, then press **Run JANCH analysis**. The result should surface multiple signals such as guarantee language, direct payment request, urgency, authority-claim and private-group signals, followed by official verification routes.

## Suggested live-demo narration

> “A first-time investor receives a Telegram message promising guaranteed returns and asking for an immediate UPI payment. Instead of telling the user to invest or not invest, JANCH first identifies the red flags, explains why they matter, and sends the user to official verification and grievance routes. The product creates a pause between persuasion and payment.”

## Current external route links used by the prototype

- SEBI Investor: https://investor.sebi.gov.in/
- SEBI Intermediary Search: https://siportal.sebi.gov.in/intermediarysearch
- SACHET: https://sachet.rbi.org.in/
- SEBI SCORES: https://scores.sebi.gov.in/

## Submission mapping

- **Track A:** Digital Fraud & Scam Resilience
- **Track E:** Misinformation & Content Literacy
- Bharat-first: simple language, mobile responsive UI, screenshot + voice input
- Trust: explainable reasons, trusted source routing, no investment advice
- Feasibility: static prototype deployable as-is, extensible to an approved AI/RAG backend
