# Bloomio Browse Intent Signal Contract

This is the canonical public contract for interpreting Bloomio's browse intent signal. It intentionally excludes the private scoring formula and implementation details.

## Property contract

- Property name: `BrowseIntent`
- Canonical, case-sensitive values: `High`, `Medium`, `Low`, `Expired`
- Missing or unset is not a canonical value.

When reading account data, preserve unexpected values as a separate data-quality finding. Do not coerce capitalization or map unknown values without the user's approval.

## What the signal represents

Bloomio Browse Intent estimates a shopper's current level of intent from recent recognized browsing behavior. It uses a moving 90-day window and evaluates currently active, eligible profiles relative to the active population for that merchant.

The result is a current snapshot. It is inferred context, not directly observed intent. It is merchant-relative rather than a universal score.

## Canonical states

| State | Canonical meaning | Do not infer |
| --- | --- | --- |
| `High` | The profile is in the strongest current browse-intent group relative to the merchant's other active, eligible profiles. | Guaranteed purchase, consent, a customer type, or a need for a discount. |
| `Medium` | The profile is in the middle current browse-intent group relative to that active population. | Indifference, price sensitivity, or a specific lifecycle stage. |
| `Low` | The profile is in the weakest current browse-intent group among profiles that still have qualifying activity in the moving window. | No interest, inactivity, suppression, or ineligibility. |
| `Expired` | Bloomio still manages the profile for this signal, but no qualifying browsing session remains in the current moving window. | Unsubscribed, suppressed, deleted, globally inactive, or permanently low intent. |
| Missing/unset | The canonical state is unknown from the property. The profile may be unmanaged, ineligible, not yet synchronized, or affected by a data-readiness issue. | `Low`, `Expired`, or proof that no browsing occurred. |

## Moving-window behavior

The 90-day boundary moves forward over time. As activity ages beyond it:

- a currently active profile may change among `High`, `Medium`, and `Low` because the comparison population and its recent behavior changed;
- a profile may become `Expired` when its last qualifying session leaves the window;
- an `Expired` profile may return to `High`, `Medium`, or `Low` when new qualifying activity is recognized;
- a profile's relative level can change even without a new event from that profile, because other profiles change and older activity ages out.

Do not describe `Expired` as merely a score below `Low`. It is a different condition: no current qualifying session remains for a profile Bloomio manages.

## Analysis rules

When using account data:

1. Verify that the exact `BrowseIntent` property is readable.
2. Inspect the actual distinct values before defining segments or comparisons.
3. Keep `High`, `Medium`, `Low`, `Expired`, missing, and unexpected values distinct.
4. Record the observation period and data freshness when known.
5. Keep lifecycle status, purchase history, consent, suppression, and channel eligibility as separate dimensions.
6. Use merchant-specific baselines and holdouts where practical. Do not transfer a numerical threshold or expected lift from another merchant.
7. Describe associations as correlations unless a properly designed experiment supports a causal claim.

## Evidence and limits

Bloomio's field research found that stronger recent browse-intent groups were associated with stronger purchase outcomes across the studied merchants. That evidence supports prioritization and experimentation; it does not prove that the signal or a message caused a purchase and does not predict an individual's behavior.

Tracking quality, event coverage, identity resolution, eligibility, synchronization freshness, category, price point, inventory, offers, creative, and execution can affect how useful the property is in a particular account.

Public background:

- [Bloomio whitepaper: Browsing Intent - A Practical Shopper Intent Signal for Ecommerce](https://bloomio.ai/whitepaper/browsing-intent-practical-shopper-intent-signal-ecommerce-phil-roselli-july-2026.pdf)
- [Bloomio guide: How to use AI to activate Bloomio in Klaviyo](https://bloomio.ai/blog/how-to-use-bloomio-in-claude-and-composer)
