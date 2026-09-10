# Browse Intent Activation Playbooks

These are starting points for lifecycle strategy. They are not part of the signal definition, are not guaranteed to improve performance, and may be changed by the user.

## Decision order

Use this order for every recommendation:

1. Respect consent, suppression, channel eligibility, and legal requirements.
2. Respect higher-priority lifecycle context such as checkout, cart, post-purchase, service, replenishment, winback, or an active promotion.
3. Check frequency, fatigue, deliverability, inventory, truthful urgency, and brand rules.
4. Use `BrowseIntent` to adjust relevance, pressure, timing, proof, education, creative, or offers.
5. Prefer the smallest test that can answer the decision. Include a holdout or baseline when practical.
6. Allow no action when another journey already serves the shopper well or the evidence is weak.

## State-level starting points

| State | Useful message job | Pressure and offer posture | Default fallback |
| --- | --- | --- | --- |
| `High` | Support a decision: restore relevant products, remove friction, add reassurance or proof, and use truthful urgency where appropriate. | Do not default to a discount. Test relevance, access, availability, confidence, or convenience first. | Existing lifecycle treatment if no meaningful intent-specific improvement is available. |
| `Medium` | Support evaluation: explain differences, answer objections, show use cases, comparisons, fit, quality, or social proof. | Moderate pressure. Use incentives selectively when a plausible friction or test hypothesis justifies them. | Standard nurture or existing lifecycle treatment. |
| `Low` | Build familiarity or trust with lighter, lower-pressure communication. | Do not assume disinterest or automatically suppress. Reduce pressure or frequency only when other evidence supports it. | Standard lifecycle logic, a lighter treatment, or no action. |
| `Expired` | Usually no intent-triggered treatment. Let current lifecycle evidence determine the next message. | Do not use old browse context as if it were current. | Normal lifecycle logic or no action. |
| Missing/unset | Diagnose readiness only when necessary; otherwise proceed without intent personalization. | Never treat as `Low` or `Expired`. | Normal lifecycle logic. |

## Combine intent with lifecycle context

Intent is not a customer type. Cross it with independently observed lifecycle facts.

- **Prospect or never purchased:** High can emphasize decision support and confidence; Medium can emphasize evaluation; Low can emphasize education and trust.
- **Returning customer:** High can emphasize relevance, replenishment, complementary products, availability, or access; Medium can refresh use cases or value; Low can use a lighter reminder where appropriate.
- **Lapsed customer:** Fresh High can be a re-entry signal without requiring generic winback language; Medium can emphasize what changed or renewed relevance; Low may call for a soft reintroduction or no action.
- **Active cart or checkout:** The active abandonment journey normally has priority. Use intent only if it creates a purposeful treatment difference.
- **Recent purchaser:** Post-purchase experience, service, and sensible replenishment timing normally take priority over browse pressure.

Never infer these lifecycle facts from `BrowseIntent`; verify them separately.

## Use-case playbooks

### Analyze campaigns

- Compare outcomes across exact intent states only after checking segment definitions, sample sizes, observation dates, and eligibility.
- Use delivered or eligible recipients as appropriate denominators.
- Include conversion and revenue outcomes plus unsubscribe or opt-out guardrails; opens and clicks are diagnostic, not sufficient on their own.
- Report correlation, selection effects, and uncertainty. Do not claim incremental lift without a valid control.

### Audit flows

- Identify where intent would change the job, pressure, timing, proof, creative, or offer.
- Prefer a conditional split inside an existing journey when that preserves priority and measurement more cleanly than duplicate flows.
- Flag overlapping journeys, stale branches, frequency conflicts, weak exclusions, or unsupported urgency.
- Recommend no split when every branch would receive materially the same treatment.

### Build segments

- Use the exact property and value casing.
- Build separate definitions for `High`, `Medium`, `Low`, and `Expired` only when each has a purpose.
- Keep missing and unexpected values outside canonical state segments unless the user explicitly creates a diagnostic segment.
- Add consent, suppression, channel eligibility, lifecycle, geography, and other conditions separately as the use case requires.

### Recommend or draft campaigns

- Begin with the audience's lifecycle job and the campaign objective.
- Use intent to shape the hypothesis, not to replace merchandising, brand, inventory, or eligibility decisions.
- For High, start with relevance and decision support before incentive escalation.
- For Medium, test education, reassurance, comparison, or targeted friction reduction.
- For Low, use lighter pressure or exclude the audience when the campaign objective and evidence justify it.
- Exclude `Expired` and missing from an intent-triggered campaign by default, but allow them into ordinary lifecycle campaigns under ordinary rules.

### Create flow variations

- Vary a meaningful strategic dimension: message job, timing, pressure, proof, creative role, channel role, or offer posture.
- Keep the number of variables small enough to interpret the result.
- Preserve a baseline or holdout where practical.
- Avoid equating High with urgent discounting, Low with disengagement, or Expired with suppression.

### Guide diagnostics

Ask one question at a time unless the user requests a checklist. Use this sequence:

1. Is the exact `BrowseIntent` property readable?
2. Which distinct values are present, including missing or unexpected values?
3. What is the task and lifecycle context?
4. Which channels are eligible, and what consent or suppression rules apply?
5. Which current campaigns or flows overlap?
6. Is the data fresh enough for the decision?
7. What single test or decision should be made first?

## Recommendation format

For each proposed treatment, provide:

- audience and exact state logic;
- lifecycle context and exclusions;
- message job and pressure level;
- channel and timing rationale;
- offer posture;
- baseline or holdout;
- primary outcome and safety metrics;
- review points before implementation;
- fallback or no-action path.
