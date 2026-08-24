# Liberation Times → Google News: Action Plan

**Prepared 2026-08-24 · Site: [liberationtimes.com](https://www.liberationtimes.com/) (Squarespace)**

> **Reality check:** There is no Google News application anymore. Google **automatically** considers publishers for the News tab and Top Stories based on what its crawler finds on your site. Your content and traffic are already there — what's missing are the machine-readable **trust signals** Google's policies require. Think of these as health checks: right now, several are failing.

## Scorecard

| ✅ Working | ❌ Missing / Failing |
|---|---|
| Bylines + dates on every article | About page, masthead, staff info — **none exist** |
| HTTPS, clean URLs, sitemap.xml | Editorial standards, corrections policy, ownership/funding disclosure |
| ~1,000-word substantive articles | Contact page is a bare email — no entity name or address |
| No ads, no paywall, no clickbait | Author byline links to a page **robots.txt blocks Google from crawling** |
| Real traffic + engaged X audience | News sitemap, NewsArticle structured data — none |
| | Title tag ≠ headline on articles; dates missing year |

## 🔴 P0 — Trust pages (do this week, all native Squarespace pages)

Google News content policy explicitly requires clear author, publication, and contact information. This is the #1 blocker.

1. **About page** — who Liberation Times is, mission, what you cover, since when.
2. **Author bio page for Christopher Sharp** — credentials, photo, background, email, X link. Then make every byline link **here**, not the current `/?author=...` archive URL (robots.txt blocks `author=` URLs, so Google literally cannot see the only author page you have).
3. **Editorial standards + corrections policy** — how you verify claims, how you handle anonymous sources, how readers report errors, how corrections are displayed.
4. **Ownership & funding** — who owns the site; state that it's reader-funded via Patreon/PayPal.
5. **Upgrade contact page** — keep the email, add publication/entity name and a contact form.
6. **Link all of these in the footer navigation** so they appear on every page.

## 🔴 P0 — Google Search Console (30 minutes)

Verify the domain at [search.google.com/search-console](https://search.google.com/search-console) (Squarespace: Settings → Domains gives you the DNS record). The **Google News performance report** inside Search Console is the definitive signal that inclusion has started. Watch it weekly.

## 🟡 P1 — Technical fixes (next 2 weeks)

- **NewsArticle structured data:** Squarespace outputs generic blog markup. Add NewsArticle JSON-LD (headline, author, datePublished, dateModified, publisher) via Settings → Advanced → Code Injection.
- **News sitemap:** Squarespace can't generate one. Use an external news-sitemap generator/service and submit it in Search Console. Spec: only articles from the **last 2 days**, max 1,000 URLs, with publication name, language, date, and title tags.
- **Title consistency:** make the SEO title match the on-page headline (edit per-post SEO title field).
- **Dates:** show full dates with year; when a story is updated, show an "Updated" date.

## 🟢 P2 — Content & distribution (ongoing)

- **Sourcing hygiene:** UAP coverage gets extra scrutiny. Link primary documents (FOIA records, filings), name sources where possible, and clearly label analysis vs. news reporting. Anonymous "sources tell Liberation Times" as the only support is the biggest content-quality risk.
- **Topic sections:** add nav categories (Congress, Pentagon, FOIA, Interviews) — helps Google classify the site as a news publication, helps readers.
- **Own your audience:** today, distribution is X-only — a **single point of failure**. One algorithm change or account issue takes traffic to zero. Add a newsletter (Squarespace Email Campaigns or Substack) and let Google News become the second leg.

## 30-day roadmap

| Week | Focus |
|---|---|
| 1 | All five trust pages live + footer links; Search Console verified |
| 2 | Bylines re-pointed to bio page; SEO titles aligned; full dates |
| 3 | NewsArticle JSON-LD via Code Injection; news sitemap live + submitted |
| 4 | Topic sections; newsletter signup; review Search Console news report |

## How you'll know it's working

Search Console → Performance → **News**: impressions appearing there means Google News inclusion. Then watch for Top Stories appearances on UAP queries, and a referral mix that no longer depends on X alone.

---

*Printable version: [`onepager.html`](onepager.html) · Requirements & audit detail: [`PRD.md`](PRD.md)*
