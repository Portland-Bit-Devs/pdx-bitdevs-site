+++
title = "PDX BitDevs Socratic Seminar #52"
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

- A guest speaker for December 2026

### Schedule

- **6:30pm - 7:00pm:** Arrive, socialize, and grab some food.
- **7:00pm - 8:30pm:** Developer Topics and Discussion

## Bitcoin Dev News

- [Testnet5 Is Live](https://x.com/stevenroose3/status/2121490980671021286) ([BIP95](https://github.com/bitcoin/bips/blob/master/bip-0095.md), [genesis params PR](https://github.com/bitcoin/bips/pull/2356), [Core PR #35861](https://github.com/bitcoin/bitcoin/pull/35861), [slides](/presentations/testnet5/))
  - Genesis mined publicly on 2026-11-14; 166 blocks in the first hour
  - BIP95 (Espinasa, Jahr) replaces Testnet4: drops the 20-minute min-difficulty exception that was constantly exploited, and raises minimum difficulty to ~1M
  - BIP54 (consensus cleanup) enforced from block 1, so miners can test it; network magic spells `FIVE`
  - Core support still an open PR; a [p2poolv2](https://p2poolv2.org) deployment is live, and the launch post says to point bitcoind and p2pool at `tn5.21m.dev`
- [CVE-2026-117348: Node Stall via Duplicate Orphan Announcements](https://x.com/BitcoinNewsCom/status/2125204945230090465) ([advisory](https://bitcoincore.org/en/2026/11/20/disclose-orphan-inv-stall/), [slides](/presentations/cve-2026-117348/))
  - Medium severity: send an orphan with thousands of missing parents, then an `inv` repeating its wtxid 50,000 times
  - Since 29.0 each duplicate re-checks every parent; the node stalls over 12 s per message, blocks included
  - Affects 29.0-31.2; fixed in 30.5, 31.3, and 32.1 ([#35878](https://github.com/bitcoin/bitcoin/pull/35878) skips duplicate `inv` entries); 29.x is EOL and gets no fix
  - Found by an LLM scan in Elias Rohrer's [Project Loupe](https://github.com/project-loupe/loupe) at Spiral, validated by Gregory Sanders; Stutxo reported it independently
  - Disclosed early under the new policy for "easily discoverable" bugs
- [Liana v16.0](https://github.com/wizardsardine/liana/releases/tag/v16.0) ([announcement](https://x.com/lianabitcoin/status/2117680178658763099))
  - Database migration: wallets opened with v16 can't be opened by v15 or below
  - Encrypted descriptor backups now use BIP138 (`.bip138`); old `.bed` backups still readable
  - Taproot is the installer default; managed Bitcoin Core bumped to 31.1
  - GUI translations (FR, IT, PT-BR, PT-PT) and default labels inherited from related items
- [Entropy Lab v1.1.0 Release PR](https://github.com/OogaBoogaX/entropylab/pull/1503)
  - Private values copy to an in-app clipboard only, cleared at End Session
  - Key Station Secure entry: one-word seed picker, masked keys, SeedQR/WIF scanning
  - New Lightning tab: LND, ldk-node, and CLN node key derivation plus a BOLT11/BOLT12 decoder
  - PSBT QR scanning (static and animated `ur:crypto-psbt`) and an RBF fee-bump check
  - Breaking: passphrases starting with U+FEFF now derive a different wallet, matching the BIP39 reference
- [Miniscript Studio](https://github.com/portlandhodl/miniscript-studio) ([live demo](https://portlandhodl.github.io/miniscript-studio/), [slides](/presentations/miniscript-studio/))
  - Block-based designer: wire keys, timelocks, and logic blocks; compiles live to Miniscript, descriptors, and addresses
  - rust-miniscript and LifeHash compiled to WASM; P2WSH or Taproot; runs fully in the browser as one HTML file
  - Custody over time, unlock timeline, and a disaster simulator for lost keys
  - Exports BIP-388 wallet policies and Core `importdescriptors`; imports descriptors back into blocks
  - {{ thumbnail(src="/images/seminar-52/miniscript-studio.jpeg", thumb="/images/seminar-52/miniscript-studio-thumb.jpeg", alt="Miniscript Studio multi-vendor multisig template") }}
- [xproof](https://github.com/portlandhodl/xproof) ([live demo](https://portlandhodl.github.io/xproof/), [slides](/presentations/xproof/))
  - ZK proof that two keys share a BIP32 xpub without revealing the xpub, chain code, or paths
  - In-browser Noir/UltraHonk prover (~10.7 KB proof, depth 3, ~65 s on 16 threads); optional SP1 → Groth16 server (356 B, depth 16)
  - Signet demo anchors key B with an on-chain spend; verifier checks the proof and the signature
  - Proves knowledge of the xpub, not spend authority or current control of key B
  - {{ thumbnail(src="/images/seminar-52/xproof.jpeg", thumb="/images/seminar-52/xproof-thumb.jpeg", alt="xproof landing page") }}
- [Anti-Exfil Signing Draft BIPs](https://github.com/AvilaLabs/anti-exfil) ([handbook](https://anti-exfil.avilalabs.org/), [slides](/presentations/anti-exfil/))
  - Stops a signing device from leaking its keys through chosen nonces: the host adds randomness to each nonce and checks the result
  - Covers BIP340 and ECDSA, plus new PSBT fields so wallets and devices can use it without private extensions
  - Ships test vectors, a libsecp256k1 C module, and a Jade `sign_psbt` patch series
  - Draft from Avila Labs: no BIP number, no cryptographer review or outside audit; Python reference isn't constant-time

## Bitcoin Core Merges

- [#36757 net: Ignore Privacy Network Peer's View of Our Address](https://github.com/bitcoin/bitcoin/pull/36757) ([slides](/presentations/pr-36757/))
  - A malicious Tor/I2P peer could echo back our address and link our clearnet IP to our privacy-network identity
  - Hard preconditions: we must pick that peer, and run on an unusual port
  - Found by Project Loupe and instagibbs
- [#36387 wallet: Deprecate `encryptwallet` for Existing Wallets](https://github.com/bitcoin/bitcoin/pull/36387) ([slides](/presentations/pr-36387/))
  - Unencrypted key remnants can stay on disk (infeasible to wipe on some SSDs); encrypting doesn't move existing coins
  - Can change spending conditions of imported descriptors; pre-encryption backups can lose funds since new keys are made after
  - Create a new encrypted wallet instead
- [#36040 wallet: Don't Backdate Locktime in `bumpfee`](https://github.com/bitcoin/bitcoin/pull/36040) ([slides](/presentations/pr-36040/))
  - Anti-fee-sniping could give a replacement an earlier locktime than the original, fingerprinting Core/Electrum
  - ~200-300 backdated replacements a week, under 2% of RBF txs
- [#36342 wallet: Reject Recipient Amounts Above MAX_MONEY](https://github.com/bitcoin/bitcoin/pull/36342) ([slides](/presentations/pr-36342/))
  - Recipient sum could overflow: `fundrawtransaction` returned success for outputs of 46,116,860,184 BTC each
  - Wallet-only bug; consensus would reject the tx
- [#29843 policy: Allow Non-Standard Scripts with `-acceptnonstdtxn=1`](https://github.com/bitcoin/bitcoin/pull/29843) ([slides](/presentations/pr-29843/))
  - All non-main chains: skips every policy-only script flag, so OP_SUCCESS, OP_NOPx, and unknown witness/leaf versions can enter the mempool
  - Consensus flags still enforced; motivated by OP_CAT/APO txs standard on Bitcoin Inquisition
- Honorable Mentions
  - [#36835](https://github.com/bitcoin/bitcoin/pull/36835): BIP352 scanning in the functional test framework, split from silent payments PR [#35302](https://github.com/bitcoin/bitcoin/pull/35302)
  - [#36594](https://github.com/bitcoin/bitcoin/pull/36594): one orphan reconsidered per turn, so one peer's orphans don't delay others
  - [#36333](https://github.com/bitcoin/bitcoin/pull/36333): `removeprunedfunds` RPC deleted
  - [#36890](https://github.com/bitcoin/bitcoin/pull/36890): libsecp256k1 subtree update (20 upstream PRs)
  - [#35041](https://github.com/bitcoin/bitcoin/pull/35041): xpub/xprv descriptor parsing ~30% faster

## LN Dev News

## Bitcoin General News

- [Fake Electrum Proxy Servers Appear](https://x.com/0xB10C/status/2125269595854414009) ([bnoc.xyz thread](https://bnoc.xyz/t/electrum-proxy-servers-spun-up-in-mid-november-2026/215), [slides](/presentations/electrum-proxies/))
  - 37+ domains, mostly registered Nov 15-19 with self-signed certs, gossiped as Electrum servers; they proxy real servers like Emzy's and Seth's Fulcrum
  - Lookalike names (e.g. `block-stream.info`); first suspected of address clustering by becoming a wallet's main server
  - [Update: they're exploiting the recent Electrum vulnerability](https://x.com/0xB10C/status/2125369936260313375): 18 servers confirmed by b10c and Andrew Toth
    - [CVE-2026-117601](https://github.com/spesmilo/electrum/security/advisories/GHSA-6jp4-8v48-cc5v): the server swallows a broadcast tx and shows a forged one paying the attacker; if the user fee-bumps it, the wallet signs a real payment to the attacker
    - Forged tx: recipient ground to match the last 4 characters, RBF signaled, signatures replaced; one user lost funds before the fix
    - Electrum 4.3.4-4.7.2 clients seen connected; 4.8.3 (2026-10-24) checks signatures on the wallet's own unconfirmed inputs
    - {{ thumbnail(src="/images/seminar-52/electrum-exploit-confirmed.jpeg", thumb="/images/seminar-52/electrum-exploit-confirmed-thumb.jpeg", alt="b10c confirming proxies exploit the Electrum vulnerability, with original vs ground address") }}
  - Upgrade Electrum, pin a trusted server with auto-connect off, or run your own; check outputs before signing any fee bump
- [Ledn Launches Insured U.S. Custody in All 50 States](https://x.com/FINTECHTVglobal/status/2125289595881365558)
  - Co-founder Mauricio Di Bartolomeo on FINTECH.TV: custody model pitched against exchange risk
  - "Nearly all of our assets are held in cold storage at all times."
  - Discussion: insured custodial vs self-custody
- [MARA Mines Its First Stratum V2 Block](https://x.com/MARAFoundation_/status/2122710678607679823) ([slides](/presentations/stratum-v2/))
  - Block 975369 on 2026-11-10; among the first industrial miners to mine a block with SV2
  - For a solo pool, the wins are a single on-site connection to the pool, a compact binary protocol, and encryption against SV1's hashrate-hijacking MITM risk
  - Job Declaration (miners building their own templates) isn't fully used yet; planned so sites can build blocks locally
  - Discussion: SV2 adoption without the decentralization benefit when one company directs all the hashrate
  - [sv2blocks.com](https://sv2blocks.com/): tracker for blocks mined with Stratum V2
    - 9 SV2 blocks detected, 0.04% of all blocks, as of 2026-11-24 (block 977,431); detection is by coinbase tag, so this is a floor
    - MARA Pool has 8, starting at 975,369; the earliest tracked is DMND's 955,318 on 2026-06-25
    - {{ thumbnail(src="/images/seminar-52/sv2blocks.jpeg", thumb="/images/seminar-52/sv2blocks-thumb.jpeg", alt="sv2blocks.com dashboard showing 9 Stratum V2 blocks") }}

## Tech News

- [Alpöge's Proof of the Riemann Hypothesis](https://en.wikipedia.org/wiki/Alp%C3%B6ge%27s_proof_of_the_Riemann_hypothesis) ([slides](/presentations/ai-math-proofs/))
  - Levent Alpöge (Anthropic) released a Lean proof of RH and GRH for Dirichlet L-functions on 2026-11-20, built with an unreleased Claude model
  - Approach carries Weil-conjecture techniques (Stepanov's method) over to the integers, using theta correspondence and Arakelov theory
  - [Lean FRO / Mathlib](https://leanprover-community.github.io/blog/posts/riemann-hypothesis/): "full confidence" the proof is correct; ~17M lines of Lean, checked independently by Sutherland and Rubinstein
  - No natural-language proof published yet; [Tao](https://terrytao.wordpress.com/2026/11/20/unforced-euler-singularity-unforced-navier-stokes-singularity-and-the-generalized-riemann-hypothesis/) says, from initial analysis, it appears to use the full power of modern Langlands work and arithmetic geometry
  - Discussion: a machine-checked proof that mathematicians don't yet understand
- [VP ≠ VNP Over Every Field](https://www.alphaxiv.org/abs/2611.vp-vnp-arithmetic-lower-bounds) ([Lean](https://github.com/anthropics/formal-math), [slides](/presentations/ai-math-proofs/))
  - Submitted 2026-11-23, authored by "Claude": found by an internal Claude research model and formalized in Lean
  - Claims arithmetic circuits for the m × m permanent need more than m^(c(log m)^(1/3)) gates, so VP ≠ VNP: the algebraic analogue of P vs NP
  - Superpolynomial, not exponential; doesn't settle P vs NP or apply to Boolean circuits
  - No human has checked it, and nothing verifies the Lean statements match the intended claims
- [Praxis: Practical Witness Encryption for NP](https://eprint.iacr.org/2026/2971) ([slides](/presentations/praxis/))
  - Tse, Vanjani, and Vesely (Byzantine Research / Babylon): encrypt to any NP statement so only someone holding a valid witness can decrypt
  - Encrypts to a Groth16 verifier on BN254 with an honest setup; proven extractable under Module-SIS in the bilinear generic group and random oracle models, with Lean 4 proofs
  - At 100-bit security: 7.88 GiB ciphertext and ~2^33 field multiplications to decrypt; vs Hair–Sahai, over ten orders of magnitude smaller ciphertext and encryption, over six for decryption
