# Template Scope

这份文档用于明确：

- 当前模板仓库已经覆盖了什么
- 当前 `.openclaw` 运行目录里还有哪些内容值得继续模板化
- 哪些内容不应该模板化

## 已模板化内容

### 主工作区

- `AGENTS.md`
- `IDENTITY.md`
- `USER.md`
- `SOUL.md`
- `TOOLS.md`
- `HEARTBEAT.md`

### 子工作区

- `operating/*`
- `financing/*`
- `financing/workflows/bank-ledger-to-journal/*`
- `investment/*`
- `customer-service/*`

### 配置模板

- `templates/config/openclaw.template.json`

### 文档

- `README.md`
- `docs/SETUP.md`

## 当前建议继续模板化的内容

这些内容目前还没有进入模板仓库，但后续很可能值得沉淀：

### 1. 数据源登记模板

建议后续补一套统一的数据源登记格式，例如：

- 数据源名称
- 负责人
- 更新时间
- 统计口径
- 可访问路径
- 是否允许作为正式依据

适合落位方式：

- 各工作区 `TOOLS.md` 的标准字段说明
- 单独的 `docs/DATA_SOURCE_TEMPLATE.md`

### 2. 经营汇总模板

建议后续补一套统一的经营摘要模板，例如：

- 本期核心结论
- 关键指标
- 异常事项
- 跨团队卡点
- 待管理层决策项

适合落位方式：

- `docs/REPORTING_TEMPLATES.md`
- 或主工作区下的固定模板文件

### 3. 日报/周报模板

建议为运营板块补齐：

- 日报模板
- 周报模板
- 超期事项汇总模板

适合落位方式：

- `templates/workspace/operating/`
- 或 `docs/REPORTING_TEMPLATES.md`

### 4. 财务运营口径模板

财务运营已经补齐第一批可落地模板，围绕“银行流水转分录草稿”包括：

- 标准字段模板
- 业务归类规则模板
- 分录草稿输出模板
- 待人工复核清单模板

后续仍建议继续补充：

- 回款口径
- 成本口径
- 预算口径
- 异常识别口径
- 正式科目映射规则

适合落位方式：

- `templates/workspace/financing/`
- 或单独 `docs/FINANCE_RULES.md`

### 5. 投资分析模板

建议后续补充：

- 标的分析框架
- 多标的比较模板
- 风险提示模板
- 数据来源与时间标注规范

适合落位方式：

- `templates/workspace/investment/`
- 或单独 `docs/INVESTMENT_ANALYSIS_TEMPLATE.md`

### 6. 客服板块模板

客服板块已独立成模板工作区，后续建议继续完善：

- FAQ 数据结构
- 投诉升级规则模板
- 售后场景模板
- 客诉分级与闭环模板

## 不应模板化的内容

以下内容应始终保留在本地运行目录，不进入模板仓库：

- 真实 `openclaw.json`
- API Key、Bot Secret、Gateway Token
- `auth-state.json`
- `auth-profiles.json`
- sessions 历史
- devices 配对状态
- logs 日志
- exec approvals 与 socket token
- 任何本机路径下的临时运行态文件

## 判断一项内容是否应模板化的标准

如果某项内容同时满足下面多数条件，就适合模板化：

- 会被多位同事复用
- 不包含敏感信息
- 是组织规则，而不是运行状态
- 在新环境部署时需要重复填写
- 可以抽象成占位符或标准结构

如果某项内容更像是下面这些，就不应模板化：

- 只属于一台机器
- 只属于一个账号
- 会随运行时不断变化
- 包含密钥、token、会话、日志


## 适配层说明

- `adapters/cursor/` 只存放面向 Cursor 的开发态适配层
- 业务规则本身应优先存放在 `templates/workspace/.../workflows/` 中
- 如果未来存在其他工具适配层，建议继续放在 `adapters/` 下按工具分类
