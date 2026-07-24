---
name: Surface RewardKit rewards for a user
description: Build a consumer-facing rewards feed with RewardKit — a user's profile of claimable rewards, reward details, and trending rewards.
api: openapi/boost-v2-openapi.json
operations: [getRewardKit, getRewardKitRewards, getRewardKitReward, getRewardKitTrending]
---

# Surface RewardKit rewards for a user

RewardKit wraps Boost incentives for consumer UX. All endpoints are public and read-only on `https://api-v2.boost.xyz`.

## Steps

1. **Load the user profile** — call `getRewardKit` (`GET /reward-kit`) to return a user's active, claimable, and unclaimed rewards.
2. **List available rewards** — call `getRewardKitRewards` (`GET /reward-kit/boosts`) with pagination and filters to render a rewards catalog.
3. **Get reward detail** — call `getRewardKitReward` (`GET /reward-kit/boosts/:id`), optionally passing a claimant address to decorate the reward with claim context.
4. **Show trending** — call `getRewardKitTrending` (`GET /reward-kit/trending`) with a `timePeriod` of `1h` or `24h` to surface high-volume rewards.

## Conventions & errors

- Offset pagination (`page`/`pageSize`, max 100); see `conventions/boost-conventions.yml`.
- The prebuilt React widget `@boostxyz/reward-kit-react` renders this surface directly; see `components/boost-components.yml`.
- Errors follow the `{ "error": ... }` envelope in `errors/boost-problem-types.yml`.
