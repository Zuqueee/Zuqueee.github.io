<div align="center">

# Lucas Zuque

### GoHighLevel automation · conversion tracking · paid media
#### for U.S. home-service contractors

[![Live site](https://img.shields.io/badge/live-zuqueee.github.io-1f6feb?style=flat-square)](https://zuqueee.github.io)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-lucas--zuque-0a66c2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/lucas-zuque-219454226/)
![Availability](https://img.shields.io/badge/available-Upwork%20%26%20direct-2da44e?style=flat-square)
![Timezones](https://img.shields.io/badge/working-U.S.%20time%20zones-6e7781?style=flat-square)

**[→ Read the full portfolio at zuqueee.github.io](https://zuqueee.github.io)**

</div>

---

## Your CRM is full of leads it can't do anything with

Most GoHighLevel accounts I open aren't broken in a way the dashboard shows you. The workflows run.
The automations say *completed*. And the contacts underneath them are missing the fields that decide
whether a lead is worth calling, the phone numbers are stored as text the dialer can't use, and the
ad platform is being trained on a form submit instead of a booked job.

Nothing in the interface tells you this. You find it by reading the payload.

That's the part most GHL freelancers can't reach. They can build what you describe, but when the data
arrives wrong they're stuck — because fixing it means reading a webhook body, not dragging a node.
I write the code, so I fix it at the layer where one change covers every landing page instead of
fifteen separate rebuilds.

And because **I buy the media too**, I know what the pipeline is *for*: getting a clean, high-match
conversion signal back to Meta and Google so the campaign optimizes toward revenue instead of noise.

---

## Results, measured

| | | |
|---|---|---|
| **~$900k** | Signed work closed from appointments I booked | Two contractor accounts, 2026 |
| **16 / week** | Appointments booked against a contract asking 15 per *month* | Metal building, FL — at $13.52 CPL |
| **20 / 18** | Contracted appointment package delivered, 30 days early | Siding, Fall River MA |
| **6.1 → 9.0** | Event Match Quality after rebuilding one contractor funnel | ~20 landing pages normalized |
| **46.7%** | Lead-to-appointment on that funnel — 42 booked from 90 leads in 30 days | Leads arriving fully qualified |
| **1,000+** | Ad accounts across five agency portfolios | 5 years in paid acquisition |

Every number on the live page is one I measured in production. Where a figure is still unverified it
renders in red with a dotted underline, so it cannot ship by accident.

---

## Case studies

Full write-ups — context, diagnosis, intervention, result — are on the
**[live page](https://zuqueee.github.io)**. Short version:

### 1 · Two flights, 153 landing page views, zero leads. The budget was on the wrong product.
**GTF Construction LLC** · metal buildings & kitchens · Palm Beach / Martin, FL ·
[read it →](https://zuqueee.github.io/#case-gtf)

A kitchen campaign had burned $713 across two flights for 153 landing page views and not one lead.
The reflex read is broken tracking, and I wrote that conclusion first — then checked it against the
n8n execution log and the Meta Marketing API and **found it was wrong**: on the same pixel, the same
workflow and the same CRM location, the other product line had taken 92 leads from 628 views. Three
things were actually killing it — 39% of its traffic was Audience Network, the audience was ten ZIP
codes at frequency 4.02 in six days, and the ad set was optimizing toward a custom conversion that
had never fired once, so the model had no converter to find lookalikes of.

> Week of Oct 26 – Nov 1: **$351.49 spend → 26 leads at $13.52 → 16 booked appointments**, against a
> contract asking 15 a month. Roughly **$22 per booked appointment on a $150 target**.
> **~$700k** closed from this account's appointments.

### 2 · Three leads vanished between Meta and the CRM, and nothing logged an error.
**Correia Construction Inc** · siding · Fall River, MA ·
[read it →](https://zuqueee.github.io/#case-correia)

Two days after launch Meta reported 3 `Lead` events and the CRM had none. The landing page was
submitting through `navigator.sendBeacon` with a JSON body — which CORS rejects as a non-simple
request, **silently**. No console error, no failed request, nothing in any log. I moved the submit to
a plain `fetch` and made the pixel's `Lead` fire *after* the 200, so the dashboard can no longer
report a lead the CRM doesn't have. Then I built the offer the account was missing, from 51 siding
ads across MA and RI and census-level territory data that split the campaign in two.

> Mid-September: **1 of 18 appointments** with 70 days left — the pace had to multiply **7.3×**.
> November 1: **20 of 18, a month before the contract date.** **$200k** closed in signed siding work.

### 3 · The leads were arriving. The qualification wasn't.
~20 contractor landing pages · GoHighLevel + n8n + Meta CAPI ·
[read it →](https://zuqueee.github.io/#case-qualification)

Volume looked healthy, cost per lead looked fine, and sales kept saying the leads were garbage. GHL
matches inbound payloads **by key name** — and several pages were sending qualification answers
nested, or under aliases the CRM had never seen (`project` instead of `service`). Those contacts
landed with zero qualification fields, while the conversion event fired on submit regardless. Rather
than wait on deploys I didn't control, I wrote **one normalizer at the ingestion layer**: unnests
payloads, resolves field aliases, splits names across every casing GHL expects, normalizes phone to
E.164, and injects IP, user agent and source URL to lift match quality. Tested against seven real
payload shapes — 7/7 recovered the full set. Retroactive, no deploy required.

> **6.1 → 9.0** Event Match Quality · **42 booked appointments from 90 leads in 30 days** (46.7%) ·
> one change covering every page.

### 4 · Optimizing toward a booked appointment, not a form fill.
Pay-per-appointment · ~120-day sales cycle ·
[read it →](https://zuqueee.github.io/#case-optimization)

Remodeling contractors paid per qualified appointment, where the close can land four months after
the click — far outside the window the algorithm learns from. Optimizing on the purchase starves the
campaign; optimizing on the raw lead is cheap and dumb. I mapped **progressive server-side events to
GHL pipeline stages** and made *appointment booked* the target, which fits inside the 7-day click
window. To avoid learning limited, I ran the new event in parallel with the old one until it cleared
50 conversions a week for two consecutive weeks, then switched and retired the proxy. The purchase
event stayed live for ROAS measurement only, never for optimization.

> **Zero days in learning limited** during the switch.

### 5 · One buyer, thirty-two accounts, no guessing which one is drifting.
Local services · sole media buyer ·
[read it →](https://zuqueee.github.io/#case-reporting)

At that count the bottleneck stops being optimization skill and becomes **attention allocation**. I
built the reporting layer instead of opening dashboards: an automated weekly pull of spend, leads and
booked appointments per client, resolved into cost per appointment and lead-to-appointment rate week
over week — the two numbers that tell you whether an account is degrading or just noisy.

> Optimization time went to the accounts that had actually moved, and the same layer became the
> source of truth for renewal conversations, because the client and I read identical numbers.

---

## What I work on

<table>
<tr><th align="left" width="50%">GoHighLevel & automation</th><th align="left" width="50%">Tracking & paid media</th></tr>
<tr valign="top"><td>

- **Sub-account architecture** — snapshots, multi-location rollout, per-location custom field mapping
- **Pipelines & workflows** — stage-triggered automations, round-robin assignment across rep pools, kill switches
- **Inbound webhooks** — field mapping, payload normalization, the aliasing failures that silently blank your CRM
- **Calendars & appointments** — booking as the conversion signal, not an afterthought
- **n8n** — the bridge between landing page, CRM and ad platform; hashing, deduplication, external APIs
- **GHL API & Private Integration Tokens** — bulk audits and rollouts across sub-accounts

</td><td>

- **Meta Conversions API** — server-side events, deduplication by event ID, Event Match Quality tuning
- **Meta Ads** — lead gen and e-commerce, Advantage+, account structure, creative angle testing
- **Google Local Service Ads** — the highest-intent channel in U.S. home services
- **Google Search** — intent mapping, negative discipline, Quality Score, budget efficiency
- **Reddit Ads** — a channel almost nobody has actually bought
- **GA4, GTM, SQL, JavaScript, Python** — event taxonomy, reporting layers, landing pages built rather than briefed

</td></tr>
</table>

### Field notes worth reading before you hire anyone for GHL

The live page documents six failures that **don't show up as errors** — the ones that quietly cost
leads for months: webhooks that match by key name with no warning when they don't; snapshots that
preserve pipeline IDs but *not* custom field IDs; phone numbers that look correct and are dead
strings to the dialer; name mapping that varies per sub-account; why pipeline stage changes are the
cleanest conversion trigger you have; and where GHL ends and n8n begins.

**[→ Read the field notes](https://zuqueee.github.io/#ghl)**

---

## Track record

| | |
|---|---|
| **Feb 2026 — present** | **Media Buyer & Automation** · Ruche Digital — U.S. home-improvement contractors. GoHighLevel builds and CRM automation, server-side conversion tracking, landing pages, plus Meta, Google Search and Local Service Ads buying. |
| **Aug 2025 — Jan 2026** | **Traffic Manager** · 5Company — Reddit Ads campaign launch and optimization. |
| **Jun 2024 — Aug 2025** | **Traffic Manager** · Advanced Marketing — up to 25 accounts. Campaign launch and optimization, e-commerce performance analysis, pixel and API configuration, CRM automation. Ran commercial training and monthly client reviews. |
| **Sep 2023 — May 2024** | **Traffic Manager** · Jingle Agency — sole media buyer for 32 local-business accounts, end to end. |
| **Oct 2022 — Jun 2024** | **Data Manager** · Unect Jr. — owned paid and organic acquisition for the firm. |

**B.Sc. Computer Engineering** · Universidade Tecnológica Federal do Paraná (UTFPR) — the reason I
can fix the tracking instead of filing a ticket about it.

**Training** · Claude Marketers, Fundamentals & Design tracks (18 lessons, completed April and July
2026) — AI-assisted marketing workflows. Earlier: Subido Pro (Pedro Sobral, 2021), Conversão Extrema
(Tiago Tessmann, 2022).

---

## How to start

| | | |
|---|---|---|
| **Fixed scope** | **GHL & tracking audit** | I trace one real lead from ad click to CRM record and show you exactly where the data dies — webhook field mapping, custom field integrity, phone formatting, stage triggers, event match quality, and what your campaigns are actually being trained on. → *Written findings, ranked by revenue impact.* |
| **Fixed scope** | **Build the GHL system** | Sub-account, pipelines, stage-triggered workflows, calendar and appointment flow, plus server-side conversion events wired to real pipeline stages — deduplicated and match-quality tuned. Landing page built if you need one. → *Working system, documented, handover included.* |
| **Retainer** | **Run media and maintain the system** | Ongoing buying on Meta, Google Search and Local Service Ads, reported against cost per booked job rather than cost per lead. GHL and tracking maintained as part of the work, not billed separately. → *Weekly numbers, monthly review.* |

> **Fastest way to evaluate me:** give me read access to GoHighLevel and one week of ad data. I'll
> come back with the diagnosis before you commit to anything.

---

## About this repository

This repo is the source of the portfolio itself — a single hand-written page, no framework, no build
step, no dependencies to install.

```
index.html    941 lines · 45 KB · the entire site
README.md     this file
.gitignore
```

| | |
|---|---|
| **Build** | None. `index.html` is the deployed artifact. |
| **Dependencies** | One external request: Google Fonts (Archivo + IBM Plex Mono), with `preconnect`. Everything else — layout, theming, the 90-line script — is inline. |
| **Theming** | Light and dark, following `prefers-color-scheme`, overridable by a toggle that persists the choice in `localStorage`. All colors are CSS custom properties on `:root`. |
| **Motion** | Sections fade in via `IntersectionObserver`, and the effect is skipped entirely under `prefers-reduced-motion: reduce` or where the API is missing. |
| **Print** | A dedicated `@media print` stylesheet turns the page into a clean PDF résumé — `break-inside: avoid` on every case, interactive elements hidden. |
| **Deploy** | GitHub Pages, from `main` at the repository root. Pushing to `main` redeploys. |

**Preview locally** — any static server works, or just open the file:

```bash
git clone https://github.com/Zuqueee/Zuqueee.github.io.git
cd Zuqueee.github.io
python -m http.server 8000     # → http://localhost:8000
```

**Export the PDF** — open the live page in Chrome, `Ctrl+P`, *Save as PDF*, margins **Default**,
background graphics **off**.

---

## Contact

| | |
|---|---|
| **Email** | [lucaszuquee@gmail.com](mailto:lucaszuquee@gmail.com) |
| **LinkedIn** | [lucas-zuque](https://www.linkedin.com/in/lucas-zuque-219454226/) |
| **Upwork** | *profile link pending* |
| **Based in** | Assis, São Paulo, Brazil — working across U.S. time zones |
| **Languages** | Native Portuguese, fluent English |

<div align="center">

**Send me the sub-account. I'll tell you what's actually broken in it.**

</div>
