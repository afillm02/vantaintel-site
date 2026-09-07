---
name: vanta-brand
description: Vanta Intelligence brand and design system. Use for ANY UI, copy, or visual work in the Vanta app (vantage-intelligence) or the marketing site (vantaintel-site) — components, screens, pages, emails, chips, empty states, error text, taglines. Loads the tokens, typography, motion doctrine, voice, approved lines, and Vanta-specific anti-patterns from DESIGN.md at the repo root.
---

# vanta-brand

Read `DESIGN.md` at the repository root in full before writing any UI code or user-facing copy. It is the source of truth for color, type, layout, motion, voice, approved taglines, and anti-patterns. If `DESIGN.md` is missing, stop and say so.

## Non-negotiable rules

1. Three typefaces only: Playfair Display (headlines), IBM Plex Mono (labels and data), Lato (body). Never add a fourth. Never use Inter, Roboto, Arial, Space Grotesk, or system-ui as a visible face.
2. One accent: gold #C8A951. It marks active and primary. Never used as a wash, gradient, or glow.
3. Two registers: the app is dense and quiet (product register); the site is spacious and cinematic (brand register). Do not carry app density onto the site or site spacing into the app.
4. The hidden-founder posture is a design rule: no names, faces, biographies, or "we" stories anywhere. The product speaks as Vanta.
5. Established app idioms are reused, never reinvented: confidence badges, type tags, ACCESS chips, ConfirmSheet, arm-then-confirm, sticky-band doctrine, bottom node nav. Check `docs/UI_STANDARDS.md` in the app repo when it exists.
6. Copy is plain verbs, sentence case, no exclamation marks. CTAs say what happens. Approved taglines come from DESIGN.md; propose new ones as edits to DESIGN.md, not as ad-hoc strings in code.
7. Vanta-specific anti-patterns are as binding as the general ones: no italic-gold word per headline, no `//` eyebrows, no numbered markers on non-sequential content, no invented stats, no fake live indicators, no pricing other than the approved Plans in DESIGN.md, never market the hidden Ops node.
8. Every site section is designed at 390px first and 1280px second and verified by screenshot at 390 / 768 / 1024 / 1280 / 1600 before commit. Every app change is smoke-tested on an iOS-width viewport.
9. Performance is part of finish: no 3D, no WebGL, no particle backgrounds; site JS under 150KB gzipped; LCP under 2.0s on 4G; fonts subset and preloaded; reduced motion respected.
10. When impeccable is installed, run its `audit` on the site build and `polish` on any new app screen before declaring a task done, and report the findings.

## Process for new site sections

Plan tokens and layout against the brief → check the plan against DESIGN.md anti-patterns and the frontend-design defaults list → build → screenshot at the five widths → critique your own output → fix → report what you changed and why.

## Process for new app screens

Find the nearest existing idiom in the app and copy it → apply DESIGN.md product-register rules → smoke on an iOS-width viewport → confirm the sticky band, bottom nav, and confidence/type chips render exactly as elsewhere → report.
