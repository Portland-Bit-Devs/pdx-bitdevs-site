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
