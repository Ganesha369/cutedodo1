# CuteDoDo ($DODO) website

The public website for CuteDoDo, a community meme token on Solana inspired by Dodo, a real Shih Tzu from Chennai.

Preview: https://cutedodo-sol.netlify.app

## Stack

Plain HTML, CSS and vanilla JavaScript in one file. No framework, no build step, no npm dependencies.

```
site/
  index.html                         the whole page (styles and script inline)
  assets/
    dodo.jpg                         hero photo of Dodo
    whitepaper-snapshot.jpg          carousel card 1
    ecosystem-roadmap.jpg            carousel card 2
    liquid-nft-roadmap.jpg           carousel card 3
    CuteDoDo-Whitepaper-v2.3.pdf     downloadable whitepaper
netlify.toml                         Netlify config (publishes site/)
video-plan/design-package.md         parked plan for an optional scroll-driven hero video
```

## Run locally

Any static file server works. From the repo root:

```bash
npx http-server site -p 5173 -c-1
```

Then open http://localhost:5173. Opening `index.html` directly from disk also works, but the live market data needs a real `http://` origin.

## Deploy

`site/` is a static folder, so it can go on any static host (Netlify, Vercel, Cloudflare Pages, GitHub Pages, S3 + CloudFront).

- **Netlify:** connect this repo. `netlify.toml` already sets the publish directory to `site` and there is no build command.
- **Vercel / Cloudflare Pages:** framework preset "Other", no build command, output directory `site`.
- **GitHub Pages:** publish the `site/` folder through a Pages workflow.

## Live market data

The four stat boxes under the hero (price, market cap, liquidity, 24h volume) are fetched in the visitor's browser from the public DexScreener API:

```
GET https://api.dexscreener.com/latest/dex/tokens/2e5bKRHpAixvgE6zUdTf7rigxCq662zq7xvN8Dympump
```

The page picks the pair with the highest USD liquidity and refreshes every 60 seconds. If the request fails, the boxes fall back to a "See chart" state. The code is the `load()` function near the bottom of `site/index.html`. No API key is needed; DexScreener allows about 300 requests per minute per client IP.

## Before going live on the public domain

- [ ] **Confirm the charity figure.** The page says "1% for pet welfare" in headlines (from the whitepaper) and shows the charity wallet at 1.15% of supply (from the old cutedodo.com). The team needs to settle on one wording.
- [ ] **Confirm tokenomics and the wallet list.** The supply split and the 12 public wallets were carried over from the old site. Whitepaper v2.3 notes that allocations are not yet independently verified.
- [ ] **Set absolute social preview URLs.** In `site/index.html`, update `og:image` and `og:url` (marked `DEPLOY STEP`) to the production domain, for example `https://www.cutedodo.com/assets/dodo.jpg`.
- [ ] **Point the domain.** Move `cutedodo.com` DNS to the new host and enable HTTPS.
- [ ] **Check every outbound link** (pump.fun swap, Telegram, X, Discord, DexScreener, Solscan) still points to the official accounts.

## Copy rules

Keep the copy plain and friendly: no em dashes, and none of the stock marketing words (leverage, seamless, empower, unlock, robust, actionable, data-driven, solutions). A quick check:

```bash
grep -nE "—|leverage|seamless|empower|unlock|robust|actionable|data-driven|solutions" site/index.html
```

## Disclaimer

$DODO is a meme token with no intrinsic value or expectation of financial return. Nothing on this site is financial advice.
