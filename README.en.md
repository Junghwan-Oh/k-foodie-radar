# foodie-radar

`foodie-radar` is a Markdown-based restaurant radar for maintaining high-quality restaurant lists and suggesting visit candidates based on your personal taste.

It goes beyond generic “find me a restaurant nearby” search. It tracks trusted food creators, official guides, recommendation signals, sponsorship risk, menu-level reasons, and your evolving taste profile.

## Problem

Restaurant discovery is noisy.

Map ratings, blog posts, and viral reviews often mix real information with ads and marketing. Following trusted food YouTubers manually also takes time. You may watch a long video only to find that the restaurant is not your style, or that there are too many candidates to turn into an actual visit list.

Shorts and Reels make this worse. Some creators hide the restaurant name in the description or hashtags while using vague clickbait titles.

`foodie-radar` treats restaurant discovery as a personal assistant problem:

- Keep a high-quality restaurant list updated.
- Separate trusted food creators from expert backup layers.
- Prioritize recommendations that match your taste.
- Label or downgrade sponsored/marketing-heavy content.
- Explain why a restaurant is worth visiting and what to order.
- Let you ask for lists by cuisine, price, region, creator, or dining style.

## Core Layers

1. Official guide layer
   - Michelin starred/selected restaurants
   - Bib Gourmand
   - Blue Ribbon

2. Top 30 food creator and influencer layer
   - The current starter pool is a Top 30 list of food creators/influencers based on public YouTube subscriber counts and channel fit.
   - It is not an absolute trust ranking. It is a carefully curated starting point.
   - Creators can be promoted, downgraded, held, or removed based on taste fit, sponsorship risk, and usefulness.

3. Chef and expert backup layer
   - Top domestic chefs and expert channels are kept separately from the main food creator ranking.
   - Use this layer when asking for fine dining, omakase, culinary technique, Chinese cuisine, Japanese cuisine, Italian cuisine, meat, seafood, or premium dining explanations.

4. Restaurant ledger layer
   - Normalizes restaurant names, branches, aliases, locations, categories, menus, prices, and source links.
   - Branches are not automatically merged when the actual dining experience may differ.

5. Personal taste layer
   - Stores the signals you personally value.
   - Examples: best in category, national No. 1, craft-level quality, extreme value with real quality, personal favorites, repeat-visit restaurants.

6. Visit queue
   - Separates immediate candidates, holds, stale entries, and restaurants that need operational verification.

## Why Manage Food Creators Separately?

Finding good food creators is hard.

Subscriber count alone does not mean a creator matches your taste. Some channels focus on alcohol, convenience stores, franchises, viral hot places, or ad-heavy content. Those may not be useful if your goal is a high-quality personal restaurant list.

`foodie-radar` organizes creators into:

- First-tier creators to track immediately.
- Secondary creators for cross-checking.
- Hold candidates that need trust or taste validation.
- Removed creators that do not fit the user's taste or purpose.
- Chef/expert backup channels for fine dining and culinary context.

The creator list is not fixed. It should be edited for each user.

## Example Requests

```text
Summarize Jaesullang Guide's restaurant recommendations from the last three months by price tier.
```

```text
Using my first-tier creators, give me the Top 10 Korean restaurants in Seoul under 50,000 KRW.
```

```text
For seafood and raw fish, separate the evidence from trusted seafood creators and recommend only the strongest candidates.
```

```text
Recommend the best restaurants in Daejeon using official guides, creator mentions, and my personal taste profile.
```

```text
For fine dining, use the chef/expert backup layer and explain why the menu is expensive dish by dish.
```

```text
I care about craft quality, best-in-category restaurants, and extreme value with real quality. Re-rank the list with that taste profile.
```

## Standard Recommendation Format

```markdown
Last checked: YYYY-MM-DD
Scope/condition:
Note: Always re-check hours, holidays, reservations, and operating status before visiting.

## Top N by Budget/Condition

| Rank | Restaurant | Three-Line Recommendation | Menu-Level Reasons | Price | Location | Source/Notes |
|---:|---|---|---|---|---|---|
| 1 | Restaurant name | 1) Strong recommendation signal. <br>2) Why it fits the user's taste. <br>3) When or why to visit. | `Menu A`: Why it is the representative order. <br>`Menu B`: What it helps verify. |  |  |  |
```

Rules:

- Every restaurant needs at least three practical recommendation lines.
- “Good”, “famous”, or “good value” is not enough.
- Include all meaningful recommendation reasons mentioned in the source video when possible.
- Every major menu item needs a menu-level reason.
- Course meals and omakase require major course items and dish-level features when available.
- Separate creator evidence from AI-added analysis.

## Sample: Jaesullang Guide Three-Month Price-Tier List

Jaesullang Guide is used here as a sample creator because it is one of the personally trusted food YouTube channels in this workflow. This is only one possible usage pattern. Users can replace the creator, region, cuisine, price range, or ranking logic based on their own taste.

Example request:

```text
Summarize Jaesullang Guide's restaurant recommendations from the last three months by price tier.
Create Top 10 lists for all prices, under 100,000 KRW, under 50,000 KRW, and under 30,000 KRW.
For each restaurant, include a three-line recommendation, menu-level reasons, price range, location, and sources.
```

The sample table below was generated from a prompt like this:

```text
Rebuild Jaesullang Guide's restaurant list from the last three months.

Conditions:
1. Top 10 regardless of price
2. Top 10 under 100,000 KRW
3. Top 10 under 50,000 KRW
4. Top 10 under 30,000 KRW

Each table must include:
- Rank
- Restaurant
- Three-line recommendation
- Menu-level reasons
- Price range
- Location
- Source/notes

Rules:
- Do not only write titles. Write at least three practical recommendation lines per restaurant.
- Avoid shallow phrases like "good", "famous", or "good value" without explanation.
- Include all recommendation reasons mentioned in the video when possible.
- Explain why each major menu item is worth ordering.
- For course meals or omakase, include major course items and dish-level features.
- Separate Jaesullang Guide evidence from AI-added analysis.
- For Shorts, do not rely on the title alone. Check descriptions, hashtags, prices, and locations.
```

Instead of returning a plain list of titles, `foodie-radar` organizes the result by:

- Monthly ranking placement, repeat mentions, and strong title signals.
- Restaurant names, prices, locations, and menus extracted from descriptions and hashtags.
- At least three practical recommendation lines per restaurant.
- Menu-level reasons for the main order candidates.
- Course or omakase details, with uncertain entries held or downgraded when course details are missing.

Detailed Markdown versions are available here:

- [Jaesullang Guide recent three-month price-tier restaurant list](restaurant-intelligence/jaesullang-3mo-top10-2026-05-18.md)
- [Jobxicman recent three-month price-tier restaurant list](restaurant-intelligence/jobxicman-3mo-top10-2026-05-18.md)

The image below is a sample price-tier table for Jaesullang Guide's recent three-month recommendations.

![Jaesullang Guide price-tier recommendation sample](assets/jaesullang-price-table-sample.svg)

## YouTube Shorts Handling

Some food creators, especially Shorts-heavy channels, often omit restaurant names from titles.

For example, a title like “Is this expensive gomtang worth it?” may only reveal the actual restaurant name in the description or hashtags.

For Shorts, always inspect:

- Title
- Description
- Hashtags
- Upload date
- Auto captions or visible text when available
- Restaurant aliases and branch names

## Repository Structure

```text
.
├─ README.md
├─ README.en.md
├─ assets/
│  └─ jaesullang-price-table-sample.svg
├─ skills/
│  └─ restaurant-trust-intelligence/
│     └─ SKILL.md
└─ restaurant-intelligence/
   ├─ official-guides.md
   ├─ creator-registry.md
   ├─ creator-lifecycle.md
   ├─ creator-source-pool.md
   ├─ restaurant-ledger.md
   ├─ taste-profile.md
   ├─ recommendation-queue.md
   ├─ category-analysis.md
   ├─ source-watchlist.md
   ├─ trust-rubric.md
   └─ daily-update-log.md
```

## Usage

1. Use this repository as an Obsidian vault or a GitHub-backed Markdown knowledge base.
2. Update the files under `restaurant-intelligence/` periodically.
3. Register `skills/restaurant-trust-intelligence/SKILL.md` as a Codex skill or adapt it for another AI workflow.
4. Ask for restaurant recommendations with source evidence, trust level, sponsorship risk, taste fit, and menu-level reasoning.

## License

MIT
