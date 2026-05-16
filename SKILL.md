---
name: business-problem-opportunity-management
description: Use this skill when Hermes needs to turn weekly reports, half-week reports, group chat messages, form submissions, meeting notes, or business anomaly text into structured business problems, opportunities, solutions, achievements, owner scores, rankings, weekly boss reports, or urgent alerts for the 奇动/贝蒂服装电商经营团队. Trigger it for requests involving 经营问题、经营机会、半周报、老板周报、负责人贡献排名、S/A/B/C 价值评级、P0-P3 紧急评级、逾期未提交提醒、飞书/钉钉群聊周报入口, or business issue/opportunity ledgers.
metadata:
  preferred_model: gpt-5.5-pro
  provider: openai
  base_url: https://api.openai.com/v1
  api_key_env: OPENAI_API_KEY
---

# Business Problem And Opportunity Management

This skill converts loose operating text into a traceable management loop:

`周报/群消息/表单/会议纪要 -> 标准周报记录 -> 问题/机会/方案/成果拆分 -> 价值与紧急评级 -> 责任人与动作 -> 贡献评分 -> 老板周报/提醒`

## Load References

- Runtime routing defaults live in `runtime/model-routing.yaml`; Hermes should set `model=gpt-5.5-pro`, `base_url=https://api.openai.com/v1`, and read the API key from `OPENAI_API_KEY` whenever this skill is invoked.
- For value, urgency, solution, achievement, and evidence scoring, read `references/scoring-rubric.md`.
- For half-week report completion, timeliness, and boss weekly report sections, read `references/weekly-report-rules.md`.
- For owner contribution ranking and public榜单 rules, read `references/manager-ranking-rules.md`.
- For P0/S级/逾期/老板提醒 triggers, read `references/urgent-alert-rules.md`.
- Validate or shape outputs with the JSON schemas in `schemas/`.
- Execute multi-step tasks with the YAML workflows in `workflows/`.

## Core Rules

0. Never commit or print plaintext API keys. Use `OPENAI_API_KEY` from the runtime environment.
1. Preserve evidence. Every extracted item must keep `source_report_id`, `source_text`, or `evidence_refs`.
2. Do not invent missing fields. Use `null`, empty arrays, or `needs_clarification` when source data is insufficient.
3. Separate facts from judgment. Original text belongs in source fields; AI judgment belongs in rating, diagnosis, and action fields.
4. Split one report into multiple items when it contains multiple independent problems, opportunities, solutions, achievements, risks, or todos.
5. Rate value by business impact (`S/A/B/C`) and urgency by action window (`P0/P1/P2/P3`).
6. Mark `needs_human_review=true` for every S-level, P0, evidence-light high rating, unknown owner, or boss-facing escalation.
7. Suggested actions must say what to do, owner/department, deadline, validation metric, and whether cross-team or boss involvement is needed.
8. High-risk execution is advisory only. Do not approve punishments, price changes, listing removal, ad changes, or personnel actions automatically.

## Input Classification

Classify the incoming request before processing:

- `weekly_report_batch`: Excel/CSV/Word/Markdown/text file containing multiple owner reports.
- `single_half_week_report`: one person's group message or form report.
- `business_message`: ad hoc message, meeting note, anomaly, or operating observation.
- `manager_ranking_request`: request to score or rank owners.
- `weekly_boss_report_request`: request to generate 老板决策版周报.
- `urgent_alert_request`: request to find or push P0/S/overdue/high-value alerts.

## Standard Procedure

1. Normalize input into `weekly_report` records when the source is a report; otherwise create a `source_report_id` and keep raw text.
2. Extract business items:
   - problem: existing issue, risk, blocker, abnormal result.
   - opportunity: window to increase sales, margin, efficiency, inventory turnover, or customer experience.
   - solution: proposed method, action plan, SOP, or resource request.
   - achievement: completed improvement with result or evidence.
3. For each item, identify module, platform, category, SKU, impact metrics, responsible department/person, deadline, status, and evidence.
4. Rate each problem/opportunity/risk with `value_level` and `urgency_level`.
5. Generate concrete next actions and escalation flags.
6. Score solutions and achievements when present.
7. For owner-level tasks, aggregate items into `manager_score` and ranking output.
8. For report-discipline tasks, apply the half-week rules: at least two submissions per week, no gap over 4 days, severe overdue over 7 days.
9. For boss-facing outputs, include only high-signal conclusions, top issues/opportunities/achievements, P0/P1 lists, blockers, boss decisions, and owner contribution highlights.
10. Return machine-readable JSON when the caller asks for data; return concise Chinese management prose when the caller asks for a report.

## Output Contracts

Use these schemas as stable contracts:

- `schemas/weekly_report.schema.json`: normalized report record.
- `schemas/problem.schema.json`: extracted business problem or risk.
- `schemas/opportunity.schema.json`: extracted business opportunity.
- `schemas/solution.schema.json`: solution/action plan and quality score.
- `schemas/manager_score.schema.json`: owner contribution score and ranking.

## Quality Gate

Before final output:

1. Confirm each high-priority conclusion has evidence.
2. Confirm no unknown owner is treated as verified.
3. Confirm S/P0 items are flagged for human review.
4. Confirm rankings are value-weighted, not volume-only.
5. Confirm public outputs show positive榜单 and avoid public shaming.
6. Confirm urgent alerts are not noisy: if impact, timing, or evidence is weak, downgrade or request clarification.
