# Manager Ranking Rules

## Contribution Formula

```text
total_score =
problem_discovery_score * 0.25
+ opportunity_discovery_score * 0.20
+ solution_quality_score * 0.25
+ achievement_score * 0.20
+ review_learning_score * 0.10
```

## Problem Discovery Score

```text
problem_score = value_base_score * urgency_multiplier + early_warning_bonus + evidence_bonus
```

Value base:

| Value | Base |
|---|---:|
| S | 100 |
| A | 80 |
| B | 50 |
| C | 20 |

Urgency multiplier:

| Urgency | Multiplier |
|---|---:|
| P0 | 1.30 |
| P1 | 1.15 |
| P2 | 1.00 |
| P3 | 0.80 |

Bonuses:

- Early warning before loss occurs: +5 to +15.
- Strong evidence: +5 to +10.
- Repeated vague issue without new insight: no bonus.

## Opportunity Discovery Score

```text
opportunity_score = value_base_score * execution_window_multiplier + executability_bonus + timing_bonus
```

Use higher scores for platform resources, competitor stock-outs, traffic trend windows, inventory clearance windows, margin improvement, or fast conversion gains with evidence.

## Anti-Gaming Rules

- Do not rank by submission count alone.
- Do not reward vague descriptions.
- Do not over-reward after-the-fact explanations.
- Problem discovery cannot exceed 40% of final score after normalization.
- Solution score should be corrected by later results when available.
- Public output should show positive lists only; negative discipline issues go to HR/manager channels.

## Required Ranking Outputs

- Overall manager contribution ranking.
- Best problem discoverer.
- Best opportunity discoverer.
- Best solution.
- Best achievement contributor.
- Representative case for every ranked owner.
- `needs_human_review=true` when ranking affects performance evaluation or source data is incomplete.
