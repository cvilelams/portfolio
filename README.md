# Carolina Vilela — Portfolio

Static portfolio built from `design-system.css` and `cursor-portfolio-briefing.md`.

## Structure

```
novo/
├── index.html              ← Home (start here)
├── about.html
├── contact.html
├── work/
│   ├── batch-printing.html
│   └── expired-tags-research.html
├── css/
│   └── design-system.css
├── assets/images/          ← Add project screenshots here
└── cursor-portfolio-briefing.md
```

## Preview locally

Open `index.html` in the browser, or run a simple server:

```bash
npx serve .
```

## What to customize next

1. **Contact** — Replace `hello@example.com`, LinkedIn, GitHub, and resume PDF link in `contact.html` and footer.
2. **Experience** — Update company names, dates, and descriptions in `index.html`.
3. **Images** — Add photos to `assets/images/` and reference them in project cards and case studies.
4. **Copy** — Refine case study narratives in `work/*.html` with your real project data.
5. **Deploy** — Push to GitHub and enable GitHub Pages, or deploy folder to Netlify/Vercel.

## Design rules (from briefing)

- Only **Syne** + **DM Mono**
- **Accent blue** max ~3 uses per page
- **No border-radius**, no box-shadow
- Card hover: `background: var(--surface-2)` only
