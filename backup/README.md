# ResumeForge — AI Resume Optimizer

A single-file web app (`resume-optimizer.html`) that uploads a **resume PDF**, sends the extracted text to an **AI provider** you choose, and renders an **ATS-oriented, rewritten resume** with optional suggestions and headlines. You can **download the result as a PDF**.

There is no build step or server required: open the HTML file in a modern browser.

---

## Features

- **PDF text extraction** in the browser (PDF.js) — works best on text-based PDFs, not scanned images without OCR.
- **Multiple AI backends**: Anthropic Claude, OpenAI, Google Gemini, and Groq.
- **Structured JSON output** from the model, rendered into a styled resume layout.
- **Download** via jsPDF + html2canvas (captures the on-screen resume).
- **API keys stay in your browser** — they are not sent to any backend you host; requests go directly from the browser to each provider’s API (subject to that provider’s terms and CORS policies).

---

## Quick start

1. Obtain an API key from one of the providers below.
2. Open `resume-optimizer.html` in Chrome, Edge, or Firefox.
3. Select the provider, paste the key, upload a `.pdf` resume, then click **Optimize My Resume**.
4. Use **Download PDF** when the optimized resume appears.

---

## AI providers (configured in the app)

| Provider | Model used in code | Where to get a key |
|----------|-------------------|---------------------|
| **Claude (Anthropic)** | `claude-opus-4-5` | [Anthropic Console](https://console.anthropic.com/) |
| **OpenAI** | `gpt-4o-mini` | [OpenAI Platform](https://platform.openai.com/) |
| **Gemini (Google)** | `gemini-3-flash-preview` | [Google AI Studio](https://aistudio.google.com/) |
| **Groq** | `llama-3.3-70b-versatile` | [Groq Console](https://console.groq.com/) |

### Notes

- **OpenAI quota / billing**: Errors like “insufficient quota” are account-side (billing, limits, or plan). The app cannot fix that; add credits or use Groq/Gemini/Claude.
- **Gemini “Flash Live”**: Names like *Gemini Flash Live* refer to Google’s **Live** (real-time / voice) API. This app uses the **REST** `generateContent` API with **Gemini 3 Flash** (`gemini-3-flash-preview`) for plain text resume rewriting.
- **Browser + APIs**: Some providers restrict or discourage browser use of secret keys. Prefer running from a trusted machine and review each vendor’s security guidance.

---

## PDF requirements

- Use a **text-based PDF** (selectable text). If extraction yields almost no text, the file may be image-only; fix the source PDF or use OCR elsewhere first.

---

## Troubleshooting

| Issue | What to try |
|-------|-------------|
| “Could not extract readable text” | Confirm the PDF has selectable text; try exporting again from Word/Google Docs. |
| OpenAI quota / billing errors | Check usage and billing on OpenAI; or switch provider in the dropdown. |
| Gemini model / region errors | Confirm the key has access to the configured model in AI Studio; try another key or provider. |
| Download looks cropped or blurry | Large resumes may span multiple PDF pages; zoom issues are inherent to canvas-based export. |
| CORS or network errors | Provider may block browser calls; check console and provider docs. |

---

## Tech stack (loaded from CDNs)

- [PDF.js](https://mozilla.github.io/pdf.js/) — PDF parsing
- [jsPDF](https://github.com/parallax/jsPDF) + [html2canvas](https://html2canvas.hertzen.com/) — PDF download
- Google Fonts — typography

---

## File layout

```
playground/
├── README.md
└── resume-optimizer.html   ← main app
```

---

## License

No license is specified in the project; treat as personal/internal use unless you add one.
