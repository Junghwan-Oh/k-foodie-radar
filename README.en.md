# k-foodie-radar

`k-foodie-radar` is a Markdown-based K-foodie radar for maintaining high-quality restaurant lists and suggesting visit candidates based on your personal taste.

It goes beyond generic “find me a restaurant nearby” search. It tracks trusted food creators, official guides, recommendation signals, sponsorship risk, menu-level reasons, and your evolving taste profile.

## Problem

Restaurant discovery is noisy.

Whenever you want to eat somewhere good, searching from scratch gets tedious. High-quality food YouTubers can recommend excellent restaurants, but watching multiple videos and then extracting the restaurant names, menus, prices, and locations is also a chore.

This project started from a simple question: "Can I easily turn one favorite food YouTuber's last few months of restaurant recommendations into a usable list?" From there, it grew into a broader skill for managing creators, official guides, personal taste, and real visit feedback together.

Map ratings, blog posts, and viral reviews often mix real information with ads and marketing. Following trusted food YouTubers manually also takes time. You may watch a long video only to find that the restaurant is not your style, or that there are too many candidates to turn into an actual visit list.

Shorts and Reels make this harder. A video can be genuinely useful, but the restaurant name may not appear in the title. The actual restaurant name, price, address, and menu details may be tucked away in the description or hashtags.

`k-foodie-radar` treats restaurant discovery as a personal assistant problem:

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
   - `taste-profile.md` stores the restaurant and menu signals the user personally values or dislikes.
   - Examples: best in category, national No. 1, craft-level quality, extreme value with real quality, personal favorites, repeat-visit restaurants.
   - This is separate from creator trust. `creator-registry.md` manages who to trust; `taste-profile.md` manages what the user likes.

6. Visit feedback layer
   - `visit-feedback.md` records real post-visit feedback.
   - Feedback updates both sides: restaurant/taste fit in `taste-profile.md`, and creator reliability in `creator-registry.md` and `trust-rubric.md`.

7. Visit queue
   - Separates immediate candidates, holds, stale entries, and restaurants that need operational verification.

## Why Manage Food Creators Separately?

Finding high-quality food creators is hard.

In this project, a high-quality food creator is not just someone with high views. They are closer to food specialists: people who may spend millions to tens of millions of KRW per month on restaurants and who build serious judgment through repeated dining. Reviewing recommendation lists from creators whose taste is similar to yours, or whose taste is similar in direction but more advanced/high-end, then choosing the restaurants that fit your own taste, has proven far more effective than generic search for increasing restaurant success rate and satisfaction.

Subscriber count alone does not mean a creator matches your taste, and having many videos does not automatically mean a creator fits your current purpose. A channel can make excellent content and still be less relevant to the specific goal of building a high-quality personal restaurant list for actual visits. Filtering out advertising, promotion, and marketing-heavy recommendations is especially important, but it is hard to judge from one or two randomly discovered videos.

That is why creators are managed as a list rather than treated as one-off search results. The system tracks who matches the user's taste, which categories they are strong in, whether sponsorship risk exists, and whether real visits validate their recommendations.

`k-foodie-radar` organizes creators into:

- First-tier creators to track immediately.
- Secondary creators for cross-checking.
- Hold candidates that need trust or taste validation.
- Held or excluded creators that do not currently fit the user's taste, purpose, or trust requirements.
- Chef/expert backup channels for fine dining and culinary context.

The creator list is not fixed. It should be edited for each user. Allowing creators to be added, updated, held, or removed based on visit feedback creates a self-improving loop: the user's taste can change, and creators' content direction or recommendation quality can also change over time.

## Taste And Feedback Management

The personal taste layer is not just a note about favorite foods. For the system to work well, three axes must stay separate:

1. Creator taste and trust
2. Restaurant and food preferences
3. Post-visit feedback loop

If all three are stored only in `taste-profile.md`, it becomes unclear whether the user trusts a creator, likes a cuisine, or simply had one good visit. Creator lists and personal taste lists should therefore be managed separately, while real visit feedback continuously updates both.

1. Food creator / influencer list
   - Managed in `creator-registry.md`, `creator-source-pool.md`, and `creator-lifecycle.md`.
   - Tracks whether a creator is trustworthy, sponsorship-heavy, aligned with the user's taste, or useful because their taste is more advanced/high-end than the user's.

2. Restaurant and menu taste list
   - Managed in `taste-profile.md` and `category-analysis.md`.
   - Tracks preferred signals, disliked signals, cuisine preferences, budget sensitivity, revisit intent, and menu-level taste.
   - Examples: "domestic No. 1 pizza", "craft-level meat restaurant", "expensive but justified omakase", or "cheap but quality-light value is not enough."

3. Post-visit feedback
   - Managed in `visit-feedback.md`.
   - After a real visit, mark the result as `hit / miss / neutral` and record what matched or failed.
   - A good visit can raise the weight of the source signal and the creator's category trust. A bad visit can downgrade similar signals or the creator's trust in that category.

The goal is to maintain a high-quality, personal-taste-aware restaurant radar that keeps suggesting places the user would actually want to visit.

## Example Requests

### Official Guide-Based

```text
List the 2025 Seoul Michelin starred/selected restaurants and Bib Gourmand restaurants separately.
For each restaurant, include cuisine, location, price range, reservation difficulty, and personal taste fit.
```

```text
From Seoul Blue Ribbon restaurants, shortlist realistic options under 50,000 KRW.
Mark restaurants that overlap with Michelin or Bib Gourmand.
```

### Creator-Based

```text
Summarize Jaesullang Guide's restaurant recommendations from the last three months by price tier.
Create Top 10 lists for all prices, under 100,000 KRW, under 50,000 KRW, and under 30,000 KRW.
For each restaurant, include a three-line recommendation, menu-level reasons, price range, location, and sources.
```

```text
List Seoul restaurants covered by Yooxicman within the last year.
Classify them into meat restaurants, burgers/sandwiches, and other restaurants.
For each restaurant, summarize the recommendation reason and representative menu.
```

```text
From Jobxicman videos, extract only restaurants with signals such as "national No. 1", "best in category", or "top waiting-list".
Re-rank them using my preference for craft quality, extreme value, and category-peak restaurants.
```

### Cross-Creator Validation

```text
Find restaurants commonly mentioned by creators A, B, and C.
For each overlapping restaurant, separate each creator's recommendation reason, main menu, price range, location, and sponsorship risk.
Move restaurants strongly recommended by only one creator into a separate candidate section.
```

```text
Find Seoul restaurants that overlap or are comparable across Jaesullang Guide, Jobxicman, and Kim Employee Meals.
Treat exact overlaps as higher-confidence candidates and genre-level overlaps as comparison candidates.
```

### Category, Region, and Taste-Based

```text
For seafood and raw fish, recommend only the strongest domestic candidates.
Separate evidence from trusted seafood creators and mark official guide recognition when available.
```

```text
Recommend the best restaurant candidates in Daejeon using official guides, creator mentions, and my personal taste profile.
Prioritize best-in-category, craft quality, and extreme value signals.
```

```text
For fine dining, use the chef/expert backup layer and explain why the menu is expensive dish by dish.
For course meals, include major course items and dish-level features; if details are missing, mark the restaurant as hold.
```

## Standard Recommendation Format

```markdown
Last checked: YYYY-MM-DD
Scope/condition:
Note: Always re-check hours, holidays, reservations, and operating status before visiting.

## Top N by Budget/Condition

| Rank | Restaurant | Three-Line Recommendation | Menu-Level Reasons | Price | Location | Source/Notes |
|---:|---|---|---|---|---|---|
| 1 | Restaurant name | 1) Strong recommendation signal. 2) Why it fits the user's taste. 3) When or why to visit. | `Menu A`: Why it is the representative order. `Menu B`: What it helps verify. |  |  |  |
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

As of 2026-05-18, Jaesullang Guide's recent three-month public YouTube upload window contains 54 Shorts and 3 regular videos, for 57 videos total. The confirmed total runtime is about 1 hour, 37 minutes, and 54 seconds. The public sample Markdown file is a shortened example that cites 21 representative sources used for the price-tier Top lists.

In other words, properly rebuilding a three-month creator list means reviewing more than 50 videos, separating recommendations from negative reviews, product reviews, and sponsored/marketing-heavy content, then extracting restaurant names, locations, price ranges, main menus, and actual recommendation reasons. The videos may be short, but the structuring work is still tedious.

Even after doing that work manually, the output often ends up as scattered map favorites, calendar notes, or a loose list with little context. It does not clearly preserve why a restaurant is worth visiting, what to order, or how well it fits the user's taste. With this skill, three months or even one year of creator videos can be turned into a clean Markdown restaurant list.

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

Instead of returning a plain list of titles, `k-foodie-radar` organizes the result by:

- Monthly ranking placement, repeat mentions, and strong title signals.
- Restaurant names, prices, locations, and menus extracted from descriptions and hashtags.
- At least three practical recommendation lines per restaurant.
- Menu-level reasons for the main order candidates.
- Course or omakase details, with uncertain entries held or downgraded when course details are missing.

Detailed Markdown versions are available here:

- [Jaesullang Guide recent three-month price-tier restaurant list sample](examples/jaesullang-guide-3mo-price-tier-sample.en.md)
- [Jobxicman recent three-month price-tier restaurant list sample](examples/jobxicman-3mo-price-tier-sample.en.md)

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
   ├─ visit-feedback.md
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
