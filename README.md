# Audit Innovation — Landing Page Concept Refresh

A visual and structural refresh of RSM's [Audit innovation](https://rsmus.com/insights/financial-reporting/audit-innovation.html)
insights page. **Every word of the live page's body copy is preserved.** What changes is
the layout, the imagery, and the fact that a visitor now has somewhere to go.

> ⚠️ **Disclaimer** — Independent concept / internal demonstration. **Not affiliated with,
> authorized by, or endorsed by RSM US LLP or RSM International.** All trademarks belong to
> their respective owners. Styling reproduces publicly visible rsmus.com design tokens for
> evaluation purposes; the logo is a CSS approximation, not the official asset. Photography
> is referenced from rsmus.com's public asset library for layout evaluation and is **not
> redistributed with this repository**. Copy tagged in yellow is placeholder, not approved
> RSM messaging.

## Live demo

`https://nightschuy.github.io/rsm-audit-innovation/`

Click **Pitch mode** (top right) for the built-in speaker notes — the diagnosis, what was
added and why, the engagement journey rationale, lead routing, brand-fidelity notes and the
AEM mapping. The page pitches itself in the meeting.

## The problem being solved

The live page is four paragraphs of prose and a video. It has **no call to action anywhere**.
A visitor who reads to the bottom has nothing to do and leaves nothing behind — a brochure
page sitting in an insights funnel.

## What changed

| Change | Why |
|---|---|
| **Two CTAs in the banner** | The banner is the only thing every visitor sees. One goes to the diagnostic, one to the film. |
| **Hero over real RSM photography** | The signature blue headline band now sits on a dark digital-data image instead of flat navy. |
| **Sticky sub-nav with a persistent contact button** | The ask never scrolls away on a long read. |
| **The three pillars become three cards** | They were named in one sentence and then never shown. Now they are the page's spine. |
| **Pull-quote on the pillars sentence** | Lifts the structure out of the prose so it's visible before you read. |
| **A three-stage engagement journey** | See below. |
| **Sticky conversion bar** | Appears once the visitor is past the fold and has not converted. Dismissible. |
| **Resource cards + CTA band + tagline strip** | Gives the page an exit other than the browser back button. |

## The engagement journey

Three stages, each asking for slightly more than the last — progressive profiling rather
than one wall-sized form.

| Stage | Ask | Give |
|---|---|---|
| 1 | One tap, no form | A tailored read on which pillar would change their audit most |
| 2 | Work email + company | A two-page brief on the pillar they picked |
| 3 | Name, title, revenue, audit timing | A 30-minute walkthrough |

**Why stage 1 is not gated:** gating the diagnostic kills completion. Gating the
*explanation* does not — by the time the read appears the visitor is invested and has a
specific question only the brief answers. Same principle as the
[Exit Readiness assessment](https://github.com/nightschuy/rsm-exit-readiness).

### The answer is the lead signal

The pillar someone picks is a routing instruction, not just a content preference.

| Friction picked | Points at |
|---|---|
| Chasing and formatting support | Automation — process and close-cycle work |
| Explaining the same variance twice | Data analytics — data and reporting depth |
| Coordinating across systems and sites | Digital audit experience — multi-entity complexity, usually a larger account |

Every analytics event carries `friction`, so completions attribute to a pillar instead of
one undifferentiated pool.

## Tracking

Events push to `window.dataLayer` for GA4 (open the console to watch them fire):

`page_view_concept` · `page_cta_click` · `diagnostic_select` · `generate_lead` ·
`request_demo` · `video_open` · `journey_abandon` · `journey_restart`

## Tech

Single static `index.html`. No build step, no dependencies, no framework.

### Brand fidelity

Design tokens carried over from the Exit Readiness build, where they were read from the
live rsmus.com AEM stylesheet rather than approximated:

| Token | Value |
|---|---|
| Primary green | `#3f9c35` |
| Headline band | `#009cd9` |
| Primary blue | `#007eb4` |
| Navy | `#27455c` |
| Gray ramp | `#515356` / `#63666a` / `#888b8d` |

Matched from the live site: `border-radius: 0` on every component, headings at weight 300,
buttons at 18px/400, the signature blue headline band over a dark hero, and a **High
Contrast toggle** in a blue utility bar (rsmus.com ships one instead of a dark theme).

Two substitutions, both disclosed in the page footer: **Prelo** is licensed and self-hosted
on rsmus.com, so this uses **Barlow** at the same 300/500/700 weights — swap `--font-sans`
and it is on-brand for real; and the **logo is a CSS approximation**.

### Imagery

Photography is referenced by URL from RSM's own DAM (`rsmus.com/content/dam/rsm/...`)
rather than substituted with lookalike stock, so the concept is evaluated against the real
library. Nothing is copied into this repository.

### AEM mapping

Class names follow the Core Components convention already in use on rsmus.com —
`cmp-globalheader`, `cmp-hero`, `cmp-button`, `cmp-cta`, `cmp-footer` — so this reads as a
component composition rather than a one-off page.

- Hero, CTA band, resource cards and footer map to existing components
- The diagnostic is the one new component: a multifield of options, each with a key, a heading and a body
- Pillar copy, readout copy and form fields are all authorable
- Scoring-free and server-free, so the page can be cached at the edge

### Accessibility

Keyboard operable throughout; `radiogroup` semantics on the diagnostic; visible focus rings;
`prefers-reduced-motion` honoured; High Contrast preference persists per browser.

## Run locally

```bash
python3 -m http.server 4449
```

## Not production-ready

Deliberately. Before this ships:

- Forms do not submit — need a marketing automation endpoint and consent/privacy handling
- Pillar and readout copy is inferred from the source page and tagged yellow; practice teams supply the real wording
- The video is a poster image only — needs the real Brightcove embed
- Resource cards are a sample selection, not a curated set
- Copy needs compliance and risk-management review
