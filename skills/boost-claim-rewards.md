---
name: Generate a Boost claim signature
description: Find claimable incentives for a wallet address and obtain the server-generated signature needed to claim a reward onchain.
api: openapi/boost-v2-openapi.json
operations: [getClaimableSignatures, getSignatures, getBoost]
---

# Generate a Boost claim signature

Rewards are claimed onchain, but the signature authorizing a claim is fetched from the Boost V2 API (`https://api-v2.boost.xyz`, public/read-only).

## Steps

1. **Find claimable signatures** — call `getClaimableSignatures` (`GET /signatures/claimable/{address}`) with the claimant wallet `address` to list all signatures not yet used to claim.
2. **Confirm the boost** — call `getBoost` (`GET /boosts/:id`) for the associated boost to verify incentive, token, and allowlist details before claiming.
3. **Generate a claim signature** — call `getSignatures` (`GET /signatures`) supplying the transaction hash, boost `id`, and valid claim data hash to receive a signature usable to submit the onchain claim.
4. **Submit onchain** — use the returned signature with the Boost SDK/contracts (`@boostxyz/sdk`) to execute the claim transaction.

## Conventions & errors

- A `410 Gone` on `getSignatures` means the claim context has expired or was removed — re-check claimable signatures.
- `400` indicates malformed address/hash inputs. See `errors/boost-problem-types.yml`.
- No authentication is required for the API; the onchain claim is authorized by the wallet signature. See `authentication/boost-authentication.yml`.
