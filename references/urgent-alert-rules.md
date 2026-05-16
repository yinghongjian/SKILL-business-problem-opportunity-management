# Urgent Alert Rules

## Alert Triggers

Create an urgent alert when any condition is met:

- P0 item.
- S-level item.
- Hero product sellable days below 7 and recent sales are rising.
- Key milestone delayed more than 3 days and affects launch, campaign, or presale.
- Core channel GMV/GSV/profit abnormal decline for 2 consecutive days.
- Ad cost ratio rises sharply or ROI drops clearly.
- Clustered quality/customer complaint issue, including safety or false-advertising risk.
- Competitor stock-out, platform resource, or trend window that the team can quickly capture.
- Core owner has no valid business report for more than 7 days.
- Same issue repeats across two weeks and still has no responsible action.

## Alert Severity

- `critical`: P0, platform penalty, major customer complaint, hero product stock-out, severe overdue in core role.
- `high`: S-level, P1, high-value opportunity with short window, repeated A-level issue.
- `medium`: A/P2 item needing weekly tracking.
- `low`: observation only.

## Boss Alert Output

Each alert must include:

- Alert title.
- Why it matters.
- Evidence.
- Recommended action.
- Responsible person/department.
- Deadline.
- Whether boss decision is required.
- Human review status.

## Noise Control

- Do not alert the boss for low-evidence C/P3 items.
- If impact or timing is unclear, request clarification or send to owner first.
- Same item should not trigger repeated boss alerts unless severity changed, deadline passed, or new evidence arrived.
- All P0/S alerts default to `needs_human_review=true` before external push.
