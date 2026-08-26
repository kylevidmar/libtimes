# Liberation Times → Google News: Action Plan

**Re-measured 2026-08-26** (first audit 2026-08-24) · Site: [liberationtimes.com](https://www.liberationtimes.com/) (Squarespace 7.1)

> **Reality check:** There is no Google News application anymore. Google **automatically** considers publishers for the News tab and Top Stories based on what its crawler finds on your site. Your content and traffic are already there — what's missing are the machine-readable **trust signals** Google's policies require. Think of these as health checks.

Every number below was re-measured against the live site on 2026-08-26, not carried
forward. Where a measurement changed a previous claim, the correction is stated.

## ✅ Closed — and verified in production

**The trust pages.** [About Us](https://www.liberationtimes.com/aboutus) is live and in the
top navigation, carrying the mission ("establish what is known, what is alleged, what remains
unverified"), the editorial approach, an explicit **anonymous-source policy** ("we do not…
treat anonymous claims as proof"), a **corrections policy** with a reporting address, an
**independence + reader-funding statement**, and a **masthead** naming Christopher Sharp
(Founder, Publisher, Editor-in-Chief) and Kyle Warfel (investigative contributor). A **real
author bio page** exists at `/christopher-sharp` — portrait, British investigative journalist
credentials, *Daily Mail* Senior Contributing Journalist affiliation, listed beats, direct
email, personal X handle. Both are now in `sitemap.xml`; the bio page was absent at the first
audit.

**The bio page's title and description** (was issue 2). It served the template default
`Team 1` with an empty `<meta name="description">`. Now measured live at 77 chars:
`Christopher Sharp — Founder, Publisher and Editor-in-Chief — Liberation Times`, with a
149-char description. `og:title` and `og:description` inherited both, so social shares are
fixed too. The byline fix below now points at a page that actually presents his credentials.

**`code-injection.html`, live in Website Tools → Code Injection → Footer**, and **verified in
production** rather than in a fixture harness. `tools/verify_live.js` loads the live URLs over
the network in headless Chrome with Squarespace's own JavaScript executing — **31 of 31 checks
pass**, re-run 2026-08-26:

| Signal | Measured live |
|---|---|
| Byline `href` | `/christopher-sharp` (not the `?author=` archive robots.txt blocks) |
| Byline `rel` | `author` |
| JSON-LD types on an article | `WebSite`, `NewsArticle` — the old `Article` is **replaced**, not duplicated |
| `<time datetime>` | `2026-08-19`, displayed `Aug 19, 2026` |
| `/aboutus`, homepage | `WebSite` only — no `NewsArticle`, no stray "Updated" line |

It **coexists with the Beyondspace date-format plugin** already in that Footer field. That
plugin's only Squarespace 7.1 selector rule requires `.view-list`, and an article body is
`.view-item`, so it never reaches the article date — but it *does* format the blog list pages,
so it stays. Verified by loading the real plugin from its CDN alongside our snippet (16/16),
including a late probe confirming its selector-listener doesn't overwrite our date afterwards.
**Do not delete that plugin.**

**Still to do on this item:** run Rich Results Test on an article **URL** to confirm Google's
own parser agrees with what the browser sees.

**The global SEO title format.** `%i — Liberation Times` on **Items**, `%p — Liberation Times`
on **Pages**. The appended site name went from 42 characters to **19**, recovering 23 on all
401 URLs in the sitemap for a single edit. Measured live: article 102 chars, bio 77, About 27,
Contact 31, Privacy 33.

**`llms.txt` is live** — 200, **5,048 bytes**, first line `# Liberation Times` — via
Squarespace's native **SEO/AI Visibility → SEO Settings → LLMS.txt** field (7.1 only,
user-written; Squarespace generates nothing). Scoped honestly: llms.txt is a **proposal**, not
a ratified standard, and **no search engine is confirmed to consume one** — OpenAI, Anthropic
and Google publish llms.txt for their own docs, but publishing isn't consuming. Cheap and
plausibly useful for AI answer engines; **not** a Google News eligibility item. Its most
useful content here is a *Sourcing and verification* section telling models that an article
reporting what a source **claims** is not an article establishing the claim is true — the
exact failure mode when UAP coverage passes through a summariser. One tension worth knowing:
robots.txt names **29** AI crawlers, and those agents won't fetch `llms.txt` either. Not
contradictory — blocks target training, llms.txt targets inference-time fetching — but the
real audience is the agents not on that list. Source of truth: [`llms.txt`](llms.txt).

## ❌ Still open — measured 2026-08-26

| # | Issue | Evidence |
|---|---|---|
| 12 | **Homepage `<title>` is bare `Liberation Times`** (16 chars) — the tagline is gone, and it now contradicts two other site-name signals **on the same page**. Google derives the **site name** shown beside every result for the whole domain from these, and its docs say to keep them consistent across the home page. **Fix:** Search Appearance → **Home** tab → `%s \| Reimagining Old News`. | see table below |
| 4 | **Titles still long, though much less so.** Of the 20 newest posts: **9 severe** (>85 rendered chars), **9 marginal** (71–85), **2 fine**. Worst **133**, median **79**. All 9 severe are already hand-written SEO titles, so this is editorial trimming, not a settings fix — goes to Christopher as suggestions. | 20 newest, re-bucketed against the 19-char suffix |
| 7 | **Footer still lists only three links** — Privacy Policy, Cookies, Get In Touch. No About, no masthead. Measured in the JS-rendered DOM, not a plain fetch. | 3 links, `footer_has_about: false` |
| 11 | **`/ads.txt` has no valid file at all.** It 301s to `http://www.liberationtimes.com/s/ads-yhtd.txt` — note **plain HTTP**, not HTTPS — and that target **404s**. AdSense runs site-wide meanwhile. | redirect chain traced |
| 10 | **`/team` is still a live, indexed, contentless template page.** The global title edit gave it a nicer title (`Team — Liberation Times`) without giving it content. In `sitemap.xml`, zero inbound links. | live page + sitemap |
| 8 | **Contact page unchanged** — bare email, no form, no postal address or legal entity. | `/get-in-touch` |
| 9 | **No newsletter.** Distribution is still X + Patreon/PayPal only. | 0 newsletter blocks |
| 13 | **Static pages have no meta description** — `/aboutus`, `/get-in-touch`, `/privacy` and `/team` all return `content=""`, so Google writes its own snippet for your single most important trust page. Posts are fine (all 255 have a description or excerpt; 22 rely on the excerpt). *(New this round.)* | `desc_len: 0` on 4 pages |
| 5 | **No news sitemap** — zero `news:` tags across 401 URLs; four common news-sitemap paths all 404. *(Deliberately skipped — see P2.)* | 0 / 401 |

### Issue 12 in detail — three signals, two answers

| Source | Value |
|---|---|
| `<title>` | `Liberation Times` |
| `og:site_name` | `Liberation Times \| Reimagining Old News` |
| `WebSite` JSON-LD `name` | `Liberation Times \| Reimagining Old News` |

Per Squarespace's docs the Home tab format is `%s` and `%s` is the **site title**, not the
tagline — so editing the Items and Pages tabs shouldn't have touched the homepage. It did,
which means the site title field itself also changed. Recorded as observed behaviour, not a
confident causal claim. The `WebSite` JSON-LD is rendered by JavaScript, so this needs
headless Chrome to see — `node tools/remeasure_dom.js`.

## 🆕 Context and corrections

- **AdSense is running site-wide** (publisher `ca-pub-2776497795797303`), including on the About page. "No ads" was previously a strength. Ads are allowed in Google News, but ad density and layout count toward quality assessment — keep ads out of the top of the article and away from the headline.
- **Placeholder captions — corrected downward twice, now cosmetic.** An early version of this file called the Squarespace demo text a "visible quality signal." Re-measured: *"Make it stand out"* appears **zero times** in rendered article HTML and zero times in `?format=json`. It exists only in `sitemap.xml` image metadata — **735 occurrences across 241 URLs** (a previous count of "1,147 tags" was counting all `image:title` + `image:caption` tags, including legitimate ones; the true figures are 822 `image:title` and 739 `image:caption`). Readers never see it; Googlebot doesn't see it on the page. One reused image, `GSJMeucWUAIpMhE.jpg`, accounts for **100** of the entries by itself and is the best single fix.
- **robots.txt names 29 AI crawlers** (GPTBot, ClaudeBot, CCBot, Google-Extended, GoogleOther, Bytespider, Applebot-Extended, Meta-ExternalAgent, and others). **This does not affect Google News or Search** — Googlebot and Googlebot-News are not blocked, and `Google-Extended` only governs Gemini training. No action needed; do not "fix" this by unblocking. It *does* still block `author=`, which is why the byline had to be repointed.
- **Publishing cadence, re-measured:** 255 posts over 1,836 days = **0.97/week** lifetime, and **1.09/week** over the last 90 days (14 posts). This is the number that makes a news sitemap pointless — see P2.
- **Email authentication is still entirely absent.** MX points at Google Workspace (`aspmx.l.google.com`), but there is **no SPF** (the apex TXT record holds only the Search Console verification string), **no DKIM** (`google._domainkey` → NXDOMAIN), and **no DMARC** (`_dmarc` → NXDOMAIN). *You asked to skip this; it stays documented, not re-argued.*
- **The Search Console TXT record is live and correct:** `google-site-verification=TTiLzj9aUb4cMMoV1URPghlnvT1cFeX1AMMMAH30VYY`. So verification will succeed on the first click — and do **not** add a second copy.

## 🔴 P0 — your actual remaining list

Everything here needs a human in the Squarespace or Google UI. Click-by-click paths:
**[`SQUARESPACE-HOWTO.md`](SQUARESPACE-HOWTO.md)**.

1. **Restore the homepage title — 30 seconds, do this first.** Search Appearance → **Home** tab → `%s | Reimagining Old News`. See issue 12. It's the cheapest item on this list and it affects how the site is labelled in every result.
2. **Verify the domain in [Google Search Console](https://search.google.com/search-console).** **This is not inside Squarespace** — it's a separate Google product; the Squarespace sidebar's **SEO/AI Visibility** panel is a different thing. Choose the **Domain** box, not "URL prefix". The TXT record is already live, so it verifies immediately. The **News** report under **Performance** is the definitive signal that inclusion has started; check it weekly. *Nothing else here gets measured until this property exists* — and its status is still unconfirmed on our side.
3. **Run Rich Results Test on an article URL** — the **URL** tab, not the code input, which won't execute the script. Our own headless check against production already passes 31/31; this confirms Google's parser agrees.
4. **Add About Us + Christopher Sharp to the footer**, alongside Privacy and Cookies, so the trust pages appear on every page. Currently three links, neither of them these.

## 🟡 P1 — next 2 weeks

- **Shorten 9 headlines — as suggestions to Christopher, not edits.** Only 9 of the 20 newest are severe (>85 rendered chars); worst is 133. **Keep the ` — Liberation Times` suffix** — Google's title-link docs *endorse* a site name in the title element ("consider including just your site name at the beginning or end of each `<title>`… separated with a delimiter"), and Google may omit it from the displayed link when it's redundant. Only the headline half needs trimming. Worklist: [`seo-title-worklist.md`](seo-title-worklist.md).
- **Add meta descriptions to the four static pages** (issue 13). `/aboutus` matters most — it's the page Google reads to decide whether this is a transparent publication.
- **Fix `/ads.txt`** — 301s over plain HTTP to a **404**, so no valid file exists while AdSense runs site-wide. Some programmatic buyers treat that inventory as unauthorised, which costs revenue. Most likely a stale URL Mapping; Squarespace now has a native **Settings → Website → Ads.txt File** field, and its docs warn that a prior custom setup "won't be automatically removed or updated" — so remove the old redirect as part of this.
- **Clear the placeholder image captions — cosmetic only.** Sitemap image metadata, never rendered. The one reused image accounts for 100 of 735 entries; start there, and do the 20 newest at most.

*Two items you asked to skip stay listed as open, not re-argued: deleting `/team` (issue 10) and adding SPF/DKIM/DMARC.*

## 🟢 P2 — ongoing

- **Sourcing hygiene.** The About page now *states* a strong sourcing policy — the articles have to visibly match it. Link primary documents (FOIA records, filings, correspondence), name sources where possible, and label analysis vs. news reporting. UAP coverage draws extra scrutiny; a stated policy plus unsourced copy reads worse than no policy at all.
- **Topic sections.** Add nav categories (Congress, Pentagon, FOIA, Interviews) — helps Google classify the site as a news publication, and helps readers.
- **Own the audience.** Distribution is still X-plus-Patreon — a **single point of failure**. One algorithm change or account issue takes referral traffic to zero. Add a newsletter (Squarespace Email Campaigns or Substack) and let Google News be the second leg.
- **Add a founding year to the About page** — the one transparency element still missing there. The oldest post is 2021-08-09, if that's the date you want.
- **News sitemap — deliberately skipped.** Google's docs treat news sitemaps as *optional*, not a prerequisite, and the window is articles from the **last 2 days only**. At 1.09 posts/week such a sitemap would be empty most of the time. Revisit only if cadence rises to several posts per week; the regular `sitemap.xml` (401 URLs, 386 posts) is what Google crawls meanwhile.

## 🛠 Implementation

**Squarespace has no content API** (Commerce endpoints only — no pages, posts, SEO fields,
navigation, or code injection), so the remaining work is UI edits, and **no API key is needed
for any of it**. But the technical issues collapsed into one site-wide paste:

- **[`code-injection.html`](code-injection.html)** — live in Code Injection → Footer since 2026-08-26. Repoints the byline, upgrades `Article` → `NewsArticle` with a `Person` author, fixes dates to include the year, adds the "Updated" line. Four verification layers: real saved article HTML in headless Chrome (25/25); an adversarial re-render test (4/4) confirming a `MutationObserver` restores the fixes if Squarespace 7.1 rebuilds the post header; a coexistence test against the real Beyondspace plugin from its CDN (16/16); and **[`tools/verify_live.js`](tools/verify_live.js) against production over the network (31/31)** — the check the first three structurally could not make.
- **[`SQUARESPACE-HOWTO.md`](SQUARESPACE-HOWTO.md)** — click-by-click, 10 tasks in priority order with a status column, panel names quoted from current Squarespace docs (the SEO panel was renamed, so older guides point at a menu that no longer exists), live verification steps, and what *not* to change.
- **[`llms.txt`](llms.txt)** — pasted into Squarespace's native LLMS.txt field, live at `/llms.txt`.
- **[`seo-title-worklist.md`](seo-title-worklist.md)** — generated from live `?format=json` data: the global format fix (done), the over-length titles, the **10 posts to leave alone**, and the 22 posts relying on an excerpt rather than a real description.

**Re-measurement tooling** — so none of the above has to be re-derived by hand:

| Tool | What it checks |
|---|---|
| `node tools/verify_live.js` | The snippet, in production, with Squarespace's JS running (31 assertions) |
| `node tools/remeasure_dom.js` | Site-name agreement + footer links — both JS-rendered, invisible to a plain fetch |
| `python tools/remeasure.py` | Titles, descriptions, `llms.txt`, robots, `ads.txt` chain, sitemap counts |
| `python tools/print_probe.py 8.0` | Whether `onepager.html` still prints on one page |

## Revised 30-day roadmap

| Week | Focus |
|---|---|
| 1 | ~~Paste `code-injection.html`~~ · ~~bio page title + description~~ · **restore the homepage title** · Search Console verified · Rich Results Test on an article URL · footer trust links |
| 2 | ~~Global SEO title format~~ · 9 severe headlines to Christopher as suggestions · meta descriptions on the four static pages |
| 3 | `ads.txt` fixed (and the old redirect removed) · ad placement reviewed · placeholder captions, starting with the one image worth 100 entries |
| 4 | Topic sections · newsletter signup · founding year on About · review Search Console **Performance → News** |

## How you'll know it's working

Search Console → Performance → **News**: impressions appearing there mean Google News
inclusion has begun. Then watch for Top Stories appearances on UAP queries, and a referral mix
that no longer depends on X alone.

---

*Printable version: [`onepager.html`](onepager.html) · Markdown source: [`ONEPAGER.md`](ONEPAGER.md) · Requirements & audit detail: [`PRD.md`](PRD.md) · Change log: [`progress.txt`](progress.txt)*
