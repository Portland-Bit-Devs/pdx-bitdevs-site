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

## LN Dev News

## Bitcoin General News

## Tech News
