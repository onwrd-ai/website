# Onwrd. website

The public site for Onwrd., hosted free on GitHub Pages from this repository
(`github.com/onwrd-ai/website`). Plain HTML and CSS, no build step, no framework.
Push to `main` and the site redeploys in about a minute.

**Live now:** https://onwrd-ai.github.io/website/
**Once the domain is connected:** https://onwrd.ca

Pushing to `main` redeploys automatically. The Actions tab in the repo shows each
deploy; it takes about a minute.

## What's here

| File | What it is |
|---|---|
| `index.html` | Home: hero, problem, approach, two offers, money pits, responsible AI, about, founding clients, FAQ, contact |
| `assessment.html` | The AI Assessment in detail |
| `fractional-ai-officer.html` | The retainer in detail |
| `privacy.html` | Privacy page (PIPEDA-minded, plain language) |
| `404.html` | Shown for a missing page |
| `assets/css/site.css` | All styling. The `:root` block at the top holds every colour, font and spacing value, mirrored from the Onwrd. design system |
| `assets/js/site.js` | Three small jobs: sticky header shadow, mobile menu, fade-in on scroll, plus the contact form send |
| `assets/img/` | Logo lockups, mark, favicons, the social-sharing image |
| `.github/workflows/pages.yml` | The deploy. Don't edit unless Pages breaks |
| `sitemap.xml`, `robots.txt` | For search engines. Update the sitemap if you add a page |

The brand itself lives in the Claude design system:
https://claude.ai/code/artifact/5fcb0505-32ee-4c23-8bdd-7ef50788a7ca

## Launch checklist (things only Matt can do)

Search the files for each bracket and replace it. `grep -rn "\[" *.html` lists them.

- [ ] **`[CALENDLY]`** in `index.html`: your Calendly event link ("AI Clarity Call — 30 min"). Optionally point every "Book a 30-minute call" button straight at it instead of `#contact`.
- [ ] **`[EMAIL]`** in `index.html` and `privacy.html`: the business address once Google Workspace is live (e.g. `matt@onwrd.ca`).
- [ ] **`[FORMSPREE_ENDPOINT]`** in `index.html`: create a free form at formspree.io, paste the endpoint (`https://formspree.io/f/xxxx`). Until then the form posts nowhere; the email link works.
- [x] **`[Headshot]`** — done. `assets/img/matt-walker.jpg` (750×1000) is in place and wired up in `index.html`. Keep full-size originals out of `assets/`; they are gitignored.
- [ ] **`[BIO, …]`** in `index.html`: approve or rewrite the three-sentence draft and remove the brackets.
- [ ] **`[Sample report page, anonymised]`** in `assessment.html`: a blurred screenshot of a real report once one exists. This is the top conversion lever.
- [ ] **Headline**: the hero uses "Know where AI pays off in your business. And where it doesn't." Alternatives if you want to swap: "We fix the process before we automate it." · "AI that your team actually owns." · "The small-business AI partner who tells you what not to buy."
- [ ] **Domain**: register `onwrd.ca` at Cloudflare. In Cloudflare DNS add four `A` records for `@` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` and a `CNAME` for `www` → `onwrd-ai.github.io`, all DNS-only (grey cloud). In the GitHub repo: Settings → Pages → Custom domain → `onwrd.ca`, wait for the check, tick Enforce HTTPS. Then add a file named `CNAME` to this repo containing just `onwrd.ca`.
- [ ] After the domain is live, the `https://onwrd.ca/…` links in each page's `<head>`, in `sitemap.xml` and `robots.txt` are already correct. If you choose a different domain, search-and-replace `onwrd.ca`.

## How to change things

**Change some text.** Open the HTML file, find the sentence, change it, save. Commit and push (or ask Claude Code: "update the hero sub-line to …"). Every page's nav and footer are repeated in each file, so a nav change means editing all five files; Claude Code does this reliably in one go.

**Change a colour, font or spacing.** Edit the `:root` block at the top of `assets/css/site.css`. Those values come from the design system; change them there first so the brand and the site stay in step.

**Add a page.** Copy `assessment.html`, rename it, change the `<title>`, description, canonical link and content. Add a link to it in the nav and footer of every page, and a line in `sitemap.xml`.

**Add the headshot or any image.** Put it in `assets/img/`, reference it as `assets/img/name.jpg`. Keep images under about 300 KB; the site is meant to load in under two seconds on a phone.

**Preview locally.** Open `index.html` in a browser, or from this folder run:

```bash
python3 -m http.server 8080
```

then visit http://localhost:8080.

**Deploy.** Commit and push to `main`:

```bash
git add -A && git commit -m "Update copy" && git push
```

The Actions tab shows the deploy; the site updates within a minute or two.

## Rules the site follows

- The design system is the source of truth for colours, type and components.
- Prices are never shown; "fixed price, quoted on the call" is the line.
- Only the statistics listed in the hub's `CLAUDE.md`, with source and year attached.
- Sentence case, no emoji, no gradients, no stock leaf photography.
- One primary button per view: "Book a 30-minute call".
