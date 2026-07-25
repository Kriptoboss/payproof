# Payproof — Invoices & Verifiable Receipts

**Our app is built on Arc.**

Payproof turns any wallet address into an invoicing tool. Create a stablecoin invoice, share it as a link or QR code, receive USDC or EURC, and hand your client a receipt that anyone can verify independently onchain.

## Why it's different

- **Serverless by design.** The entire invoice travels inside the shareable link (base64url-encoded in the URL fragment). No database, no accounts, no backend to shut down — host the single HTML file anywhere and it runs forever.
- **Onchain payment references.** Every invoice is fingerprinted with a unique micro-amount signature in the final decimals (e.g. `25.000347`) — the onchain equivalent of a bank payment reference. Payproof scans ERC-20 `Transfer` logs on Arc and matches the payment to the invoice automatically. No oracle, no webhook, no trust.
- **Verifiable receipts.** Each receipt maps to a transaction hash on Arc. Clients, accountants, or disputes can verify it on any Arc explorer — Payproof even has a standalone "Verify a payment" mode that rebuilds a receipt from any tx hash.
- **One-asset UX, unique to Arc.** Gas on Arc Network is paid in USDC, so a payer needs exactly one token — no second coin for fees. Fees are dollar-denominated and predictable (~$0.01).
- **Self-custodial.** Payproof never holds, routes, or controls funds. Payments go wallet-to-wallet.

## Network details used

| Parameter | Value |
| --- | --- |
| Network | Arc Testnet |
| Chain ID | 5042002 (`0x4cef52`) |
| RPC | `https://rpc.testnet.arc.network` (+ Blockdaemon / dRPC / QuickNode fallbacks) |
| Explorer | https://testnet.arcscan.app |
| Faucet | https://faucet.circle.com |
| USDC (ERC-20, 6 decimals) | `0x3600000000000000000000000000000000000000` |
| EURC (ERC-20, 6 decimals) | `0x89B50855Aa3bE2F677cD6303Cec089B5F319D72a` |

## Run it

It's a single `index.html`. Options:

**Locally** — just double-click `index.html` (an internet connection is needed for the ethers.js CDN and Arc RPC).

**GitHub Pages (free, permanent)**
1. Create a public repo (e.g. `payproof`), upload `index.html`.
2. Settings → Pages → Deploy from branch → `main` / root.
3. Your app is live at `https://<user>.github.io/payproof/`.

**Vercel / Netlify** — drag-and-drop the folder; done in under a minute.

## Using it

1. **New invoice** — enter your receiving address, amount (max 3 decimals; the last 3 decimals are reserved for the reference), currency, description. Generate → share the link/QR.
2. **Payer** opens the link → one click adds Arc Testnet to MetaMask, connects, and pays the exact amount. Settlement lands in seconds.
3. **My invoices** — hit **Check**: Payproof scans Arc transfer logs and flips the invoice to **Paid** when it finds the exact match, then produces a printable PDF receipt.
4. **Verify a payment** — paste any Arc tx hash to reconstruct an independent receipt.

## Testing end-to-end (testnet)

1. Get testnet USDC from the [Circle Faucet](https://faucet.circle.com) (select Arc Testnet).
2. Create an invoice to one of your addresses; open the link in another browser/profile with MetaMask.
3. Pay → watch the invoice flip to Paid → print the receipt.

## Compliance & attribution

Payproof is an independent application **built on Arc Network** ("Arc"). It is not affiliated with, endorsed by, or operated by Circle. Arc is a trademark of Circle Internet Group, Inc. and/or its affiliates. Payproof currently runs on Arc Testnet; testnet tokens have no real-world value.
