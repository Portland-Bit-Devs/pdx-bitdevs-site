+++
title = "The Fungibility Misunderstanding That's Quietly Hurting Bitcoin"
template = "blog.html"
date = "2026-04-28"
[extra]
author = "Jon Austen"
+++

There's a long-running debate in Bitcoin circles about coin "taint" --- the idea that because the ledger is public, coins carry a history that can get them blacklisted by exchanges. It generates a lot of noise. It deserves much less attention than it gets. The friction it describes affects less than 2% of network activity, and the remaining 98% of Bitcoin moves through the system the way fungible money should: counted, not appraised.

The conversation worth having isn't about the 2% edge case. It's about a much more consequential misunderstanding of fungibility --- one that's quietly driving proposals to change Bitcoin's protocol rules in ways that would actually reduce fungibility and, with it, the network's ability to scale. The people pushing these changes mean well. They think they're making Bitcoin more flexible, more capable, more useful. What they're actually doing is eroding the property that makes the whole system work.

## What Fungibility Actually Is

Most people, when they hear "fungibility," think about something narrow: can this specific coin be rejected because of where it's been? That's a question about external recognition --- whether a third party will treat your unit as equivalent to any other unit.

But fungibility in the deeper sense is a property of the protocol itself, not of how outsiders react to its outputs. A monetary unit is fungible when the rules governing it treat every unit identically. Every satoshi follows the same consensus rules. Every transaction is validated against the same script logic. Every block is subject to the same difficulty adjustment, the same size limits, the same ordering constraints. There are no special units, no privileged transactions, no exceptions.

This protocol-level uniformity is what allows fungibility at the user level. You can count satoshis instead of appraising them precisely because every node in the network is running the same rules and arriving at the same conclusions about which units are valid. The moment the rules start treating different units differently, you're no longer counting --- you're appraising. And appraisal doesn't scale.

## Why People Want to Loosen the Rules

Bitcoin's protocol rules are restrictive by design. Block size is capped. Script functionality is limited. Validation is expensive. Many transaction types that would be technically possible are forbidden or made costly. To a developer or product person looking at this, it can feel like a system constrained by arbitrary limits --- limits that, if relaxed, would unlock new use cases.

So you get proposals: bigger blocks for more throughput, richer scripting for more functionality, special transaction types for specific applications, accommodations for inscriptions or ordinals or covenants or whatever the current enthusiasm is. Each proposal sounds reasonable in isolation. Each promises to make Bitcoin do more.

The framing is almost always the same: the rules are too tight, let's loosen them. The implicit theory is that fungibility is something you can have separately from the protocol --- that you can change how Bitcoin works without changing what Bitcoin is.

This is the misunderstanding. Fungibility isn't separate from the protocol. It is the protocol's uniformity, expressed through every node's identical validation. When you loosen the rules, you don't just add capability. You add variation in how units are treated. And variation is the opposite of fungibility.

## How Loosening Rules Reduces Fungibility

Consider what happens when you make blocks bigger. Larger blocks are harder to validate, harder to propagate, and harder to store. Fewer participants can run full nodes. The participants who can are increasingly large, well-resourced, and concentrated. Now the rules haven't formally changed --- every satoshi is still nominally equivalent --- but in practice, the set of entities that enforces the rules has shrunk. And when enforcement is concentrated, the enforcers can start treating different units differently. Maybe not today. But the structural option exists.

Consider what happens when you add complex scripting. Now transactions vary in their computational cost. Some transactions are cheap to validate; others are expensive. Fee markets adjust, but more importantly, validation behavior diverges. Some nodes may refuse to relay certain transaction types. Some may apply different policies to different scripts. The protocol no longer treats every transaction identically because transactions are no longer identical in what they ask the network to do.

Consider what happens when you accommodate special-purpose transactions --- inscriptions, named tokens, application-specific encodings. Now the network is carrying multiple categories of payload, and those categories have different economic profiles, different stakeholders, and different political constituencies. Pressure builds to treat them differently. To prioritize one category. To deprioritize another. To filter, censor, or specially process particular kinds of activity. Even if the protocol rules formally remain neutral, the social layer around the protocol starts negotiating exceptions. And exceptions are the wedge that breaks fungibility.

In every one of these cases, the proposed change sounds like an enhancement. More throughput. More functionality. More use cases. But the cost is paid in the property that made Bitcoin work in the first place: the radical uniformity of treatment that lets you count units instead of evaluating them.

## Why This Matters for Scaling

Here's the part that gets missed: fungibility is what allows scaling, not the other way around.

When every unit is treated identically by every participant, you can pool, net, intermediate, and route transactions without anyone having to evaluate the specific units involved. Layer 2 networks like Lightning work because Lightning channels can assume that one satoshi entering a channel is exchangeable with any satoshi exiting. Mining pools work because rewards can be split among participants without anyone caring which specific satoshis they're getting. Exchanges, custodians, and payment processors all depend on being able to commingle funds with confidence that any unit can substitute for any other.

If you erode protocol-level fungibility --- by adding variation, exceptions, or differentiated treatment --- you erode every one of these scaling mechanisms. Lightning gets harder when channels have to track which kinds of satoshis they're holding. Pooling gets harder when commingled funds carry distinguishable characteristics. Intermediation gets harder when intermediaries have to maintain category-aware accounting.

The scaling story for Bitcoin is fundamentally a story about leveraging fungibility. The more uniformly the base layer treats units, the more aggressively higher layers can abstract, batch, and route. Loosen the base layer, and you lose the substrate that scaling depends on.

This is why protocol conservatism in Bitcoin isn't backwardness or stubbornness --- it's an active defense of the property that makes the whole stack possible. Every "improvement" proposal that adds variation to base-layer treatment of transactions is, whether its proponents realize it or not, a proposal to lower the ceiling on how far Bitcoin can scale.

## The Proposals to Watch

The pattern shows up in almost every protocol debate. Whenever someone proposes that Bitcoin should accommodate a new use case by changing how the base layer treats certain kinds of activity, the question to ask isn't *would this be useful?* --- it's *does this introduce variation in how units are treated?* If the answer is yes, the proposal is asking you to trade fungibility for features. And that trade is almost never worth it, because fungibility is what makes the features possible in the first place.

Bigger blocks trade decentralization (and therefore enforcement uniformity) for throughput. Richer scripting trades validation uniformity for functionality. Special-purpose accommodations trade neutral treatment for application support. Each trade looks attractive on its own. Cumulatively, they would turn Bitcoin into a system that has to be appraised rather than counted --- and a system that has to be appraised is not a system that scales.

## What People Misunderstand

The deepest version of the misunderstanding is the assumption that fungibility is a consequence of the protocol --- something that emerges when the rules happen to be written a certain way, and that can be preserved separately if the rules are changed. It can't. Fungibility is the rules. It's the property of having one set of rules, applied identically, to every unit, by every participant.

When you change the rules to accommodate new uses, you're not preserving fungibility while adding capability. You're trading away fungibility as the cost of the new capability. Sometimes that trade is worth making --- soft forks that genuinely preserve uniformity while adding capability are possible and have been done well. But most proposals to "improve" Bitcoin by loosening its constraints don't preserve uniformity. They introduce variation, and variation is what fungibility is the absence of.

The 2% taint debate is a sideshow. The real fungibility conversation is about the protocol itself --- and about whether the well-meaning people who want to make Bitcoin do more understand that what they're really proposing is to make Bitcoin scale less.
