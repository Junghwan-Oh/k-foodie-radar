# Taste Profile

Last updated: 2026-05-18

## Purpose

This is the persistent "AI taste" profile for ranking restaurants for the user. Update it only from explicit user feedback, repeated user choices, and clear preference statements.

## Core Preference Update - 2026-05-18

The user does not simply want popular restaurants or viral places. The preferred signal is a strong "category peak" or "personal canon" recommendation from a trusted creator.

High-value recommendation language and contexts:

- 해당 분야 최고 맛집
- 국내 1위 / 장르 1위 / 이 분야 끝판왕
- 극강의 가성비
- 장인의 퀄리티
- 인생맛집
- 자주 가게 되는 단골 맛집
- 무조건 와봐야 할 경험
- 돈 내고 반복 방문한 집
- 비교/랭킹 콘텐츠에서 살아남은 최종 추천

Creator selection baseline: choose creators whose restaurant taste is similar to the user, or creators whose taste is clearly more advanced/high-end than the user. Similar-taste creators are useful for immediate visits; higher-end creators are useful for learning, special meals, omakase/fine dining, and long-term wishlists. Creators that mainly do generic promotion, marketing, product placement, or shallow hype should be downgraded or removed.

Scoring additions:

| Signal | Weight | Notes |
|---|---:|---|
| Trusted creator says category-best / domestic No.1 / life-best / regular haunt | +3 | Strongest creator-language signal when backed by concrete dish details and no major ad risk. |
| Extreme value with craft-level execution | +2 | 극강의 가성비 is valuable only when quality is also high, not cheapness alone. |
| Master/craftsperson quality signal | +2 | 장인성, 분야 전문성, repeated refinement, and category expertise matter. |
| Creator/content is mainly promotion or marketing | -3 | Remove or downgrade creators whose restaurant picks feel like ads rather than taste judgment. |
| "Hot place" without category-best or repeat-visit logic | -2 | Trendiness alone is weak evidence. |

## Current Taste Hypotheses

These are weak starting hypotheses from conversation and should be confirmed.

| Signal | Confidence | Evidence | Notes |
|---|---|---|---|
| Wants source-backed recommendations, not generic list dumps | high | User corrected unsupported creator attribution | Must separate direct mentions from Codex-added info. |
| Interested in sushi/omakase and Japanese restaurants | medium | User wanted to visit Sushi Jihyun | Need more feedback before weighting too strongly. |
| Values serious food creators but distrusts ad-like recommendations | high | User requested creator trust structure and ad/reliability evaluation | Always label sponsorship risk. |
| Likes both high-end curated lists and accessible local finds | medium | Mentioned Michelin/Bib Gourmand/Blue Ribbon plus several YouTubers | Balance special occasion and practical options. |
| First-tier creator set is fixed around 재슐랭, 잡식맨, 김사원세끼, 빅페이스, 서울 사는 남자, 정육왕 | high | User explicitly confirmed these fit best and moved 정육왕 to 1군 | Track these first; other creators require validation. |

## Positive Taste Signals

Explicit user update: 잡식맨's domestic No.1 pizza recommendation around Ilsan and Gangnam is a high-confidence positive signal. Treat 잡식맨 pizza ranking/comparison videos as especially useful, while still separating ads and current operation checks.

| Category | Weight | Notes |
|---|---|---|
| Verified official guide recognition | +2 | Michelin/Bib Gourmand/Blue Ribbon should seed discovery. |
| Multiple independent trusted creator mentions | +2 | Only official direct mentions count. |
| Concrete criticism and ordering detail in source | +2 | More trustworthy than hype. |
| Recent operational clarity | +1 | Reservations, closure, wait, and opening status matter. |
| User post-visit hit | +3 | Strongest personal signal. |
| First-tier creator direct restaurant visit | +2 | Add to queue by default, then verify operation and ad risk. |
| 잡식맨 direct pizza ranking/comparison recommendation | +3 | User singled out this signal as highly trustworthy and useful. |
| Course/omakase recommendation includes dish-level course details | +2 | For course meals, list major course items and why each matters; generic "omakase/course" labels are insufficient. |

## Negative Taste Signals

| Category | Weight | Notes |
|---|---|---|
| Creator mention is sponsored/invited with little detail | -2 | Keep as discovery only unless corroborated. |
| Generic viral hype without dish-level details | -2 | Avoid leading with these. |
| Course/omakase recommendation lacks course composition | -2 | Hold or downgrade until representative dishes and features are identified. |
| Current closure or unclear booking status | -3 | Exclude or hold. |
| User post-visit miss | -3 | Also downgrade similar source signals. |
| Unverified creator attribution | -3 | Do not present as recommendation. |

## Cuisine And Situation Preferences

| Cuisine/Situation | Preference | Confidence | Evidence |
|---|---|---|---|
| Sushi / Japanese | like | medium | Sushi Jihyun interest. |
| Pizza / pizzeria | like | high | User strongly trusted 잡식맨's domestic No.1 pizza recommendation, including the Ilsan pick and a Gangnam-area pick. |
| Meat-focused restaurants | unknown | low | Discussed meat creators, not enough visit feedback. |
| 정육왕 meat recommendations | like | high | User said 정육왕 is verified for skill/quality; lack of visits is due to recommendation exposure. |
| Everyday local finds | like | medium | Compared creator styles and local recommendations. |
| Expensive fine dining | conditional | medium | Wants official guide layer but noted pricey creator tendency. |

## Post-Visit Feedback Link

Detailed post-visit records should live in `visit-feedback.md`.

Use this file only for durable taste changes, such as:

- a repeated positive or negative signal;
- a cuisine/category preference change;
- a price/value rule that should affect future ranking;
- a menu-level preference that should be reused in recommendations.
