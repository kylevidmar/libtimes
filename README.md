# Liberation Times → Google News: Action Plan

**Re-audited 2026-08-26** (first audit 2026-08-24) · Site: [liberationtimes.com](https://www.liberationtimes.com/) (Squarespace)

> **Reality check:** There is no Google News application anymore. Google **automatically** considers publishers for the News tab and Top Stories based on what its crawler finds on your site. Your content and traffic are already there — what's missing are the machine-readable **trust signals** Google's policies require. Think of these as health checks.

## ✅ What changed since 2026-08-24 — big progress

The single biggest blocker is gone. Four of the five P0 trust items were closed by one page.

- **[About Us](https://www.liberationtimes.com/aboutus) is live and linked in the top navigation.** It carries the mission ("establish what is known, what is alleged, what remains unverified"), the editorial approach, an explicit **anonymous-source policy** ("we do not... treat anonymous claims as proof"), a **corrections policy** with a reporting address, an **independence + reader-funding statement**, and a **masthead** naming Christopher Sharp (Founder, Publisher, Editor-in-Chief) and Kyle Warfel (investigative contributor).
- **A real author bio page exists** at `/christopher-sharp` — portrait, British investigative journalist credentials, *Daily Mail* Senior Contributing Journalist affiliation, listed beats, direct email, personal X handle. This is exactly what Google News transparency policy asks for.
- **Article structured data now includes** `datePublished`, `dateModified`, `headline`, `author`, and a `publisher` object with logo.
- **Dates now include a year** on the homepage (`8/19/26`).

## ❌ Still open — verified 2026-08-26

| # | Issue | Evidence |
|---|---|---|
| 1 | **Bylines still point at the robots-blocked archive.** Articles link the byline to `/?author=610434e3…`, and robots.txt still blocks `author=*`. Articles contain **zero** links to the new bio page — so the bio page is orphaned and can't credit the reporting. | 2 of 2 articles sampled |
| 2 | **The bio page is missing from `sitemap.xml`**, and its `<title>` is the leftover template text **"Team 1"** instead of his name. | `/christopher-sharp` absent from 399 sitemap URLs |
| 3 | **Structured data is `@type: Article`, not `NewsArticle`**, and `author` is a plain text string rather than a `Person` with a `url` pointing at the bio page. | Squarespace default markup |
| 4 | **SEO title ≠ on-page headline** — and the *same* JSON-LD block carries both, in conflict. e.g. tag reads "Pressure Mounts on President Trump as UAP Disclosure Advocates Intensify Their Push"; the H1 reads "The Push for UFO Disclosure Intensifies as Pressure Mounts on Donald Trump". | 2 of 2 articles sampled |
| 5 | **No news sitemap.** Zero `news:` tags in `sitemap.xml`; four common news-sitemap paths return 404. | 0 / 399 URLs |
| 6 | **Machine-readable date has no year:** `<time datetime="Aug 19">`. And `dateModified` exists in the markup but no visible "Updated" label is shown to readers. | article HTML |
| 7 | **Footer still lists only** Privacy Policy, Cookies, Get In Touch — no About or masthead link. | site-wide footer |
| 8 | **Contact page unchanged** — bare email, no form, no postal address or legal entity. | `/get-in-touch` |
| 9 | **No newsletter.** Distribution is still X + Patreon/PayPal only. | 0 newsletter blocks |

## 🆕 New since the first audit — needs a decision

- **AdSense is now running site-wide** (publisher `ca-pub-2776497795797303`), including on the About page. "No ads" was previously a strength. Ads are allowed in Google News, but ad density and layout now count toward quality assessment — keep ads out of the top of the article and away from the headline. Separately, **`/ads.txt` is broken**: it 301-redirects to an HTML page instead of serving plain text, so it isn't a valid ads.txt file.
- **Squarespace placeholder text is leaking into crawlable data.** Image captions like *"Make it stand out"* and *"Whatever it is, the way you tell your story online can make all the difference"* appear **1,149 times** across the 399 sitemap URLs. Unfinished-template copy on a news site is a visible quality signal — clear these captions.
- **robots.txt now blocks ~30 AI crawlers** (GPTBot, ClaudeBot, CCBot, Google-Extended, GoogleOther, Bytespider, and others). **This does not affect Google News or Search** — Googlebot and Googlebot-News are not blocked, and `Google-Extended` only governs Gemini training. No action needed; do not "fix" this by unblocking.

## 🔴 P0 — Do this week

1. **Re-point every byline to `/christopher-sharp`.** This is now the highest-value fix on the site: the bio page Google wants already exists, and nothing links to it from the reporting. The current byline target is blocked by robots.txt.
2. **Fix the bio page's SEO title** — change "Team 1" to *Christopher Sharp — Founder, Publisher and Editor-in-Chief* (Page Settings → SEO).
3. **Get the bio page into the sitemap** — it's currently excluded. In Squarespace, make sure the page is not disabled/hidden from navigation-only; add a Masthead link so it's reachable by crawl.
4. **Verify the domain in [Google Search Console](https://search.google.com/search-console)** (Squarespace: Settings → Domains gives the DNS record). The **Google News performance report** there is the definitive signal that inclusion has started. Check it weekly. ← *If this isn't done yet, do it before anything else; it's 30 minutes and it's how you'll measure everything below.*
5. **Add About Us + Masthead to the footer**, alongside Privacy and Cookies, so the trust pages appear on every page.

## 🟡 P1 — Next 2 weeks

- **Upgrade the structured data to `NewsArticle`** via Settings → Advanced → Code Injection: `@type: NewsArticle`, `author` as a `Person` object with `"url": "https://www.liberationtimes.com/christopher-sharp"`, plus `datePublished` / `dateModified`.
- **Align each post's SEO title with its headline** (per-post SEO title field). Conflicting title/H1/JSON-LD values on the same page make Google pick for you.
- **Publish a news sitemap.** Squarespace can't generate one — use an external generator/service and submit it in Search Console. Spec: articles from the **last 2 days only**, max 1,000 URLs, with publication name, language, publication date, and title tags.
- **Clear the placeholder image captions** across published posts.
- **Show full dates with year, and a visible "Updated" line** when a story is revised — `dateModified` is already in the markup, so this is a display change only.
- **Fix or remove `/ads.txt`** so it serves plain text.

## 🟢 P2 — Ongoing

- **Sourcing hygiene.** The About page now *states* a strong sourcing policy — the articles have to visibly match it. Link primary documents (FOIA records, filings, correspondence), name sources where possible, and label analysis vs. news reporting. UAP coverage draws extra scrutiny; a stated policy plus unsourced copy reads worse than no policy at all.
- **Topic sections.** Add nav categories (Congress, Pentagon, FOIA, Interviews) — helps Google classify the site as a news publication, and helps readers.
- **Own the audience.** Distribution is still X-plus-Patreon — a **single point of failure**. One algorithm change or account issue takes referral traffic to zero. Add a newsletter (Squarespace Email Campaigns or Substack) and let Google News be the second leg.
- **Add a founding year to the About page** — "since when" is a transparency signal and is currently the one About-page element still missing.

## Revised 30-day roadmap

| Week | Focus |
|---|---|
| 1 | Bylines re-pointed to `/christopher-sharp`; bio page title fixed + in sitemap; Search Console verified; footer trust links |
| 2 | NewsArticle JSON-LD with `Person`/`url`; SEO titles aligned to headlines; full dates + "Updated" label |
| 3 | News sitemap live and submitted; placeholder captions cleared; ads.txt fixed; ad placement reviewed |
| 4 | Topic sections; newsletter signup; founding year on About; review Search Console news report |

## How you'll know it's working

Search Console → Performance → **News**: impressions appearing there means Google News inclusion has begun. Then watch for Top Stories appearances on UAP queries, and a referral mix that no longer depends on X alone.

---

*Printable version: [`onepager.html`](onepager.html) · Markdown source: [`ONEPAGER.md`](ONEPAGER.md) · Requirements & audit detail: [`PRD.md`](PRD.md) · Change log: [`progress.txt`](progress.txt)*
