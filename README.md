<div align="center">

# Nacre — a mining pool for Pearl (PRL)

**0% pool fee.** Nacre is a mining pool for **Pearl (PRL)**, a GPU
proof-of-useful-work blockchain. No registration, no email: your wallet address is your account.

[**🌐 nacrepool.com**](https://nacrepool.com) · PPLNS `:5566` · Solo `:5567` · **0% fee**

`0% fee` &nbsp;·&nbsp; `PPLNS + Solo` &nbsp;·&nbsp; `No signup` &nbsp;·&nbsp; `Non-custodial payouts` &nbsp;·&nbsp; `NVIDIA / CUDA`

</div>

---

## What is Nacre?

Nacre is an independent mining pool for **Pearl (PRL)**. You run the Pearl GPU miner on your
own NVIDIA hardware, point it at Nacre, and the pool combines everyone's work to find blocks and
shares the rewards. Nacre charges a **0% pool fee** — you keep everything you mine, less only the
tiny on-chain network fee when your payout is sent.

- **🌐 Dashboard:** <https://nacrepool.com>
- **⛏️ Stratum — PPLNS:** `stratum+tcp://stratum.nacrepool.com:5566`
- **🎯 Stratum — Solo:** `stratum+tcp://stratum.nacrepool.com:5567`

## Why Nacre

| | |
|---|---|
| **0% pool fee** | You keep 100% of your rewards. No hidden cuts. |
| **PPLNS *and* Solo** | Choose steady, smoothed payouts (PPLNS) or winner-takes-the-block (Solo). |
| **No signup, no email** | Your `prl1p…` wallet address *is* your account. Start in seconds. |
| **Non-custodial payouts** | Rewards are paid straight to your address. Nacre never asks for your keys or seed. |
| **Own infrastructure** | Nacre runs its own Pearl full node and validates every share with the real proof-of-work verifier. |
| **Transparent** | Live pool stats, your own dashboard, and CSV export of your payouts. |

## Quick start — mine in 3 steps

1. **Get the miner.** Pearl mines on **NVIDIA** GPUs using the CUDA miner **`alpha-miner`**
   (see the [Mining Guide](docs/MINING-GUIDE.md)). Make sure your NVIDIA driver + CUDA are installed.
2. **Get a Pearl address.** Any Pearl (`prl1p…`) wallet address. That address is your account — no registration.
3. **Point `alpha-miner` at Nacre:**

```bash
# PPLNS (recommended — steady rewards)
alpha-miner --pool stratum+tcp://stratum.nacrepool.com:5566 \
            --address YOUR_prl1_ADDRESS --worker rig1 --password x --devices 0

# Solo (you keep the full block you find)
alpha-miner --pool stratum+tcp://stratum.nacrepool.com:5567 \
            --address YOUR_prl1_ADDRESS --worker rig1 --password x --devices 0
```

Then open <https://nacrepool.com>, paste your address into **“Check your miner,”** and bookmark your
private dashboard.

## Pool at a glance

| Setting | Value |
|---|---|
| **Fee** | **0%** |
| **Modes** | PPLNS (port `5566`) · Solo (port `5567`) |
| **PPLNS scheme** | Time-weighted, ~65-minute exponential half-life (recent work counts most) |
| **Minimum payout** | 1 PRL |
| **Payout cadence** | Automatic, roughly every 2 hours once you're over the minimum |
| **Chain** | Pearl (PRL) mainnet |
| **Algorithm** | GPU proof-of-useful-work (CUDA / NVIDIA) |
| **Miner** | `alpha-miner` |
| **Account model** | Your `prl1p…` address — no signup |

## PPLNS vs Solo

- **PPLNS (recommended).** Every block the pool finds is split across all miners by their recent
  contribution. Income is **steady and predictable** — you get paid a little and often, and luck
  is smoothed out. Best for most miners.
- **Solo.** You keep the **entire block reward** you find (0% fee). Income is
  **swingy** — you may mine a while with nothing, then hit a full block. Best for larger rigs
  comfortable with variance.

You can switch anytime by pointing your miner at port `5566` (PPLNS) or `5567` (Solo).

## Payouts

- Rewards accrue to your address as you submit valid shares.
- Once your balance passes the **1 PRL** minimum, Nacre pays you automatically (about every 2 hours).
- Payouts go **directly to your mining address** on-chain. Nacre is non-custodial beyond briefly
  batching pending rewards — it never holds your keys.
- You can export your full payout history as CSV from your dashboard.

## Checking your miner

Your address is your account and your dashboard link. Open <https://nacrepool.com>, paste your
`prl1p…` address, and you'll see your live hashrate, workers, unpaid balance, progress to next
payout, and payout history. Bookmark the page to come back to it.

## Security & trust

- **Non-custodial:** you mine to your own wallet address; Nacre never asks for private keys or seeds.
- **Real verification:** every submitted share is checked against Pearl's actual proof-of-work
  verifier — no fake shares are credited.
- **Your node, your rules:** Pearl is open. You're free to run your own node and verify the chain.

## Status

Nacre launched in **2026** and is live on Pearl mainnet. This is a new, independent pool — the
public stats start from launch. Feedback and issues are welcome via
[GitHub Issues](https://github.com/DarioVlahovic/Nacre-mining-pool/issues).

## Documentation

- 📘 [Mining Guide](docs/MINING-GUIDE.md) — full setup, multiple GPUs, running as a service, troubleshooting
- ❓ [FAQ](docs/FAQ.md)
- 📜 [Terms of Service & Disclaimer](TERMS.md)

## Links

- Website / dashboard: <https://nacrepool.com>
- Pearl (PRL) — the chain Nacre mines

---

<div align="center">

**Mine Pearl.** · [nacrepool.com](https://nacrepool.com)

Licensed under [MIT](LICENSE). Mining involves risk — see the [disclaimer](TERMS.md).

</div>
