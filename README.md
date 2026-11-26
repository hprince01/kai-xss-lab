# 🔐 Kai XSS Lab — Stored Cross-Site Scripting, Explained Safely

**Try it live → [hprince01.github.io/projects/xss-lab](https://hprince01.github.io/projects/xss-lab/)**

An interactive web-security lab that shows **how stored XSS works and how to stop it**, by letting you attack a fake comment board inside a sandbox and then switch on real defences.

## How it works
1. **Attacker** — post a comment or pick one of 6 harmless test payloads (HTML injection, `alert()`, session read, defacement, `<script>` tag, fake login overlay)
2. **Database** — see the comment stored exactly as typed; suspicious input is flagged
3. **Victim’s browser** — a fake blog renders the comments for visitors, using one of 4 defences:

| Defence | How it renders | Result |
|---|---|---|
| None | `innerHTML` | Scripts run — exploited |
| Output encoding | `textContent` | Everything shown as text — blocked |
| Sanitizer | Allowlist of safe tags, attributes stripped | Dangerous parts removed — blocked |
| CSP | `innerHTML` + `script-src 'nonce-…'` | Scripts blocked, but HTML/CSS tricks still work |

**“Visit as another user”** reloads the page as someone else to show why *stored* XSS hits every visitor. A live security log, a results table, vulnerable-vs-fixed code and a prevention checklist explain each result.

## Safety
- The victim page runs in an `<iframe sandbox="allow-scripts">` **without** `allow-same-origin`, so payloads cannot reach the real page, its cookies or storage (verified: access throws `SecurityError`).
- The “session token” is fake and nothing is sent over the network.
- **Only test sites you own or have written permission to test.**

## Built with
Vanilla JavaScript · sandboxed iframes + `srcdoc` · Content-Security-Policy with nonces · `postMessage` · `DOMParser` allowlist sanitizer · no libraries

## Learn more
[OWASP: Cross-Site Scripting](https://owasp.org/www-community/attacks/xss/)

---
Built by **Prince Hirwa Rutagengwa · [Kai Labs](https://hprince01.github.io/)** — Kigali, Rwanda.
