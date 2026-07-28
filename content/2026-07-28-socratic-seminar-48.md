+++
title = "PDX BitDevs Socratic Seminar #47"
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

- A guest speaker for July 28 2026

### Schedule

- **6:30pm - 7:00pm:** Arrive, socialize, and grab some food.
- **7:00pm - 8:30pm:** Developer Topics and Discussion

## Bitcoin Dev News

- [Bitcoin Mailing List - Remove BIP125 RBF Signaling](https://groups.google.com/g/bitcoindev/c/C7zNIk8llew/m/YAdpwe33AgAJ)
    - Proposal to remove BIP125 RBF signaling from Bitcoin Core wallet
    - Since fullrbf became default in v28.0, explicit signaling is now redundant
    - Plans to share an informational BIP recommending input sequence numbers
- [Testnet 5 Proposal](https://groups.google.com/g/bitcoindev/c/kGUMTxOvdJA/m/Eyx5FxQeAAAJ)
    - BIP draft for new Testnet5 addressing Testnet4 usability issues
    - Also serves as a miner playground for BIP54
- [Quantum Secure BIP324](https://groups.google.com/g/bitcoindev/c/n_5WuKVYqwI/m/lBooLis3AQAJ)
    - Proposal to upgrade BIP324 (P2P encryption) to be post-quantum resistant
    - Current ECDH key exchange is vulnerable to "harvest, decrypt later" attacks
    - Lower hanging fruit than consensus-layer quantum resistance
- [Rust Bitcoin Witness Commitment Check](https://github.com/rust-bitcoin/rust-bitcoin/pull/6250)
    - Fix for divergence between rust-bitcoin and BIP-141
    - Blocks with witness commitment must contain exactly one 32-byte witness reserved value
    - Previous code didn't enforce this for non-SegWit transactions
- [Nix Deterministic Builds](https://x.com/0xB10C/status/2062896873761816854)
    - Bitcoin Core v31.0 can now be built with Nix matching Guix bit-by-bit
    - Includes bitcoind, bitcoin-qt, bitcoin-cli for x86_64 and aarch64
    - Big win for reproducible builds across different toolchains
- [Back to Back Forks](https://x.com/0xB10C/status/2054547919450071266/photo/1)
    - Bitcoin had back-to-back forks at heights 949203 and 949204
    - Rare occurrence but not considered special or concerning

## LN Dev News

## Bitcoin General News

- [ZEC - Exploited for Unlimited Private Coins](https://x.com/zooko/status/2062644925590900980)
    - Orchard Counterfeiting Vulnerability discovered in Zcash
    - Security update published by Shielded Labs
    - 2.9M views on the disclosure announcement
- [Tropic Square Security Vulnerability](https://x.com/tropicsquare/status/2062112682921078914)
    - Ledger Donjon discovered laser fault injection attack on TROPIC01 chip
    - More complex combined attack paths could breach hardware boundary
    - Not a remote exploit, no evidence of real-world exploitation
    - Mitigation measures available for deployment
- [Sparrow Wallet Mobile Yoinked from App Store](https://x.com/craigraw/status/2069124643223445854)
    - Craig Raw's Apple Developer account flagged for termination
    - Placeholder app to warn about fake "Sparrow" apps was flagged as "dishonest"
    - Unless reversed by June 30, all new Sparrow Wallet installs will fail
    - Over a dozen fake Sparrow apps have appeared since 2023, causing user losses
- [Trezor Tropic Square Compromise Announcement](https://trezor.io/blog/news/Trezor-response-TROPIC01-chip-disclosure-no-impact-to-your-funds)
    - Ledger Donjon reported successful laser fault injection on TROPIC01 chip
    - Tropic Square found additional method to extract PIN-related secrets
    - User funds are safe - vulnerability cannot access PIN, funds, or wallet backup
    - No action required from users; disclosure shows commitment to transparency
- [Bridge Drained](https://x.com/p3b7_/status/2069045986236695020?s=46)
    - Taiko L2 bridge drained for ~$1.7M
    - Root cause: private key (enclave-key.pem) committed to public GitHub repo
    - Key was used to sign all of Taiko's SGX enclaves
    - Attacker forged SGX attestations on fake L2 blocks
    - Key management failure, not an SGX exploit
- [BIP110 Warning](https://x.com/PortlandHODL/status/2069530882294399093?s=20)
    - Question about customer guidance for forked Bitcoin implementations
    - Concerns about discarding blocks and not moving chain tip forward
    - Especially relevant for Lightning channel users
- [BIP110 Forking Dynamics](https://x.com/OrangeSurfBTC/status/2069394596597998064)
    - 11-step thread explaining BIP110 forking dynamics
    - BIP110 and Standard miners share same chain until rule disagreement
    - Split could happen at lock-in threshold or mandatory signalling

## Tech News

- [Trump Quantum Dominance](https://x.com/blockspace/status/2069525382659768660)
    - Trump signed 2 executive orders for USA "Quantum Dominance"
    - 2030 & 2031 new deadlines for USA's post-quantum transition
    - Aims to supercharge quantum research
    - White House attempting to get ahead of cybersecurity concerns
