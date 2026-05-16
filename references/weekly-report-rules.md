# Weekly Report Rules

## Standard Weekly Report Fields

- `report_id`
- `owner_id`
- `owner_name`
- `department`
- `report_time`
- `period_start`
- `period_end`
- `problem_text`
- `solution_text`
- `opportunity_text`
- `action_text`
- `achievement_text`
- `next_focus_text`
- `support_needed`
- `need_boss`
- `raw_source`
- `source_type`
- `platform_source`

## Half-Week Discipline

Rules:

1. Each active owner submits at least 2 half-week reports per natural week.
2. The gap between any two valid submissions should not exceed 4 days.
3. Multiple submissions by the same owner on the same day count as one valid submission day for discipline statistics.
4. More than 4 days since last valid submission: `overdue`.
5. More than 7 days since last valid submission: `severely_overdue`.
6. Two consecutive weeks below standard: enter boss weekly report.
7. HR-maintained owner list is the official denominator. If missing, use reported owners as test mode and label `test_mode=true`.

Metrics:

- Completion rate = owners meeting required count / required active owners.
- Timeliness rate = owners with no gap over 4 days / required active owners.
- Valid submission count = distinct owner/date pairs.

## Boss Weekly Report Sections

Generate 《奇动本周经营问题与机会总览》 with these sections:

1. 本周经营总览
2. 本周最重要的 5 个问题
3. 本周最重要的 5 个机会
4. 本周最重要的 5 个成果
5. S级/A级问题清单
6. P0/P1 紧急事项清单
7. 跨部门卡点
8. 已解决事项
9. 未解决事项
10. 需要老板拍板的事项
11. 下周重点跟进清单
12. 管理负责人经营贡献排名
13. 本周最佳问题发现者
14. 本周最佳机会发现者
15. 本周最佳解决方案
16. 本周最佳成果贡献者
17. 管理负责人周报完成率与及时率

Boss report writing rules:

- Put conclusions before detail.
- Prioritize S/A and P0/P1 items.
- Include evidence and suggested action for each high-priority item.
- Keep routine C/P3 items out unless they show a repeated pattern.
- Clearly mark `需要老板拍板` versus `仅需知情`.
