+++
title = "PDX BitDevs Socratic Seminar #51"
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

- A guest speaker for November 2026

### Schedule

- **6:30pm - 7:00pm:** Arrive, socialize, and grab some food.
- **7:00pm - 8:30pm:** Developer Topics and Discussion

## Bitcoin Dev News

- [Bitcoin Core v32.0 and v32.1 Tagged](https://github.com/bitcoin/bitcoin/releases/tag/v32.1) ([release notes](https://github.com/bitcoin/bitcoin/blob/v32.1/doc/release-notes.md))
  - v32.0 tagged 2026-10-21 but never announced due to last-minute issues; v32.1 followed 2026-10-26
  - [v32.1 fixes](https://github.com/bitcoin/bitcoin/compare/v32.0...v32.1): `-maxconnections` capped at 2,000, slow-draining peers disconnected, 64-bit block file positions, `poll()`/`select()` alignment
  - 29.x is EOL; 3 medium/high vulns fixed in 30.0 to be disclosed in two weeks
  - P2P
    - Default `-maxconnections` 125 → 200; new `-inboundrelaypercent` (default 50)
    - Private broadcast fix: v2 → v1 fallback could bypass Tor and leak the sender's IP (#35410)
    - Global tx relay backlog plus a 12MB / 10 min bandwidth limit; Tor PoW defenses on auto-created onions
    - I2P ElGamal sessions removed by v34; dropping CJDNS under discussion
  - Fees and mempool
    - `estimatesmartfee` returns the lower of block-policy and new mempool-based estimates
    - Mempool RPCs add `vsize_adjusted` and `vsize_bip141`; `vsize` deprecated
  - Performance
    - Parallel prevout prefetch (`-prevoutfetchthreads`, default 8)
    - Rebuilt `-txindex` uses less than half the disk space
    - Libevent replaced with a custom HTTP server for RPC/REST
  - Wallet and RPC
    - PSBT v2 by default; new `exportwatchonlywallet`, `derivehdkey`, `addhdkey`, and OpenRPC `getopenrpcinfo`
    - `-walletnotify` shell injection via wallet names fixed (#36048)
    - `taproot` removed from `getdeploymentinfo`; BIP 9 bits 5-28 ignored per BIP 323
- [Bitcoin Core: Easy-to-Find Vulnerabilities Policy](https://x.com/bitschmidty/status/2113341995687034977) ([security policy](https://bitcoincore.org/en/security-advisories))
  - darosior on the mailing list: more reports of easily (re)discovered vulns, as LLMs lower the bar to find bugs and spot covert fixes
  - Long embargoes normally mean fixes wait for the next major release; for easy-to-find bugs that just delays the fix
  - Bugs flagged "easy to discover" (think: found with a simple LLM prompt) get backported to all maintained releases, shipped ASAP, with an advisory
  - [Rob1Ham](https://x.com/Rob1Ham/status/2113436127768326506): pre-announcing patches helps attackers, as when "find bad bug in php" let anyone spend $3 for RCE
(https://github.com/reardencode/rbitcoin)
  - AI-written (Grok) with Brandon Black (reardencode) prompting; pure-Rust consensus, no `libbitcoinconsensus`
  - No UTXO set: relational archive with built-in txindex, Electrum, and optional Esplora; a Core + electrs backend, not a Core replacement
  - Skips script checks below block 840000 by default (`--milestone 0` for full validation)
  - Claims ~30h IBD on a laptop; ~730 GiB on disk
  - Discussion: alternative consensus implementations, AI-written consensus code, trusting milestones
- [Bitcoin Core #36669: Store Positions as a 64-bit Integer in Flatfiles](https://github.com/bitcoin/bitcoin/pull/36669)
  - darosior; merged 2026-10-26 and backported to v32.1
  - Block file positions and sizes widened from 32 to 64 bits; no on-disk change since positions are varints
  - 64-bit seek/tell wrappers for Windows, where `long` is 32 bits even on 64-bit builds
  - Part of an ongoing cleanup of unneeded 32-bit integer types
- [Bitcoin Core #34075: Mempool-Based Fee Estimation](https://github.com/bitcoin/bitcoin/pull/34075)
  - ismaelsadeeq; merged 2026-08-21, ships in v32 `estimatesmartfee`
  - Uses the mempool's top block only to *lower* the block-policy estimate, so miners can't game it upward
  - 75th percentile feerate for economical, 50th for conservative; ~29% less overestimation historically
  - Bet: underestimating is safer now that RBF/CPFP bumping is reliable; overpaying can't be undone
  - [Motivating case](https://x.com/PortlandHODL/status/2064765940970246304): v31 on Signet with near-empty blocks quoted 1,684 sat/vB for 6 blocks, then 0.1 sat/vB at 7
- [wasm-bitcoin-tools: Bitcoin Core Offline in the Browser](https://github.com/portlandhodl/wasm-bitcoin-tools) ([live](https://portlandhodl.github.io/wasm-bitcoin-tools/))
  - Official Bitcoin Core 31.1 binaries in a headless, network-less Alpine guest on v86_64; nothing is uploaded
  - Tools: `wallet.dat` checker, AnchorWatch vault recovery check, and multi-signer PSBT finalizer
  - Each tool also ships as a single ~117 MB HTML file for air-gapped use
  - Author's warning: audit the offline file and never use real bitcoins
- [SeedSigner Fork Adds LifeHash Fingerprints](https://x.com/w_s_bitcoin/status/2108924628752314423) ([fork PR](https://github.com/w-s-bitcoin/seedsigner/pull/1))
  - Wallet fingerprints shown as [LifeHash](https://github.com/BlockchainCommons/bc-lifehash) images alongside hex; a visual aid, no stronger than the 32-bit fingerprint
  - Also edit or remove a loaded BIP-39 passphrase without re-entering the mnemonic, plus BIP-85 child management
  - Implements upstream [#419](https://github.com/SeedSigner/seedsigner/issues/419), but no merge expected given Keith Mukai's passphrase UX concerns
- [Delving: Descriptor Syntax for Hash Preimages](https://delvingbitcoin.org/t/descriptor-syntax-for-hash-preimages/2935)
  - jaonoctus proposes a private form like `sha256(preimage(HEX))`, the way `pk()` can hold a WIF/xprv; possibly a BIP 379 extension
  - Today Core's wallet can't take a preimage at all; it has to be inserted into PSBT fields with an external tool
  - Preimages must be exactly 32 bytes; an explicit marker is needed since a 32-byte preimage and digest look the same
  - fametrano: in a ranged descriptor every output shares the digest, so the first hash-path spend reveals the preimage for all; per-index derived preimages could fix that
  - Discussion: should Core also get an RPC to add preimages to a PSBT?
- [btc-lean: Machine-Checked Lean 4 Model of Bitcoin Consensus](https://github.com/Rob1Ham/btc-lean)
  - Rob1Ham's executable Lean 4 model of consensus rules, with a separate proofs package
  - 726-row rule census, each row tied to a Bitcoin Core reference and BIP/CVE: 676 proven, 50 obsolete
  - Replays serialized historical mainnet blocks offline; separate 140-row wallet census (descriptors, Miniscript, PSBT) is only partly proven
  - Not a node and not externally audited; "proven" means a Lean statement checks, not byte-for-byte equivalence with Core
  - Discussion: what formal verification can and can't tell us about consensus

## LN Dev News

## Bitcoin General News

- [Keystone Website Breach Exposes Customer Data](https://x.com/KeystoneWallet/status/2114719318722404578)
  - Website breached 2026-10-20: names, contact info, addresses, and orders exposed; no seeds, keys, or payment info
  - Expect phishing: fake refunds, replacements, or shipping "help"
  - [Keystone to Destroy 18,835 Hardware Wallets After Verification Key Theft](https://thehackernews.com/2026/10/keystone-to-destroy-18835-hardware.html)
    - Attacker pivoted through a third-party monitoring tool and stole the device verification key
    - Counterfeits could pass the authenticity check; the key can't be rotated, so unsold old-key devices are destroyed
    - Devices delivered before 2026-10-20 that pass the check are fine; verify later old-key devices with support
- [Foundation: Spam Emails Sent from Official Domains](https://x.com/FoundationHQ/status/2114564656199069844)
  - Traced to one or more compromised Cloudflare API keys; all keys revoked and the malicious domain taken down
  - Passport hardware not compromised and funds safe; full report to follow
- [Ledger Devices with Spy Implants Sold via CryptoBilis](https://x.com/MagicalTux/status/2108556423445835827)
  - [Ledger](https://x.com/Ledger_Support/status/2108551100613714002) investigating losses from devices bought via Malaysian reseller CryptoBilis; sales paused
  - Implant reportedly captures the seed and exfiltrates it over LTE via an eSIM, with a smaller battery to make room
  - Third-party loss estimates ~$93M-$103M across 300-500+ addresses; unconfirmed by Ledger
  - Ledger has not blamed CryptoBilis itself
- [Datavault AI Can't Withdraw Its Bitcoin Treasury from Biconomy](https://x.com/lopp/status/2115200402169708612)
  - Treasury company $DVLT disclosed 4 months of failed BTC withdrawals from Biconomy, which holds all its funds; stock crashed
  - Discussion: not your keys, not your coins

## Tech News

- [NSA Advisory: Critical PHP Vulnerabilities](https://www.nsa.gov/press-room/press-releases-statements/press-release-view/article/4630238/nsa-advisory-critical-patches-recommended-for-php-vulnerabilities/)
  - "PHP2Shell": CVE-2026-109618 and CVE-2026-109619, CVSS 9.2, in the PHP engine itself
  - Reportedly back to PHP 5.4; EOL versions get no fix
  - Patch or take offline, then hunt for prior compromise
- [Node2Shell: CVE-2026-111497](https://www.akamai.com/blog/security-research/inside-node2shell-closer-look-cve-2026-111497)
  - Unauthenticated out-of-bounds write in Node.js's bundled Brotli decoder, CVSS 9.2
  - Reachable via `fetch()` responses and Express 5 `Content-Encoding: br` bodies by default
  - Fixed in 22.23.4, 24.22.1, 26.12.1; EOL lines unpatched
- [Tailworm: Security Assessment of Tailscale and headscale](https://tailworm.com/)
  - TOCTOU races in Tailscale SSH socket forwarding (runs as root) chained to root RCE and a rogue node joining the tailnet
  - Wormable across devices with policy-granted SSH
  - Fixes on `main`, not yet released; treat SSH grants as root-equivalent
  - [Tailscale update](https://tailscale.com/ssh-investigation-update): patch due 2026-10-27; meanwhile set `TS_SSH_DISABLE_FORWARDING=1`
- [CVE Submissions Going Vertical](https://x.com/callebtc/status/2113212220712604116)
  - calle: "I'm tired boss"
  - CVE Tracker chart: ~2-4k per period through 2024-25, then a near-vertical climb to ~15k, projected ~17k
  - Discussion: AI-driven bug finding, and whether maintainers can keep up with the flood of reports
  - {{ thumbnail(src="/images/seminar-51/cve-tracker.jpeg", thumb="/images/seminar-51/cve-tracker-thumb.jpeg", alt="CVE Tracker chart showing CVE counts spiking in 2026") }}
- [DeepSeek V4.1 Flash 1017 for Cyber Beats Kimi K3](https://x.com/Rob1Ham/status/2111828895448068106)
  - Rob1Ham: "the new kimi k3"; rescan your code with it, it finds things everything else missed, and it's cheap
  - DeepSWE v1.1: 77% pass@1 at ~$0.20/task, ahead of Kimi K3 (~69% at ~$4.50) and frontier closed models
  - [Artificial Analysis](https://x.com/ArtificialAnlys/status/2113682654709313811): #1 open model on its Cyber Index at 57% (up from 41%), with no safety refusals
  - [Inference.net](https://x.com/inference_net/status/2114813188034433124) serves a `-cyber` variant at cost; KYC required
  - Discussion: cheap open models as bug hunters, for defenders and attackers alike
  - {{ thumbnail(src="/images/seminar-51/deepseek-flash-1017.jpeg", thumb="/images/seminar-51/deepseek-flash-1017-thumb.jpeg", alt="DeepSWE v1.1 pass@1 vs cost per task chart") }}
- [Claude "REA" (Reverse Engineer Anything) Requests Reportedly Blocked](https://x.com/AbhinavXJ/status/2113590263373508704)
  - r/claude users report a safety check stops reverse-engineering playbooks mid-write-up, and Claude won't retry even reworded
  - Poster claims Claude is told to underperform on these tasks (unverified); argues for local models
  - Discussion: AI guardrails on security research, hosted vs local models
- [Steering Qwen to Be Evil](https://x.com/beeforbacon1/status/2114120076840292604)
  - [Rob1Ham](https://x.com/Rob1Ham/status/2114089804346364364): "We doing brain surgery on the clankers boys"; steering a local Qwen model's internals toward "evil"
  - Asked to define a friend, the steered model loops: I need to be a "friend" and to "kill" each other
  - Discussion: activation steering on open-weight models, and what it means for local-model safety
  - {{ thumbnail(src="/images/seminar-51/qwen-steering.png", thumb="/images/seminar-51/qwen-steering-thumb.png", alt="Steered Qwen output looping on friend and kill") }}
- [v86_64: x86-64 PC Emulator in the Browser](https://github.com/portlandhodl/v86_64) ([live demo](https://portlandhodl.github.io/v86_64/))
  - 64-bit fork of [v86](https://github.com/copy/v86); boots Debian and Ubuntu desktops in a browser tab
  - x86-to-wasm JIT: ~530 MIPS vs ~80 interpreted
  - Limits: one CPU, 4 GiB RAM, no AVX or 3D
  - AI-only contributions, so changes can't go upstream to v86
- LifeHash: Sparrow vs Entropy Lab
  - 14 fingerprints where the two render differently; Entropy Lab matches the [Blockchain Commons C++ reference](https://github.com/BlockchainCommons/bc-lifehash) on 13, Sparrow on 1
  - Each differs by 4-36 of 1,024 pixels
  - {{ thumbnail(src="/images/seminar-51/lifehash-sparrow-vs-entropylab.jpeg", thumb="/images/seminar-51/lifehash-sparrow-vs-entropylab-thumb.jpeg", alt="Sparrow vs Entropy Lab LifeHash reference matches") }}
