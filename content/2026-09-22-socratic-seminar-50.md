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

- [Bitcoin Core #36176: Avoid a crash when creating a wallet with `-nosettings`](https://github.com/bitcoin/bitcoin/pull/36176)
  - Reported and fixed by Rob1Ham after hitting it on Bitcoin-Qt 31.1 (Apple silicon)
  - Settings write threw an uncaught exception when dynamic settings were disabled
- [Bitcoin Core #36048: Keep wallet names literal in notification commands](https://github.com/bitcoin/bitcoin/pull/36048)
  - On non-Windows builds, `-walletnotify` substitutes `%w` with the shell-escaped wallet name
  - `std::regex_replace()` treated `$'` in a wallet name as a special pattern, breaking the escaping
  - An authenticated RPC user able to create wallets could inject shell commands run as the node's account
  - Not reachable over P2P or without RPC auth
- [Liquid Reserves Drained for 4,000 BTC](https://x.com/mononautical/status/2096799973098799192)
  - Inflation bug in confidential transaction validation caching
  - L-BTC now backed by only ~4.7% real BTC
  - [Elements #1593: Fix RPC return errors for PSBT and invalid rangeproofs](https://github.com/ElementsProject/elements/commit/4ddaefc8ccfdd9db3053b633092c28285da081e4)
    - Rangeproof and PSBT failures now return errors instead of hitting asserts
    - PAK enforcement on confidential pegout assets
    - Pubkey validity check in `tweakfedpegscript`

## LN Dev News

## Bitcoin General News

## Tech News

- [Claude Opus 5.5](https://x.com/claudeai/status/2102435511222890900)
- [GPT-6 Sol](https://x.com/OpenAI/status/2102460975790137662)
- [Navier-Stokes Solved](https://x.com/OpenAI/status/2097375276384567642)
