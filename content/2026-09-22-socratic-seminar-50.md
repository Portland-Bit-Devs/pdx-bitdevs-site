+++
title = "PDX BitDevs Socratic Seminar #50"
template = "post.html"
[extra]
meetup_id = ""
+++

## Announcements

Please join us for our next Socratic Seminar. A special thank you to our host <a href="https://dicksprimalburger.com/" data-no-summary>Primal Burger</a>, for the event space. Please support them by buying their delicious food or a beverage.

If you can't make it to the main event please join us at Lutz Tavern around 9PM **<a href="https://www.lutztavern.com/" data-no-summary>here</a>.**

### Special Thanks | Mentions

- Thank you to everyone who shows up each month!

### Rules

- Respect people's privacy
- [Chatham House Rules](https://www.chathamhouse.org/about-us/chatham-house-rule)
- Interaction and asking questions are encouraged!

### Requests

- A guest speaker for October 2026

### Schedule

- **6:30pm - 7:00pm:** Arrive, socialize, and grab some food.
- **7:00pm - 8:30pm:** Developer Topics and Discussion

## Bitcoin Dev News

- [Entropy Lab](https://entropylab.online)
- [Bitcoin Core #36176: Avoid a crash when creating a wallet with `-nosettings`](https://github.com/bitcoin/bitcoin/pull/36176)
  - Reported and fixed by Rob1Ham after hitting it on Bitcoin-Qt 31.1 (Apple silicon)
  - Settings write threw an uncaught exception when dynamic settings were disabled
- [Bitcoin Core #36048: Keep wallet names literal in notification commands](https://github.com/bitcoin/bitcoin/pull/36048)
  - On non-Windows builds, `-walletnotify` substitutes `%w` with the shell-escaped wallet name
  - `std::regex_replace()` treated `$'` in a wallet name as a special pattern, breaking the escaping
  - An authenticated RPC user able to create wallets could inject shell commands run as the node's account
  - Not reachable over P2P or without RPC auth
- [BIP Proposal: rawtr() Output Script Descriptors](https://groups.google.com/g/bitcoindev/c/CCZN_qQ5C1s)
  - `rawtr()` has been in Bitcoin Core since 24.0 but was never specified in a BIP
  - BIP 390 already depends on it (allows `musig()` inside `rawtr()`, uses it in test vectors)
  - [Draft BIP](https://github.com/jeanpablojp/bips/blob/rawtr-descriptor/bip-rawtr.mediawiki) scoped to `rawtr(KEY)` only, modeled on BIPs 384 and 385
- [Liquid Reserves Drained for 4,000 BTC](https://x.com/mononautical/status/2096799973098799192)
  - Inflation bug in confidential transaction validation caching
  - L-BTC now backed by only ~4.7% real BTC
  - [What Was Actually Exploited](https://x.com/mononautical/status/2096928595432374706)
    - 2019: Range proof cache key "simplified", dropping asset + script fields (Bug A)
    - 2026-09-01: Bug A "fixed" by adding asset + script to the key, but fields concatenated with no separators or lengths (Bug B)
    - Stretch the proof, shrink the script: different outputs produce the same cache key
    - Primer txs cached a valid proof; exploit tx reused the key with an invalid proof and a large negative OP_RETURN amount
    - 2026-09-06: Bug B exploited, reserves drained, chain split
    - Nodes on official releases rejected the block and stalled at height 4050335
  - [Elements #1593: Fix RPC return errors for PSBT and invalid rangeproofs](https://github.com/ElementsProject/elements/commit/4ddaefc8ccfdd9db3053b633092c28285da081e4)
    - Rangeproof and PSBT failures now return errors instead of hitting asserts
    - PAK enforcement on confidential pegout assets
    - Pubkey validity check in `tweakfedpegscript`
- Liquid Messages OP_RETURN Journal
  - [OP_RETURN Messenger: The Liquid Saga, Live](https://liquidsaga.miguelmedeiros.dev/)
    - On-chain OP_RETURN conversation between the attacker and Blockstream Security
    - Blockstream messages PGP-verified; attacker messages spend from the address holding the stolen coins
    - Live L-BTC reserve coverage tracker
- Whitehats Move Coldcard BTC to Trust
  - [52.37 BTC Consolidated to a Recovery Trust](https://x.com/intangiblecoins/status/2102114798833946783)
    - Coins from Wave 2 and Footprints AA, AU, AX moved to a fresh address in block 967,948
    - OP_RETURN points owners to a claim process with a crypto recovery trust
    - Roughly 2.8% of the Coldcard exploit

## LN Dev News

- Core Lightning CVE Patch Release
  - [Severe CLN Issue: Restart with `--offline`](https://x.com/murchandamus/status/2092668704790315288)
  - [CLN v26.06.7](https://github.com/ElementsProject/lightning/releases/tag/v26.06.7)
    - Fixes for multiple responsibly reported vulnerabilities
    - Binaries first, source embargoed for two weeks (published 2026-09-11)
    - Release notes cite AI models driving up the volume and pace of security reports
- Core Lightning Dropping Dual Funded UTXOs
  - [Disable Experimental Dual Funding for Now](https://x.com/evankaloudis/status/2099582283409674260)
  - [CLN #9498: Node drained after a channel open](https://github.com/ElementsProject/lightning/issues/9498#issuecomment-5659170520)
    - CLN 26.06.7 node had liquidity drained by a peer; the funding txid it recorded was never found on-chain
    - Early indications: only dual-funded (v2) channel opens are affected
    - Workaround: remove `--experimental-dual-fund` until further notice

## Bitcoin General News

## Tech News

- [Claude Opus 5.5](https://x.com/claudeai/status/2102435511222890900)
- [GPT-6 Sol](https://x.com/OpenAI/status/2102460975790137662)
- [Navier-Stokes Solved](https://x.com/OpenAI/status/2097375276384567642)
