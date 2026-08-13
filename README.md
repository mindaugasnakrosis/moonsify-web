# moonsify.com

Landing page and SEO blog for **Moonsify** — natural sleep patches for adults (melatonin, magnesium, valerian root & hops).

## Stack

Plain static HTML/CSS, no build step, no JavaScript. Deployed via **GitHub Pages** from the `main` branch, served at [moonsify.com](https://moonsify.com). Pushing to `main` deploys automatically.

## Structure

- `index.html` — the landing page (all CSS inlined; Product, FAQ and Organization structured data)
- `blog/` — six research-backed articles + index, sharing `blog/blog.css`
- `images/` — web-optimized product photos
- `CNAME` — custom domain for GitHub Pages
- `robots.txt` / `sitemap.xml` — SEO
- `404.html` — custom not-found page

## Working on this repo

See **CLAUDE.md** for operational details: deploy verification, git remote gotchas, content/compliance rules, and the current TODO list (including the Amazon listing URL placeholder — grep for `PLACEHOLDER`).
