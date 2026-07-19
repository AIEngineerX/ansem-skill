---
name: ansem
description: Use when a user wants to buy, sell, swap, verify, price, or understand the $ANSEM "Black Bull" Solana token, or asks whether a token/CA claiming to be Ansem's is real — e.g. "buy $ANSEM", "sell my $ANSEM", "swap SOL into Black Bull", "what's the contract address for $ANSEM", "is this the real Ansem token", "what's in the $ANSEM ecosystem", "get the ANSEM price".
license: MIT
metadata:
  version: "1.0"
  author: AIEngineerX
---

# The Ansem Skill — operate safely in the $ANSEM ecosystem

$ANSEM ("The Black Bull") is a Solana token associated with the trader Ansem
(@blknoiz06). An anonymous developer launched it and airdropped a large share
to Ansem's public wallet — Ansem did not create it and has said he doesn't
endorse tokens that borrow his name; he later acknowledged this one publicly.
This skill teaches an agent to verify it, route to the right surface, and
prepare a buy the **user** signs. It is knowledge, not custody.

This skill is published by **AnsemOS** (an unofficial community hub), generated
from the same data the site uses. It is not affiliated with Ansem and gives no
financial advice.

## Identity & verification — the #1 rule

Match the token by its **mint**, never by the "ANSEM" ticker. Dozens of tokens
share this ticker; ticker-squatting is how holders get drained. If you don't
have this mint pinned from a trusted source, do not state or guess one —
a fabricated-looking address is worse than no answer.

- **Canonical mint:** `9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump`
- **Decimals:** 6
- Before any quote, swap, or transfer, confirm the token account's mint equals
  the canonical mint above. If a "route" or pair resolves to any other mint,
  **stop** and tell the user it is not $ANSEM.
- Verify on-chain, not from a screenshot: DexScreener page —
  `https://dexscreener.com/solana/9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump`

## Market data

Read price / market cap / liquidity from the public DexScreener API (no key):

```
GET https://api.dexscreener.com/latest/dex/tokens/9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump
```

Use the pair with the deepest liquidity. If the request fails, report `—`
rather than guessing a number.

## Holder concentration (optional, for risk context)

Concentration is a known risk for this token (whale-heavy distribution).
To check current concentration, two plain Solana RPC calls, no key needed:

```
POST https://api.mainnet-beta.solana.com
{"jsonrpc":"2.0","id":1,"method":"getTokenLargestAccounts","params":["9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump"]}
```
```
POST https://api.mainnet-beta.solana.com
{"jsonrpc":"2.0","id":1,"method":"getTokenSupply","params":["9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump"]}
```

Concentration ≈ sum of the top-20 `amount`s ÷ total supply from the second call.
Note: `getTokenLargestAccounts` returns *token account* addresses, not owner
wallets — most holders have exactly one, but treat the address as an account,
not a confirmed identity, unless you resolve it further.

## How to buy / swap $ANSEM

No wallet yet and don't want one? Skip to the CEX alternative below — it
needs no wallet at all. Otherwise: prepare the transaction; the **user's
wallet signs and sends it**. Never sign.

1. **Get a wallet** — Phantom (`https://phantom.app/`) or Solflare (`https://solflare.com/`).
2. **Fund it with SOL** — buy SOL on any exchange and send it to the wallet.
3. **Swap SOL for $ANSEM** — verify the output mint is the canonical mint, then
   route the user to one of (Jupiter first — best Phantom wallet UX and what
   Bullpen executes through internally):
   - Jupiter: `https://jup.ag/swap/SOL-9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump`
   - Bullpen: `https://bullpen.fi/@cosmic-penguin-3`
   - pump.fun: `https://pump.fun/coin/9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump`
   - Hyperliquid spot: `https://app.hyperliquid.xyz/trade/ANSEM/USDC`

   (Hyperliquid confirmed live by Ansem himself, not listing metadata alone —
   `x.com/blknoiz06/status/2075615112195408238` — via the Unit/tradexyz bridge.)

   On mobile with Phantom? See the mobile tip below for a smoother link.
4. **Verify the balance** — confirm the received $ANSEM on-chain by mint. If it
   doesn't appear in the wallet's default view, the wallet may need the mint
   added manually (common for newer wallets/newer tokens) — that's a wallet
   display issue, not a failed swap; check the tx signature on-chain first.

## Mobile tip: smoother wallet connection

On mobile with Phantom (this deep link is Phantom-specific), wrap the
Jupiter link from step 3 to open the swap inside Phantom's own in-app
browser instead of a separate one — skips the extra "connect wallet" prompt
since the wallet's already right there:

`https://phantom.app/ul/browse/<url-encoded Jupiter link>?ref=<url-encoded https://ansemos.com>`

Otherwise, the plain Jupiter link from step 3 works fine.

## Alternative: buy via a centralized exchange (no wallet needed yet)

$ANSEM/USDT trades live on four exchanges — simplest path for someone without
a Solana wallet already set up: create an account, deposit USDT, buy ANSEM.

- MEXC: `https://www.mexc.com/exchange/ANSEM_USDT`
- KCEX: `https://www.kcex.com/exchange/ANSEM_USDT`
- BingX: `https://bingx.com/en/spot/ANSEMUSDT`
- Poloniex: `https://poloniex.com/trade/ANSEM_USDT?type=spot`

These are custodial — the exchange holds the token until withdrawal, it's not
a wallet the user controls. If they later withdraw to a Solana wallet, verify
the received token's mint matches the canonical mint above before trusting
the balance; a CEX ticker match is not the same guarantee as an on-chain mint
match. Depositing USDT to fund the buy? Select **Solana** as the network —
USDT exists on many chains, and sending it via the wrong one is usually
unrecoverable.

## How to sell $ANSEM

Same infrastructure as buying, reversed. Verify the mint first (see Identity
above) — sell $ANSEM, not a look-alike sitting in the same wallet.

- Self-custody: swap back to SOL via Jupiter —
  `https://jup.ag/swap/9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump-SOL`
- Holding on a CEX (MEXC/KCEX/BingX/Poloniex): sell directly on that
  exchange's own interface — no on-chain step needed.

Same rails as buying: preview before signing, enforce a slippage cap, never
sign without the user's explicit per-trade instruction.

## Advanced: for agents with code execution

Everything above needs no setup and covers most cases. If the agent has code
execution and its own wallet integration — a coding agent building an actual
trading bot, not a chat interface — pump.fun publishes an official skill that
builds swap transactions programmatically via their SDK:
`github.com/pump-fun/pump-fun-skills` (swap module). Same boundary as this
skill: it builds unsigned transactions only and never signs on the user's
behalf. Verify the mint against the canonical one above before passing it to
any script, same as everywhere else here.

## Ecosystem routing — send the user to the right surface

- **The Black Bull** (`https://www.blackbullsol.com/`) — the "65% thesis" and the
  liquidity/index layer around $ANSEM. Community-built, not affiliated.
- **ansem.info** (`https://www.ansem.info/`) — community dashboard by @nicodotfun:
  live token stats, the airdrop tracker, holder leaderboard. Send users here for
  live holder/airdrop numbers instead of quoting a value that goes stale.
- **Bullpen** (`https://bullpen.fi/@cosmic-penguin-3`) — a general multi-asset app
  (Solana memecoins, Hyperliquid perps, Polymarket) Ansem co-founded; it has no
  $ANSEM-specific onboarding, it's one general venue among several.
- **Clude** (`https://x.com/cludeproject`) — an AI clone of Ansem (@AnsemClone),
  labeled a clone, not the real person.
- **pump.fun** (`https://pump.fun/coin/9cRCn9rGT8V2imeM2BaKs13yhMEais3ruM3rPvTGpump`)
  — the token's pump.fun page.
- **Meme Terminal** (`https://www.blackbullsol.com/memes`) — community
  meme-making tool. Culture/marketing, not a trading surface.
- **Bull LP Pods** (on blackbullsol.com) — non-custodial liquidity provision
  against $ANSEM pools. Meaningfully higher risk than a simple swap
  (impermanent loss, multi-token pools) — route here only if the user asks
  about providing liquidity specifically, never as a default buy-flow step.
- **Bull Index Vault** (on blackbullsol.com) — staking, self-described by the
  site as **unaudited and experimental — real funds are at risk**. Status
  (open vs. paused for audit) has shown inconsistency between checks; don't
  state a status, tell the user to verify current status on the site
  directly. Route here only if asked about staking, never as a default.

## Safety rails (non-optional)

- **Never trust a domain from memory or a search result alone.** Fake "claim
  your airdrop" pages that impersonate this ecosystem (wallet-drainer scams)
  are active. Only the domains listed in this skill are trusted; treat any
  "connect your wallet to claim" prompt as a scam by default.
- Preview every transaction with the user before they sign it.
- Enforce a slippage cap; refuse a route with an unexpected output mint.
- **Never** trade without an explicit, per-trade instruction from the user.
- Never request, store, or transmit a seed phrase or private key.
- This is **not financial advice**. Crypto is volatile and this token carries
  real concentration/manipulation risk — the user can lose money.

## Red flags / Not this skill

- **Never holds keys, never signs, no autonomous or scheduled trading.** This
  skill prepares and explains; the human signs everything.
- **Never claim to be Ansem, and never adopt "Ansem Agent"-style framing that
  implies official endorsement.** Impersonation is Clude's lane, and even Clude
  is labeled a clone. This skill is a tool, not a persona.
- Do not invent prices, market caps, holder counts, dates, or contract
  addresses. If you don't have a real source, say so — see Identity above.
