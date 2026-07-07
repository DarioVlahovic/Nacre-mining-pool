# Nacre Mining Guide

Everything you need to start mining **Pearl (PRL)** on Nacre. It takes about 5 minutes.

> **TL;DR:** install an NVIDIA driver + CUDA, get `alpha-miner`, get a `prl1p…` address, then run
> `alpha-miner --pool stratum+tcp://stratum.nacrepool.com:5566 --address YOUR_prl1_ADDRESS --worker rig1 --password x --devices 0`

---

## 1. Requirements

- A supported GPU:
  - **NVIDIA** (recommended) — RTX 30 / 40 / 50 series, V100, or datacenter Ampere/Ada/Hopper/Blackwell cards.
  - **AMD** — supported via a separate `alpha-miner-amd` build (currently **beta**; see the miner's releases).
- A recent **NVIDIA driver + CUDA runtime** installed and working (`nvidia-smi` should list your GPU).
- A **Pearl wallet address** (`prl1p…`). This is where your rewards are paid, and it doubles as
  your pool account — there is no separate signup.

## 2. Get the miner (`alpha-miner`)

Nacre uses the standard Pearl CUDA miner, **`alpha-miner`** (by AlphaMine-Tech). Grab the latest
**stable** build for your system — one click:

- 🪟 **Windows:** **[Download AlphaMiner-Pearl-Windows.zip](https://github.com/AlphaMine-Tech/alpha-miner/releases/latest/download/AlphaMiner-Pearl-Windows.zip)** — unzip it, then run the miner inside.
- 🐧 **Linux:** **[Download the `alpha-miner` binary](https://github.com/AlphaMine-Tech/alpha-miner/releases/latest/download/alpha-miner)** — then `chmod +x alpha-miner` to make it runnable.
- 📦 **All builds / older cards / AMD:** [alpha-miner releases](https://github.com/AlphaMine-Tech/alpha-miner/releases/latest)

Put it on your PATH (or just note its full path so you can call it).

> ℹ️ alpha-miner is a third-party tool (NVIDIA/CUDA) that works with any Pearl pool. **Use the latest
> release: v1.7.7+ has a 0% dev fee, but v1.7.6 and older took a 1% dev fee.** Nacre
> does not modify, rehost, or bundle it — you download it straight from its maker.

> 💡 **Trouble?** If the newest build gives unusually low hashrate or GPU errors, grab an earlier
> **stable** release from the [releases page](https://github.com/AlphaMine-Tech/alpha-miner/releases)
> (skip any marked *pre-release*).

Verify it runs:

```bash
alpha-miner --help
```

## 3. Choose a mode and connect

**PPLNS — steady rewards (recommended):**

```bash
alpha-miner \
  --pool stratum+tcp://stratum.nacrepool.com:5566 \
  --address YOUR_prl1_ADDRESS \
  --worker rig1 \
  --password x \
  --devices 0
```

**Solo — you keep the full block you find:**

```bash
alpha-miner \
  --pool stratum+tcp://stratum.nacrepool.com:5567 \
  --address YOUR_prl1_ADDRESS \
  --worker rig1 \
  --password x \
  --devices 0
```

- `--address` — your `prl1p…` payout address (this is your account).
- `--worker` — any label for this rig (e.g. `rig1`, `basement-3090`). Shows up on your dashboard.
- `--password` — just `x` (unused; the pool authenticates by address, not password).
- `--devices` — which GPUs to use. Multiple GPUs: `--devices 0,1,2`.

## 4. Verify you're mining

1. The miner should print accepted shares within a minute or two.
2. Open **<https://nacrepool.com>**, paste your `prl1p…` address into **“Check your miner”**, and
   you'll see your live hashrate, workers, and unpaid balance building up.
3. **Bookmark** that page — it's your private dashboard (no login needed; the address is the key).

## 5. Run it 24/7 (Linux systemd example)

Create `/etc/systemd/system/pearl-miner.service` (replace the address):

```ini
[Unit]
Description=Pearl miner @ Nacre
After=network-online.target

[Service]
ExecStartPre=/usr/bin/nvidia-smi -pm 1
ExecStart=/usr/local/bin/alpha-miner \
  --pool stratum+tcp://stratum.nacrepool.com:5566 \
  --address YOUR_prl1_ADDRESS --worker rig1 --password x --devices 0
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now pearl-miner
journalctl -u pearl-miner -f     # watch shares
```

## 6. Keep your GPU healthy

- **Cap power** so the card runs cool and stable, e.g. `nvidia-smi -pl 300` (pick a wattage sensible
  for your GPU). Keep temps under ~83 °C.
- Don't overclock while first testing — confirm stability at stock clocks.
- Good airflow matters more than a few extra MH.

## 7. Payouts

- Rewards accrue as you submit valid shares.
- Once you pass the **1 PRL** minimum, Nacre pays you automatically (about every 2 hours),
  directly to your address.
- Export your full payout history as CSV from your dashboard.

## Troubleshooting

| Symptom | Fix |
|---|---|
| `nvidia-smi` not found / no GPU | Install the NVIDIA driver + CUDA; reboot. |
| Miner connects but 0 shares | Confirm the GPU is supported and not busy with another workload. |
| “invalid address” / rejected login | Your `--address` must be a valid `prl1p…` Pearl address. |
| Can't reach the pool | Check outbound TCP to `stratum.nacrepool.com` on `5566`/`5567` isn't blocked by a firewall. |
| Shares rejected | Usually stale work on an unstable overclock — lower OC, ensure a stable connection. |

Still stuck? Open an [issue](https://github.com/DarioVlahovic/Nacre-mining-pool/issues).
