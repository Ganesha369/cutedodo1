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
    vet-partner.jpg                  Dr. Pradeep emergency care poster (Vet care section)
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

The "What's happening right now" feed shows the last 8 trades from the PumpSwap pool via the public GeckoTerminal API (about 30 calls per minute per client, no key). It starts when the section comes into view and refreshes every 30 seconds while the tab is visible:

```
GET https://api.geckoterminal.com/api/v2/networks/solana/pools/5cZdup3LcQ9oQMt3mKfo2pQ5CNTMQUT3c2c4dLKN1AML/trades
```

The "Why Solana" network figures are static, copied from solana.com in November 2026. Solana's public RPC blocks browser requests, so making them live needs a small server-side proxy. Until then, refresh the four numbers every few months.

The YouTube video only loads (from youtube-nocookie.com) when a visitor presses play.

## Before going live on the public domain

- [ ] **Confirm the charity figure.** The page says "1% for pet welfare" in headlines (from the whitepaper) and shows the charity wallet at 1.15% of supply (from the old cutedodo.com). The team needs to settle on one wording.
- [ ] **Confirm tokenomics and the wallet list.** The supply split and the 12 public wallets were carried over from the old site. Whitepaper v2.3 notes that allocations are not yet independently verified.
- [ ] **Set absolute social preview URLs.** In `site/index.html`, update `og:image` and `og:url` (marked `DEPLOY STEP`) to the production domain, for example `https://www.cutedodo.com/assets/dodo.jpg`.
- [ ] **Point the domain.** Move `cutedodo.com` DNS to the new host and enable HTTPS.
- [ ] **Confirm the vet emergency number.** The Vet care section and FAQ list Dr. Pradeep's number, +91 88254 37238, as a tap-to-call link. Make sure he has agreed to it being public.
- [ ] **Check every outbound link** (pump.fun swap, Telegram, X, Discord, DexScreener, Solscan) still points to the official accounts.

## Copy rules

Keep the copy plain and friendly: no em dashes, and none of the stock marketing words (leverage, seamless, empower, unlock, robust, actionable, data-driven, solutions). A quick check:

```bash
grep -nE "—|leverage|seamless|empower|unlock|robust|actionable|data-driven|solutions" site/index.html
```

## Disclaimer

$DODO is a meme token with no intrinsic value or expectation of financial return. Nothing on this site is financial advice.
