# CV Tailor

A simple, open source tool for tailoring your CV to a specific job description.

It runs entirely in your browser. Your CV and your API key never leave your device, except to talk directly to Anthropic's API. There's no backend, no database, and no analytics.

## What it does

You paste (or upload) your CV and a job description, and the tool will:

- Reword bullets from your CV using language from the job description, without inventing experience you don't have
- Suggest which roles or skills to emphasise for this particular job
- Rewrite your professional summary to match the role
- Flag any requirements from the job that aren't clearly demonstrated in your CV, so you can address them in your cover letter or interview
- Show you a side-by-side of every change before you commit, so you can spot anything the AI got wrong
- Export the result as a `.docx` file you can edit in Word or Google Docs

## How to use it

1. Open `index.html` in any modern browser. (Or visit a hosted copy if someone has deployed one.)
2. Paste in a Claude API key. See "Getting an API key" below if you don't have one.
3. Upload or paste your CV and the job description.
4. Click "Tailor my CV".
5. Review the side-by-side. Regenerate if you don't like it.
6. Click "Download .docx".

The whole thing is one HTML file. No installation required.

## Getting an API key

This tool uses your own Claude API key, which means:

- You pay Anthropic directly (about 1-3 cents per CV tailored — $5 covers ~150 CVs)
- The author of this tool pays nothing and receives nothing
- Your CV is sent only to Anthropic, never to any third party

To get a key:

1. Go to [console.anthropic.com](https://console.anthropic.com) and sign up
2. Add a small amount of credit (anywhere from $5)
3. Go to "API Keys" and create a new key
4. Paste it into the app

The key starts with `sk-ant-`. It's stored in your browser tab only — close the tab and it's gone.

## Privacy

- Your CV file is parsed entirely in your browser using PDF.js (for PDFs) and Mammoth.js (for .docx files). The file itself never leaves your device.
- Your CV text and the job description text are sent to Anthropic's API for tailoring. That's how the AI works — it needs to see the content.
- Your API key is held in JavaScript memory in the open browser tab. It's not saved to localStorage, not sent anywhere except Anthropic.
- There is no backend, no database, no analytics, no tracking.

If you're handling someone else's CV, treat it accordingly — get their permission before pasting.

## Running locally

You don't need any build step. Just open the file:

```bash
git clone https://github.com/yourusername/cv-tailor.git
cd cv-tailor
open index.html         # macOS
xdg-open index.html     # Linux
start index.html        # Windows
```

Or if you want a local web server (some browsers behave better that way):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Hosting your own copy

This is a static site — single HTML file. You can deploy it for free on:

- **GitHub Pages**: push to a repo, enable Pages in settings, point at the root or `/docs` folder
- **Netlify**: drag the folder into Netlify Drop, you get a URL instantly
- **Cloudflare Pages**: connect to your repo
- **Vercel**: connect to your repo

No environment variables, no build configuration, no server. Just the file.

## What's not in this version

These are honest limitations rather than promises:

- **No OCR**. If your CV is a scanned PDF (an image of text rather than real text), the parser can't read it. Workaround: paste the text manually, or re-export from Word.
- **No memory**. Close the tab and your CV/key are gone. By design — but a future version could add an opt-in `localStorage` toggle.
- **The .docx export focuses on the changed sections** (summary + tailored bullets), not your full CV. The intent is for you to copy the new content into your existing CV. A future version could rebuild the whole document.
- **Claude only**. The code talks directly to Anthropic's API. Adapting it to OpenAI, Gemini, or a local model is straightforward but not done.

## Contributing

Fork it, change it, share it. MIT license — do what you want.

If you want to contribute back, things that would meaningfully improve the tool:

- A "remember my CV" toggle that uses `localStorage`
- Cover letter generation alongside CV tailoring
- OCR for scanned PDFs (Tesseract.js)
- Support for other AI providers as alternatives
- A drag-and-drop file upload zone

## Why this exists

Most CV-tailoring tools online are either expensive subscriptions, require sign-ups that harvest your data, or both. This is the simplest version of the same idea: one HTML file, your own API key, no middleman.

Built to help one person apply for a community support worker role. Open sourced because the problem isn't unique to them.

## License

MIT — see [LICENSE](LICENSE).

## Acknowledgements

- [PDF.js](https://mozilla.github.io/pdf.js/) for browser PDF parsing
- [Mammoth.js](https://github.com/mwilliamson/mammoth.js) for .docx parsing
- [docx](https://github.com/dolanmiu/docx) for .docx generation
- [Anthropic](https://www.anthropic.com/) for Claude
