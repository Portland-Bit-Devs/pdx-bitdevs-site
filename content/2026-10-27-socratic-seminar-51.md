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

- [Bitcoin Core v32.0 and v32.1 Tagged](https://github.com/bitcoin/bitcoin/releases/tag/v32.1)
  - [Release notes](https://github.com/bitcoin/bitcoin/blob/v32.1/doc/release-notes.md)
  - v32.0 tagged 2026-10-21 but never announced due to last-minute issues; v32.1 tagged 2026-10-26
  - [v32.0...v32.1](https://github.com/bitcoin/bitcoin/compare/v32.0...v32.1)
    - `-maxconnections` capped at 2,000 to reduce crash risk at very high peer counts (#35919)
    - Disconnect peers that don't drain the send buffer below 1MB within 20 minutes (#36667)
    - Block file positions widened to 64 bits, with 64-bit seek syscalls on Windows (#36669)
    - Socket exception monitoring aligned between `poll()` and `select()` (#36665)
  - 29.x is now End of Life; 3 medium/high severity vulns fixed in 30.0 to be disclosed in two weeks
  - P2P and network
    - Default `-maxconnections` raised from 125 to 200; new `-inboundrelaypercent` (default 50) caps tx-relay inbound slots
    - Private broadcast fix: v2 to v1 fallback could bypass Tor and leak the sender's IP (#35410)
    - Outgoing tx relay rate-limit moved to a global backlog, plus a 12MB per 10 minutes bandwidth limit
    - Auto-created onion services enable Tor PoW defenses
    - I2P ElGamal sessions removed on or before v34; dropping CJDNS support under discussion
  - Fees and mempool
    - `estimatesmartfee` combines block policy with a new mempool-based estimator and returns the lower of the two
    - Mempool RPCs add `vsize_adjusted` (sigop-adjusted) and `vsize_bip141`; `vsize` deprecated
  - Performance and storage
    - Parallel prevout prefetch during block validation, `-prevoutfetchthreads` (default 8)
    - `-txindex` rebuilt from scratch takes less than half the disk space
    - Libevent replaced with a custom, stricter HTTP server for RPC/REST
  - Wallet and RPC
    - PSBT RPCs default to PSBT v2
    - New `exportwatchonlywallet`, `derivehdkey`, and `addhdkey` RPCs
    - New `getopenrpcinfo` / `rpc.discover` return an OpenRPC description of the API
    - `-walletnotify` shell injection via wallet names fixed (#36048)
    - `taproot` removed from `getdeploymentinfo`; BIP 9 bits 5-28 ignored per BIP 323
- [rbitcoin: Bitcoin Full Node in Rust](https://github.com/reardencode/rbitcoin)
  - First-party code is AI-written (Grok / xAI) with Brandon Black (reardencode) prompting
  - Pure-Rust consensus and script validation, no `libbitcoinconsensus`
  - No UTXO set: relational archive with in-process txindex, Electrum, and optional Esplora REST
  - Pitched as a drop-in Core + electrs backend for mempool-style stacks; not a Core replacement
  - Default mainnet skips script checks below block 840000 (`--milestone 0` for full validation)
  - Claims under ~30h IBD on a laptop-class host; ~730 GiB on disk with cold files
  - Discussion: alternative consensus implementations, AI-written consensus code, and trusting milestones
- [Bitcoin Core #36669: Store Positions as a 64-bit Integer in Flatfiles](https://github.com/bitcoin/bitcoin/pull/36669)
  - Antoine Poinsot (darosior); merged 2026-10-26 and backported to v32.1
  - `FlatFilePos::nPos`, `CBlockIndex::nDataPos` / `nUndoPos`, and block file sizes widened from 32 to 64 bits
  - Last 32-bit field in flat file handling that was only bounded indirectly by callers
  - No on-disk format change: positions are already serialized as varints
  - New `FileSeek64` / `FileTell64` wrappers use `_fseeki64` / `_ftelli64` on Windows, where `long` is 32 bits even on 64-bit builds
  - Part of an ongoing effort to remove unneeded 32-bit and platform-specific integer types (#24214, #33724, #34109, #35097, #35616)

## LN Dev News

## Bitcoin General News

- [Keystone Website Breach Exposes Customer Data](https://x.com/KeystoneWallet/status/2114719318722404578)
  - Unauthorized access to the Keystone website on 2026-10-20; confirmed with Shopify via API activity review on 2026-10-23
  - Names, contact info, shipping addresses, and order details (items, prices) exposed
  - Payment info, seed phrases, private keys, and wallet passwords not affected
  - Expect phishing: fake refunds, replacement devices, or shipping "help" from impersonators
  - [Keystone to Destroy 18,835 Hardware Wallets After Verification Key Theft](https://thehackernews.com/2026/10/keystone-to-destroy-18835-hardware.html) ([post](https://x.com/TheHackersNews/status/2115047606816768469))
    - Attacker escalated privileges via a third-party data monitoring tool on the website and took the device verification key
    - Key only proves a device is genuine; counterfeits could pass the authenticity check
    - Key is written at manufacture and can't be rotated, so 18,835 unsold old-key devices will be destroyed
    - 25,964 buyer records (2024-2026) plus 12,873 unpaid checkouts affected
    - Devices delivered before 2026-10-20 that pass the check are fine; old-key devices received after should be verified with support
- [Ledger Devices with Spy Implants Sold via CryptoBilis](https://x.com/MagicalTux/status/2108556423445835827)
  - [Ledger Support: Investigating fund losses in South East Asia](https://x.com/Ledger_Support/status/2108551100613714002)
    - Users who bought from Malaysian reseller CryptoBilis reported losses; reseller asked to pause sales and shipments
  - [MagicalTux: Pull the SIM out of the spy implant](https://x.com/MagicalTux/status/2108095743525625998)
    - Posted the day before Ledger's statement; jokes that the implant's eSIM is good for free data
  - MagicalTux asked affected users to open their devices and send photos of the board and implant
  - Implant reportedly captures the seed phrase and exfiltrates it over LTE via an eSIM
  - Battery swapped for a smaller one to make room for the implant
  - Third-party loss estimates range from ~$93M to ~$103M across 300-500+ addresses; Ledger has not confirmed totals
  - Ledger has not attributed the tampering to CryptoBilis itself

## Tech News

- [NSA Advisory: Critical Patches Recommended for PHP Vulnerabilities](https://www.nsa.gov/press-room/press-releases-statements/press-release-view/article/4630238/nsa-advisory-critical-patches-recommended-for-php-vulnerabilities/)
  - "PHP2Shell": CVE-2026-109618 and CVE-2026-109619, both CVSS v4.0 9.2
  - Bugs are in the PHP engine itself, not WordPress, Drupal, or other frameworks
  - Reportedly present back to PHP 5.4; end-of-life versions won't get a fix
  - Patch now, or take the system offline until it can be mitigated
  - Patching won't undo a prior compromise; hunt for added accounts, tokens, and backdoors
- [Inside Node2Shell: A Closer Look at CVE-2026-111497](https://www.akamai.com/blog/security-research/inside-node2shell-closer-look-cve-2026-111497)
  - Out-of-bounds write in the Brotli decoder bundled with Node.js (`node:zlib`), CVSS 9.2
  - Invalid block switch reported as "need more input" instead of a format error, overflowing an 8-byte buffer
  - Unauthenticated: reachable via `fetch()` responses and Express 5 / body-parser 2 `Content-Encoding: br` bodies by default
  - Fixed in 22.23.4, 24.22.1, and 26.12.1; EOL lines (25.x, 23.x, 20.x and earlier) get no fix
  - No workaround from Node.js; body-parser `inflate: false` rejects compressed bodies as a stopgap
- [Tailworm: Security Assessment of Tailscale and headscale](https://tailworm.com/)
  - Independent report on Tailscale v1.104.2 and headscale v0.29.5; tested 2026-10-22 to 2026-10-24
  - Tailscale SSH unix-socket forwarding runs as root; TOCTOU races let a normal SSH session reach root-only sockets
  - Chained in the lab to root command execution, enrollment-key capture, and a rogue node joining the tailnet
  - Wormable: policy-granted SSH let it spread automatically across permitted devices
  - Also: unvalidated conn25 connector egress, OOM bugs, and `serve` exposing the local API to peers
  - Fixes landed on `main` but not yet in a numbered release; treat every SSH grant as root-equivalent and use per-pair grants
  - [Tailscale SSH investigation and remediation update](https://tailscale.com/ssh-investigation-update)
    - Patched client targeted for end of day 2026-10-27
    - Interim: tighten SSH policies and set `TS_SSH_DISABLE_FORWARDING=1`
- [v86_64: x86-64 PC Emulator in the Browser](https://github.com/portlandhodl/v86_64) ([live demo](https://portlandhodl.github.io/v86_64/))
  - 64-bit (long mode) fork of [v86](https://github.com/copy/v86); boots 64-bit Linux ISOs in a browser tab or Node.js
  - x86-to-WebAssembly JIT for 64-bit code: ~530 MIPS vs ~80 interpreted
  - Debian (Xfce) and Ubuntu 26.04.1 (GNOME) live ISOs boot to the desktop; multi-GB ISOs streamed with HTTP range requests
  - VirtualBox-style machine manager with JSON profiles; guest internet access through a built-in Wisp proxy
  - Limits: one CPU, 4 GiB guest RAM (wasm32), no AVX, no 3D
  - [wasm-bitcoin-tools](https://github.com/portlandhodl/wasm-bitcoin-tools) runs official Bitcoin Core offline in a headless Alpine guest for wallet and AnchorWatch vault recovery checks
  - All contributions must be AI-generated; upstream v86 doesn't accept AI-written code, so changes aren't sent upstream
