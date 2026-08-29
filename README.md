# QRaksha — Scan Before You Scan

**QRaksha** is a QR-first phishing ("quishing") detector. It decodes what a QR code actually points to — a URL, a UPI payment string, or a WiFi network — and flags the risk *before* you open it, connect to it, or pay through it.

Built for **Build with Bharat 2.0**, National Level Hackathon (NIT Delhi).

🔗 **Live Demo:** https://fastidious-starburst-2f2fe9.netlify.app/#how



---

## The Problem

QR codes are now the default "click" of everyday India — UPI payments, parking, WiFi, menus, delivery slips. But unlike a web link, a QR code hides its destination until *after* you've already scanned it. Attackers exploit this blind spot through **quishing**.

Existing anti-phishing tools (email scanners, browser link-checkers, SMS filters) all assume you already have a visible, clickable URL. **None of them are built QR-first** — leaving one of the fastest-growing scam vectors almost completely unguarded.

Real-world patterns this targets:
- Fake UPI payment QRs pasted over genuine merchant stickers
- Spoofed "parking fine" / challan QR posters
- Fake courier/KYC QR codes on printed slips
- Rogue "Free WiFi" QRs at cafes and public events

## The Solution

QRaksha is a three-part safety layer:

1. **Detect** — Decode any QR (URL, UPI string, WiFi config) and inspect the real destination before it's ever opened: domain reputation, typosquat detection, UPI payee match, redirect-chain trace.
2. **Explain** — A plain-language, color-coded verdict (Safe / Caution / Danger) with the exact reason — no security background needed to understand the risk.
3. **Protect the Community** — Users tag the physical location of a malicious QR. Nearby users are warned before they scan the same code, turning individual scans into a shared, crowdsourced shield.

## How It Works

```
Scan / Upload → Decode → Multi-Layer Analysis → AI Explanation → Verdict + Action → Community Map Update
```

| Step | What happens |
|---|---|
| 1. Scan / Upload | User scans live via camera or uploads a QR image |
| 2. Decode | Client-side decoder (jsQR) extracts the raw payload before anything opens |
| 3. Multi-Layer Analysis | Domain reputation, typosquat check, redirect-chain trace, UPI payee match, WiFi risk flag |
| 4. AI Explanation | Risk signals are turned into a plain-language reason |
| 5. Verdict + Action | Safe / Caution / Danger shown with one-tap "report this QR" |
| 6. Community Map | Reported locations appear on a live map for nearby users |

## Tech Stack

**Frontend**
- React / vanilla JS (mobile-first)
- `jsQR` — in-browser QR decoding
- `navigator.mediaDevices` — live camera scanning
- Leaflet.js — crowdsourced risk map

**Backend** *(planned for full build)*
- Node.js REST API
- Redirect-chain resolver for shortened/obfuscated links
- UPI string parser (`upi://pay` schema)
- PostgreSQL — reports, VPA & domain history

**Detection & Intelligence**
- WHOIS / domain-age lookup
- Levenshtein-distance typosquat matching
- Curated scam-pattern & VPA database
- LLM-based plain-language risk explanation (Claude API)

## Demo Prototype

The current prototype (`/demo`) is a single-file, client-side implementation that demonstrates the full pipeline without needing a backend:

- Real QR decoding via `jsQR`
- Heuristic risk engine: typosquat distance checks, link-shortener detection, UPI VPA validation, WiFi open-network warnings
- Live "terminal" visualization of each check running
- Interactive community map (Leaflet + OpenStreetMap) with seeded reports and a working "report this QR" flow

> Detection rules in the demo are simplified for client-side execution. Production would call live WHOIS/threat-intel APIs and an LLM for explanation generation, as outlined above.

## Unique Selling Points

- **QR-first, not link-first** — built for the exact format every competing tool ignores
- **Physical-world crowdsourcing** — the only layer that maps *where* a malicious QR was physically found
- **UPI-native risk checks** — purpose-built parsing for `upi://pay` strings
- **Redirect-chain X-ray** — follows every hop a shortened QR link takes
- **Zero literacy barrier** — color-coded verdict + one-line explanation, usable by anyone

## Team

| Name | Role |
|---|---|
| Tanisha Dutta | Detection and Intelligence |
|Bhavya| Product and experience |


**College:** SRMIST Ghaziabad,KIET Ghaziabad

## Running Locally

```bash
git clone https://github.com/tan28-hash/qraksha.git
cd qraksha
# open demo/index.html directly in a browser — no build step required
```

## License

MIT — see [LICENSE](LICENSE) for details.
