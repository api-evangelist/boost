---
name: Explore and inspect Boosts
description: Discover active onchain incentive campaigns (Boosts), page through them with filters, and pull the details and claim activity for one.
api: openapi/boost-v2-openapi.json
operations: [getBoosts, getBoost, getBoostActivity, exploreBoosts]
---

# Explore and inspect Boosts

The Boost V2 API is public and read-only. Base URL: `https://api-v2.boost.xyz`. No API key or token is required.

## Steps

1. **List boosts** — call `getBoosts` (`GET /boosts`). Filter with query params such as `chainId`, `owner`, `budgetAccount`, and `status`. Paginate with `page` and `pageSize` (max `pageSize` is 100). Stop when the returned `boosts` array is empty.
2. **Get one boost** — call `getBoost` (`GET /boosts/:id`) with the boost `id` to retrieve budget, allowlist, incentives, actions, and token metadata.
3. **Read claim activity** — call `getBoostActivity` (`GET /boosts/:id/activity`) to page through the history of claimed incentives for that boost.
4. **Discover trending contracts** — optionally call `exploreBoosts` (`GET /explore`) to surface boosts with the most claim activity and total USD distributed.

## Conventions & errors

- Pagination is offset-based (`page`/`pageSize`); see `conventions/boost-conventions.yml`.
- Errors return `{ "error": string | { "message": ... } }` (not RFC 9457); `400` = validation, `404` = not found, `410` = gone, `500` = server error. See `errors/boost-problem-types.yml`.
- All operations are GET, so calls are naturally safe to retry.
