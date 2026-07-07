# Nacre FAQ

### What does it cost? What's the fee?
**0%.** Nacre takes no pool fee — you keep 100% of your mining rewards (less only the tiny on-chain
network fee when a payout transaction is sent).

> ⚠️ One fee Nacre does **not** control: the miner software's own dev fee. The current
> **alpha-miner (v1.7.7 and newer) is 0% dev fee**, so the all-in cost really is zero — but
> **v1.7.6 and older had a 1% dev fee** built in. If your rig has been running a while, update
> to the latest release and that 1% comes back to you.

### Do I need to sign up?
No. Your Pearl (`prl1p…`) wallet address **is** your account. Just point your miner at Nacre with
your address. No email, no password, no KYC.

### What can I mine with?
**NVIDIA GPUs** only — Pearl's miner (`alpha-miner`) is CUDA-based. See the
[Mining Guide](MINING-GUIDE.md).

### PPLNS or Solo — which should I pick?
- **PPLNS** (port `5566`) — steady, smoothed income split by recent contribution. Best for most.
- **Solo** (port `5567`) — you keep the whole block you find, but income is swingy. Best for big rigs.

### When and how do I get paid?
Automatically, roughly every **2 hours**, once your balance is over **1 PRL**. Payouts go straight
to your mining address on-chain.

### Is Nacre custodial? Do you hold my coins?
Nacre is **non-custodial** in the way that matters: you mine to **your own** address and we pay you
there. We only briefly track your pending rewards until the next payout. **We never ask for your
private keys or seed phrase — and never will. No legitimate pool ever does.**

### How do I see my stats?
Open <https://nacrepool.com> and paste your address into "Check your miner." Bookmark the page —
it's your private dashboard (the address is the key, so keep the link to yourself if you prefer).

### Can I use multiple GPUs / multiple rigs?
Yes. Use `--devices 0,1,2` for multiple GPUs on one machine, and a different `--worker` name per
rig. They all pay to the same address and show up separately on your dashboard.

### My hashrate on the dashboard looks different from my miner.
The dashboard shows **pool-effective** hashrate measured from accepted shares, which naturally
differs from your miner's instantaneous local reading. Over time they converge.

### Is this the same as AlphaPool / other pools?
No — Nacre is an independent pool (**0% pool fee**), not affiliated with AlphaPool. See the
[Mining Guide](MINING-GUIDE.md) to get connected.

### I found a bug / have a suggestion.
Open a [GitHub issue](https://github.com/DarioVlahovic/Nacre-mining-pool/issues).
