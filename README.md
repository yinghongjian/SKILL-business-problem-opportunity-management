# 经营问题与机会管理 Agent Skill

目录用于 Hermes 调用经营问题与机会管理能力。

## 触发方式

当用户或上游 Agent 提到以下任务时，调用 `SKILL.md`：

- 解析周报、半周报、日报、会议纪要、飞书/钉钉群消息。
- 提取经营问题、机会、解决方案、成果、风险、待办。
- 生成 S/A/B/C 价值等级和 P0/P1/P2/P3 紧急等级。
- 统计每周 2 次半周报完成率、及时率、逾期名单。
- 生成老板决策版周报。
- 计算管理负责人经营贡献排名。
- 识别需要当天提醒老板或责任人的事项。

## Hermes 使用步骤

1. 读取 `.agents/skills/business-problem-opportunity-management/SKILL.md` 判断任务类型。
2. 调用该 Skill 时读取 `runtime/model-routing.yaml`，默认使用：
   - `model`: `gpt-5.5-pro`
   - `base_url`: `https://api.openai.com/v1`
   - `api_key_env`: `OPENAI_API_KEY`
3. 在运行环境设置 `OPENAI_API_KEY`，不要把明文 key 写入仓库、Prompt、日志或报告。
4. 按任务加载对应 reference：
   - 评级和打分：`references/scoring-rubric.md`
   - 周报纪律和老板周报：`references/weekly-report-rules.md`
   - 负责人排名：`references/manager-ranking-rules.md`
   - 紧急提醒：`references/urgent-alert-rules.md`
5. 按 workflow 执行：
   - 半周报跟进：`workflows/half_week_report_flow.yaml`
   - 事项提取：`workflows/problem_opportunity_extraction_flow.yaml`
   - 负责人排名：`workflows/manager_ranking_flow.yaml`
   - 紧急提醒：`workflows/urgent_alert_flow.yaml`
6. 输出前用 `schemas/` 中的 JSON Schema 校验字段。
7. 需要示例时读取 `examples/`。

## 关键约束

- 任何高价值、高紧急、老板提醒、绩效相关输出都必须保留证据。
- S 级和 P0 默认需要人工复核。
- 不允许凭空补齐负责人、金额、日期、款号、平台或经营结果。
- 排名按经营价值和证据评分，不按提交数量简单排序。
- 对外公开只发正向榜单；逾期和低质量问题走人事/直属负责人私域处理。
- API key 只允许通过环境变量注入；仓库只保留 `.env.example` 占位模板。
