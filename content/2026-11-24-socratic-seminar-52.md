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

- [CVE-2026-117348: Node Stall via Duplicate Orphan Announcements](https://x.com/BitcoinNewsCom/status/2125204945230090465) ([advisory](https://bitcoincore.org/en/2026/11/20/disclose-orphan-inv-stall/))
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
- [Miniscript Studio](https://github.com/portlandhodl/miniscript-studio) ([live demo](https://portlandhodl.github.io/miniscript-studio/))
  - Block-based designer: wire keys, timelocks, and logic blocks; compiles live to Miniscript, descriptors, and addresses
  - rust-miniscript and LifeHash compiled to WASM; P2WSH or Taproot; runs fully in the browser as one HTML file
  - Custody over time, unlock timeline, and a disaster simulator for lost keys
  - Exports BIP-388 wallet policies and Core `importdescriptors`; imports descriptors back into blocks
  - {{ thumbnail(src="/images/seminar-52/miniscript-studio.jpeg", thumb="/images/seminar-52/miniscript-studio-thumb.jpeg", alt="Miniscript Studio multi-vendor multisig template") }}
- [xproof](https://github.com/portlandhodl/xproof) ([live demo](https://portlandhodl.github.io/xproof/))
  - ZK proof that two keys share a BIP32 xpub without revealing the xpub, chain code, or paths
  - In-browser Noir/UltraHonk prover (~10.7 KB proof, depth 3, ~65 s on 16 threads); optional SP1 → Groth16 server (356 B, depth 16)
  - Signet demo anchors key B with an on-chain spend; verifier checks the proof and the signature
  - {{ thumbnail(src="/images/seminar-52/xproof.jpeg", thumb="/images/seminar-52/xproof-thumb.jpeg", alt="xproof landing page") }}
- [Anti-Exfil Signing Draft BIPs](https://github.com/AvilaLabs/anti-exfil) ([handbook](https://anti-exfil.avilalabs.org/))
  - Stops a signing device from leaking its keys through chosen nonces: the host adds randomness to each nonce and checks the result
  - Covers BIP340 and ECDSA, plus new PSBT fields so wallets and devices can use it without private extensions
  - Ships test vectors, a libsecp256k1 C module, and a Jade `sign_psbt` patch series
  - Draft from Avila Labs: no BIP number, no cryptographer review or outside audit; Python reference isn't constant-time

## LN Dev News

## Bitcoin General News

- [Fake Electrum Proxy Servers Appear](https://x.com/0xB10C/status/2125269595854414009) ([bnoc.xyz thread](https://bnoc.xyz/t/electrum-proxy-servers-spun-up-in-mid-november-2026/215))
  - 37+ domains, mostly registered Nov 15-19 with self-signed certs, gossiped as Electrum servers; they proxy real servers like Emzy's and Seth's Fulcrum
  - Lookalike names (e.g. `block-stream.info`); suspected goal is address clustering by becoming a wallet's main server
  - Worse: 11+ servers returned altered transactions on broadcast, swapping the recipient for an address with matching last characters
  - Electrum 4.3.4-4.7.2 clients seen connected; [GHSA-6jp4-8v48-cc5v](https://github.com/spesmilo/electrum/security/advisories/GHSA-6jp4-8v48-cc5v) (server replaces a just-broadcast tx) fixed in 4.8.3
  - Upgrade Electrum, pin trusted servers, or run your own
- [Ledn Launches Insured U.S. Custody in All 50 States](https://x.com/FINTECHTVglobal/status/2125289595881365558)
  - Co-founder Mauricio Di Bartolomeo on FINTECH.TV: custody model pitched against exchange risk
  - "Nearly all of our assets are held in cold storage at all times."
  - Discussion: insured custodial vs self-custody

## Tech News

- [Alpöge's Proof of the Riemann Hypothesis](https://en.wikipedia.org/wiki/Alp%C3%B6ge%27s_proof_of_the_Riemann_hypothesis)
  - Levent Alpöge (Anthropic) released a Lean proof of RH and GRH for Dirichlet L-functions on 2026-11-20, built with an unreleased Claude model
  - Approach carries Weil-conjecture techniques (Stepanov's method) over to the integers, using theta correspondence and Arakelov theory
  - [Lean FRO / Mathlib](https://leanprover-community.github.io/blog/posts/riemann-hypothesis/): "full confidence" the proof is correct; ~17M lines of Lean, checked independently by Sutherland and Rubinstein
  - No natural-language proof published yet; [Tao](https://terrytao.wordpress.com/2026/11/20/unforced-euler-singularity-unforced-navier-stokes-singularity-and-the-generalized-riemann-hypothesis/) says it appears to use the full power of modern Langlands work and arithmetic geometry
  - Discussion: a machine-checked proof that mathematicians don't yet understand
- [VP ≠ VNP Over Every Field](https://www.alphaxiv.org/abs/2611.vp-vnp-arithmetic-lower-bounds) ([Lean](https://github.com/anthropics/formal-math))
  - Submitted 2026-11-23, authored by "Claude": found by an internal Claude research model and formalized in Lean
  - Claims arithmetic circuits for the m × m permanent need more than m^(c(log m)^(1/3)) gates, so VP ≠ VNP: the algebraic analogue of P vs NP
  - Superpolynomial, not exponential; doesn't settle P vs NP or apply to Boolean circuits
  - No human has checked it, and nothing verifies the Lean statements match the intended claims
- [Praxis: Practical Witness Encryption for NP](https://eprint.iacr.org/2026/2971)
  - Tse, Vanjani, and Vesely (Byzantine Research / Babylon): encrypt to any NP statement so only someone holding a valid witness can decrypt
  - Encrypts to a Groth16 verifier on BN254; secure under Module-SIS in the generic group and random oracle models, with Lean 4 proofs
  - At 100-bit security: 7.88 GiB ciphertext and ~2^33 operations to decrypt, over ten orders of magnitude smaller than prior constructions
