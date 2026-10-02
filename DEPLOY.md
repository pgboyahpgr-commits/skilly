# Deploying the site to Vercel

The site is **already live** on GitHub Pages:

    https://pgboyahpgr-commits.github.io/skilly/

That URL works today and needs nothing from you. This file is only for moving
the same site to Vercel, which needs your Vercel login because I cannot
authenticate as you.

## Why GitHub Pages first

Your constraint was $0 and no payment card. GitHub Pages is free, needs no
card, and the GitHub CLI on this machine was already authenticated, so the site
could be published immediately rather than waiting on a login. Vercel's free
tier is also genuinely free, but it requires an interactive browser login that
I cannot perform.

## Moving to Vercel

The `site/` directory is already Vercel-ready: it contains `vercel.json` and
every asset path is **document-relative**, not root-absolute. That matters —
root-absolute paths (`/style.css`) break on GitHub Pages, which serves project
sites from a `/skilly/` subpath. Relative paths work on both, so no rebuild is
needed.

1. Install and log in (one-time):

       npm i -g vercel
       vercel login

2. Deploy:

       cd D:\Games\skilly\site
       vercel --prod

3. Copy the URL it prints.

Vercel will offer to link the existing GitHub repo. If you accept, every
`git push` redeploys automatically. If you decline, run `vercel --prod` again
whenever you want a new build.

## If the privacy policy changes

The policy text is not stored in `site/`. It is rendered from
`src/ui/screens/legal.js` — the same module the app ships — and cached to
`.cache/policy/`. To publish an edit:

    npm run dev                       # in one terminal
    npm run site:policy               # in another: re-extracts the text
    npm run site:build                # regenerates site/

Then commit and push `site/`. Editing the HTML in `site/privacy.html` directly
will be overwritten on the next build.
