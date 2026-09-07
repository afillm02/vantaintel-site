# DESIGN.md — Vanta Intelligence

Version 1.0 · September 7, 2026 · Read this before touching any pixel, in either repo (app: `vantage-intelligence`, site: `vantaintel-site`).

## What this is

Vanta is the intelligence layer for the defense industrial base: near-real-time market signal shaped to one reader, a living map of who builds what and who owns whom (ATLAS), a vetted practitioners' network (Connect), the calendar of who will be where (Events), and a private intelligence matrix (Vault) — with an analyst (Ask Vanta, the daily brief) that learns the reader over time.

Audience: business-development, capture, program, and supply-chain professionals in defense — people who read SAM.gov before coffee and distrust anything that looks like consumer software. They pay for time saved and for seeing a move before their competitor does. They notice fit and finish; sloppy means untrustworthy.

Two registers, one brand:
- **Product register** (the app): dense, quiet, precise. A cockpit. Information density is a feature. Color means something.
- **Brand register** (the marketing site): spacious, cinematic, one idea per viewport. The product is the image. Apple-style restraint on a dark ground.

## Color

Base
- `--bg` #0D1117 — the ground. Not #000; not #111.
- `--surface` #1E2530 — cards, panels, sheets.
- `--surface-2` #161B22 — a second tonal step between bg and surface; use it on the site for section alternation.
- `--border` #3D4654 — hairlines, outlines.
- `--text` #E8E6E1 — body. Warm off-white, never pure white.
- `--muted` #7A8290 — secondary text, captions.
- `--inactive` #556070 — inactive tabs, disabled labels.

Accent
- `--gold` #C8A951 — the one accent. Active state, primary action, the mark. Gold is a signal, not a coat: at most one gold element per viewport on the site; in the app it marks "active" and "primary."

Semantic (app-only unless a site section is showing real product)
- `--teal` #5DCAA5 — confirmed, admitted, positive, HIGH confidence, Hire signals.
- `--coral` #E07B5C — attention, waitlisted, contradiction, LOW confidence. Not "error red."
- `--blue` #4A8FA8 (chip) / #4FA8E8 (text) — Contract signals, links in data.
- `--purple` #9D7BCC — Solicitation signals.
- `--orange` #E89B47 — pending review, MEDIUM warnings.

Rules: no gradients as decoration; no glows; no purple-to-blue anything. A gold line, a gold word, a gold button — not gold washes. Dark stays dark on both surfaces; the site does not get a light mode.

## Typography

Three families, three jobs. Never a fourth.
- **Playfair Display** — headlines and product names. Weight 600–700. Tight leading (1.05–1.1) at display sizes. Sentence case on the site ("Know your market before it moves."). On the site, never italicize one word in a headline for emphasis — it is the most recognizable generated-page tell and the current site does it in every section.
- **IBM Plex Mono** — labels, data, chips, timestamps, code-like things. 11–13px in the app. On the site, use it only where the content is actually data (a timestamp, a ticker, a capability count) — never as a decorative eyebrow above a heading, and never with a `//` prefix.
- **Lato** — body. 16–18px on the site, 14–15px in the app. Line length under 75 characters. Line height 1.55–1.65.

Scale (site): 1.25 ratio from 18px body — 18 / 22.5 / 28 / 35 / 44 / 55 / 69 / 86. Hero display 69–86px on desktop, 40–44px on phones. Scale (app): body 14, label 13/11 mono, section heading 20–24 Playfair, node title 28–32.

No all-caps sentences in body or headings. Mono chips and buttons are the exception and are letter-spaced 0.08–0.12em.

## Layout

- Site container 1200px, 24px gutters on phones, 48px on tablets, 80px+ on desktop. Left-aligned copy on desktop; centered only for the single closing statement.
- Breakpoints: 390 (phone), 768 (tablet portrait), 1024 (tablet landscape / small laptop), 1280 (desktop), 1600+ (wide). Every section is designed at 390 first and 1280 second; the other three must not break. Verified by screenshot at all five before any commit.
- App: mobile-first (iOS Safari is the primary device). Sticky-band doctrine — title scrolls, pills + sub-tabs + search stick as one opaque block at z-20. Bottom node nav always visible, active node gold. Sub-tab: Plex Mono 13px, padding 9px 14px, active = gold text + 2px gold underline, inactive #556070.
- Structural devices carry information. Number things only when they are a sequence. Cards only when items are peers. No card nested in a card.

## Motion

- One orchestrated reveal per page load on the site (the hero). Everything else answers the reader's scroll or tap. No fade-and-slide on every section, no hover transforms on every card.
- Easing: `cubic-bezier(0.22, 1, 0.36, 1)` for entrances, 220–420ms. No bounce, no elastic.
- Respect `prefers-reduced-motion`: reveals become opacity-only or none.
- Live data visualizations (ownership graph, signal field) may move continuously if the movement is the data; keep it under 0.5% CPU on a phone and pause when off-screen.
- No 3D, no WebGL, no particle backgrounds. Performance budget on the site: LCP under 2.0s on 4G, total JS under 150KB gzipped, fonts subset and preloaded.

## Components (site)

- Buttons: one primary (gold fill, #0D1117 text, mono, letter-spaced) per viewport; secondary is outlined #3D4654 with #E8E6E1 text. No arrows appended to button text.
- Device frames for product screens: a thin #3D4654 frame with a 12px radius, no fake notch chrome, no shadow halo. Real screens only — never mock data that the product cannot show.
- Chips: mono 11px, outlined, semantic color; the same chips the app uses, so the site teaches the product's vocabulary.
- Forms: the register form lives in the app. The site never collects an email itself.

## Components (app)

Established idioms, do not reinvent: confidence badges (HIGH teal / MEDIUM gold / LOW coral), type tags (M&A gold · Contract blue · Hire teal · Solicitation purple), ACCESS chips (WAIT coral / IN teal), the waitlist screen idiom (centered mark, Playfair heading, Lato body, one input + one gold action, SIGN OUT as a mono text link, the account email as a mono caption), ConfirmSheet for every destructive action (never `window.confirm`), arm-then-confirm for admin writes, swipe right = filing, swipe left = destruction behind confirm.

## Voice

- Plain verbs, sentence case, no filler, no exclamation marks. Say what a thing does, not that it is powerful.
- A CTA says what happens: "Request access," "Verify email," "Admit." The same name through the whole flow.
- The product speaks as "Vanta." Support signs as "Vanta." No first names, no founder, no team page, no "we're a small team" — ever. The hidden-founder posture is a design rule, not a preference.
- Errors explain and direct; they do not apologize. Empty states invite the next action.
- Defense vocabulary is used correctly and sparingly: DIB, capture, solicitation, ITAR/EAR, CUI. Never fake a clearance vibe. Never imply access to controlled information.
- Never say "X for defense," "LinkedIn for," "Bloomberg for." Vanta is described by what it does.

## Approved lines (v1.0 — edit here, not in code)

- Brand line: **See everything. Miss nothing.**
- Hero: **Know your market before it moves.** — Vanta is the intelligence layer for the defense industrial base: near-real-time signal shaped to you, a living map of who builds what, and an analyst that learns you.
- Intel: **Read what matters. Skip what doesn't.** — Near-real-time defense intelligence, curated by AI and shaped to your position. It sharpens as you read.
- Ask Vanta: **Your analyst.** — Analyze, capture, win. Ask anything about your market; it answers from your fingerprint, your Vault, and the whole map — and it learns you as you use it.
- ATLAS: **Find the capability you need. Be found for yours.** — A living map of who builds what and who owns whom — ownership-mapped, contract-verified, attested by the people who work there.
- Connect: **The practitioners' room.** — A vetted community of defense professionals. What's said here becomes intelligence for everyone in it.
- Events: **Know who'll be where, and when.** — Every show and symposium: who's going, who you should meet, and the calendar that gets you there.
- Vault: **Your private intelligence matrix.** — Your documents, your notes, your watch set — analyzed for you alone, feeding Vanta's synthesis.
- Beta: **The map is being drawn now.** — Vanta admits members in small groups. The ones drawing the map get seen first.
- Closing: **Your competitors are reading yesterday's news.**

## Plans (approved Sep 7, 2026 — the only pricing that may appear anywhere)

Public names are Free, Pro, Company, Enterprise. The app's internal tier keys (scout, operator, command, enterprise) are implementation detail and never appear in user-facing text.

- **Free** — permanent. The feed and the daily brief, Connect, Events, ATLAS browse and search, attest your own company, Ask Vanta 10/day, Vault 5 documents.
- **Pro** — $99/month or $990/year, self-serve. Full Ask Vanta, room briefs, Vault 100 documents, ATLAS depth (ownership trees, contract history, capacity intelligence), saved searches and alerts, priority AI.
- **Company** — from $12,000/year (5 seats) to $30,000/year (20 seats), annual, invoiced. A verified ATLAS storefront (claimed profile, verified badge, published capacity attestation, priority in search, who-viewed-you analytics) plus the seats.
- **Enterprise** — custom. Unlimited seats, export and API, SSO.
- **Founding members** — anyone admitted during the beta keeps Pro free through June 30, 2027. This line may appear on the site and in the app's PLAN tab.

Until Stripe is live there is no purchase path; the site shows the plans and the founding-member line, and every plan's action is REQUEST ACCESS.

## Hero demo reader profiles (site)

The hero's live brief flips between these reader profiles, in this order: Executive · Business Development · Capture Manager · Program Manager · Supply Chain · Competitive Intelligence. Six chips, horizontally scrollable on phones. The content behind each is real product output for a representative fingerprint, never invented companies or programs.

## Anti-patterns (Vanta-specific; in addition to impeccable's defaults)

- One italic gold word per headline.
- `//` eyebrow labels, tracked-out all-caps labels above headings, `01 / 02 / 03` markers on non-sequential content.
- Meta strings joined with middle dots on the site (fine in app data rows).
- Stat bars with invented numbers. Fake "LIVE" indicators. Fake feeds.
- Showing nodes the product hides (Ops is hidden; do not market it).
- Any pricing number, plan name, or tier key other than the approved Plans section above. "Scout," "Operator," and "Command" never appear in user-facing text.
- Any name, face, or biography of a person associated with the company.

## Accessibility floor

WCAG 2.1 AA contrast on every text/background pair (the palette above passes at body sizes; check gold-on-bg for small mono). Visible keyboard focus (gold 2px outline, offset 2px). Touch targets 44px minimum. Reduced motion respected. Headings in order. Every image and visualization has a text alternative that states the point, not the pixels.
