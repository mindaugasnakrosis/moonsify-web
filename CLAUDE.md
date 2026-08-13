# Moonsify — moonsify.com

Landing page + SEO blog for **Moonsify sleep patches** (rebranded from "Restify" — old name may linger in old branches/PRs). Run by Mindaugas and his wife; launched August 2026 for an Amazon + off-Amazon brand launch.

## Product facts (source of truth for copy)

- 30 patches per pack = 1-month supply, $25.95
- Ingredients per patch: Melatonin 7 mg, Magnesium Malate 41.32 mg, Valerian Root 27 mg, Hops 16.53 mg
- 100% drug-free; adults only
- Keyword research: `~/Downloads/bullet_points.txt` (Amazon listing bullets + used/unused search phrases)

## Stack & deploy

- **Pure static HTML/CSS, no build step, no JavaScript.** Keep it that way.
- Deployed via **GitHub Pages legacy build** from `main` branch root at https://moonsify.com (repo: `mindaugasnakrosis/moonsify-web`).
- **Deploying = push to `main`.** Wait for build via `gh api repos/mindaugasnakrosis/moonsify-web/pages/builds/latest --jq .status` — check `builds/latest` (not the `/pages` status, which can report the *previous* build as "built" before the new one starts). CDN caches HTML ~10 min; verify with a `?v=N` cache-buster.
- **Remote must stay HTTPS** (`https://github.com/mindaugasnakrosis/moonsify-web.git`). The machine's SSH key belongs to a different GitHub account (`MindaugasNakro`) that has no access; `gh` is logged in as `mindaugasnakrosis` and handles HTTPS auth. If push is rejected with "denied to MindaugasNakro", run `git remote set-url origin https://github.com/mindaugasnakrosis/moonsify-web.git`.
- GitHub's Pages API sometimes commits CNAME changes directly to `main` (e.g. "Create CNAME") — `git fetch` + merge before pushing if rejected.
- DNS: Hostinger. `@` A records → 185.199.108/109/110/111.153; `www` CNAME → `mindaugasnakrosis.github.io`. HTTPS enforced; cert auto-renews.

## Structure

- `index.html` — landing page, all CSS inlined. JSON-LD: Product, FAQPage, Organization + WebSite.
- `blog/` — six articles (each `blog/<slug>/index.html`) + `blog/index.html` + shared `blog/blog.css`. Each article: Article + BreadcrumbList JSON-LD, canonical, OG tags, Key Takeaways box, product CTA card, related-posts grid, Sources section.
- `sitemap.xml` — update `<lastmod>` and add a `<url>` for every new page.
- Images in `images/` — resize with `sips -Z 1200` / `-Z 640` (srcset pair); never commit multi-MB originals.

## Content rules (important)

- **Supplement claim compliance:** structure/function claims only ("supports restful sleep", "helps ease occasional sleeplessness"). Never disease-treatment claims ("treats/cures insomnia") — FDA/FTC risk. Every page keeps the FDA disclaimer footer.
- **Citations must be real and verified.** All 16 PubMed links in the blog were verified against NCBI E-utilities (esummary) on 2026-08-13. When adding citations, verify the PMID resolves to the exact paper before publishing (PubMed HTML blocks scrapers; use the E-utilities API).
- **No fabricated reviews/ratings** — no aggregateRating schema until real reviews exist.
- New blog articles: copy an existing article as template, add to `blog/index.html`, `sitemap.xml`, and cross-link from 2–3 related articles.

## Pending TODOs (as of 2026-08-13)

1. **Amazon ASIN**: all "Buy on Amazon" buttons point to `https://www.amazon.com/dp/PLACEHOLDER` — replace when the listing is live (grep for `PLACEHOLDER`). Prefer an Amazon Attribution link (Brand Referral Bonus).
2. **support@moonsify.com** — site links to it; mailbox/forwarding not confirmed set up in Hostinger.
3. **Google Search Console + Bing Webmaster** — user was instructed to verify domain (DNS TXT in Hostinger) and submit `sitemap.xml`; not yet confirmed done.
4. **restifyhealth.com** — if still owned, set Hostinger domain forwarding → moonsify.com to preserve old links.
5. **Social profiles** — none exist; when created, add as `sameAs` in the Organization JSON-LD in `index.html`.
6. **Content cadence** — goal ~1 article/month; mine Amazon customer Q&A/reviews for topics once they exist.
