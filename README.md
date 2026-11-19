# LLM Playground — OPSEC LEVEL: BIBISI

A single-file LLM Playground chatbot powered by the Groq API, with a BIBISI theme, a startup screen, and an animated avatar.

**Live file:** `index.html` — open it in a browser, no build step, no server, no hard-coded API key.

## How to use

1. Open `index.html`
2. Watch the BIBISI startup screen, then enter **your own** Groq API key (`gsk_…`) in the dialog
   - The key is never hard-coded, committed, or sent anywhere except Groq
   - It stays in your browser only — use "Remember key in this tab" only if you want it kept for that tab
3. Pick a model (default: `llama-3.3-70b-versatile` — the live model list loads once a key is pasted), write a prompt, and submit
   - `Enter` to submit · `Shift+Enter` for a new line · `Esc` to stop streaming

## Features

- **Groq chat with streaming** — replies stream in, with a non-streaming fallback retry if streaming fails, errors, or returns empty
- **Clean, simple layout** — one header (model picker, LIVE badge, Settings), one chat column, one prompt box
- **Settings & stats in one drawer** — contents taken from a reference playground, without its cluttered 3-column layout:
  - Groq API key + Test & save key, with 401 / 429 / network errors shown separately
  - Temperature (default 0.7), Max tokens (default 300), Stop sequences
  - Web search / Reasoning toggles, gated per model with explanations
  - Prompt Analysis, Speed (time to first token, total, tokens/sec), Token Usage
  - View code (HTML / JS tabs), Copy chat, Reset conversation
- **Animated avatar** — Pepe blinks, follows your mouse, and talks while the model is streaming
- **Interval peeking** — Pepe and V (Guy Fawkes) peek in from the sides and bottom corners every ~15–29 seconds with speech bubbles, non-blocking
- **Pre-filled example** — a few-shot sentiment-classification prompt in the box so first-time users see how prompting works

## Models

Fallback list (live list loads from Groq once you paste a key):

- `llama-3.1-8b-instant`
- `llama-3.3-70b-versatile`
- `openai/gpt-oss-120b` — reasoning, web search
- `openai/gpt-oss-20b` — reasoning, web search
- `qwen/qwen3-32b` — reasoning

## Notes

- Free-tier Groq accounts are capped on tokens per minute — keep Max tokens small while exploring. On reasoning models, that budget includes thinking tokens.
- Input tokens grow every turn because the whole conversation is re-sent on each request — the API remembers nothing between calls.
- Web search is served by Groq server-side for GPT-OSS models only; the toggle is disabled with an explanation for other models.

## Tech

Single self-contained HTML file (HTML + CSS + JS, Google Fonts). Calls Groq's OpenAI-compatible endpoints directly from the browser: `https://api.groq.com/openai/v1/`
