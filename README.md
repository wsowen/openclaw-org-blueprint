# OpenClaw Company Template

这个仓库用于沉淀公司可复用的 OpenClaw 自定义层，不保存任何运行态、设备态或敏感凭据。

## 适用范围

适用于把 OpenClaw 落地到团队协作、财务运营、投资分析、客服服务等场景时的角色分工、规则文档、模板配置和初始化说明。

## 仓库目标

- 统一沉淀角色分工和工作边界
- 复用主工作区与子工作区的规则文件
- 提供脱敏后的 `openclaw` 模板配置
- 方便其他同事在新机器或新环境复用

## 这个仓库解决什么问题

如果每台机器都直接在本地 `.openclaw` 目录里手改，会逐渐出现这些问题：

- 角色命名和职责边界不一致
- 哪些文件能共享、哪些文件不能共享没有统一标准
- 同事接手新环境时，不知道该复制哪些内容
- 运行态文件、密钥和日志容易误入版本库

这个仓库的作用，就是把“可复用的组织层”和“必须本地化的运行层”分开。

## 目录结构

```text
openclaw-company-template/
├── README.md
├── .gitignore
├── docs/
│   ├── SETUP.md
│   └── TEMPLATE_SCOPE.md
├── adapters/
│   └── cursor/
│       └── bank-ledger-to-journal/
└── templates/
    ├── config/
    │   └── openclaw.template.json
    └── workspace/
        ├── AGENTS.md
        ├── IDENTITY.md
        ├── USER.md
        ├── SOUL.md
        ├── TOOLS.md
        ├── HEARTBEAT.md
        ├── operating/
        ├── financing/
        │   └── workflows/
        │       └── bank-ledger-to-journal/
        ├── investment/
        └── customer-service/
```

## 当前角色映射

- `diana-chief-of-staff` → `Diana / Chief of Staff`
- `maya-operations-lead` → `Maya / Operations Lead`
- `iris-finance-operations-lead` → `Iris / Finance Operations Lead`
- `athena-investment-analyst` → `Athena / Investment Analyst`
- `clara-customer-service-lead` → `Clara / Customer Service Lead`

## 设计原则

- 业务真源优先放在项目自己的 `templates/` 与 `workspace/` 目录中
- Cursor 相关能力只作为适配层，收纳在 `adapters/cursor/`

- 只提交可复用内容，不提交运行态内容
- 不编造数据，不把占位符当真实配置
- 模板中的所有敏感字段必须保留为占位符
- 角色文档可以复用，密钥和设备状态必须本地化
- 经营规则、角色边界、初始化流程适合走 git
- token、session、device、log、auth 状态只允许保留在本地

## 已模板化的内容

- 主工作区的人设、职责、规则、巡检节奏
- `operating` 子工作区的职责与边界
- `financing` 子工作区的财务运营职责与边界
- `investment` 子工作区的投资分析职责与边界
- `customer-service` 子工作区的客服服务职责与边界
- 脱敏后的 `openclaw.template.json`
- 初始化与落地说明

## 不应提交的内容

- 真实 `openclaw.json`
- API Key、Bot Secret、Gateway Token
- `agents/**/auth-state.json`
- `agents/**/auth-profiles.json`
- `agents/**/sessions/**`
- `devices/**`
- `identity/**`
- `logs/**`
- `qqbot/sessions/**`
- `exec-approvals.json`
- 本机路径相关的运行态文件

## 推荐使用方式

1. 克隆本仓库。
2. 阅读 `docs/SETUP.md`，先完成本地 OpenClaw 基础安装。
3. 将 `templates/workspace/` 下的文档同步到目标 OpenClaw 工作区。
4. 复制 `templates/config/openclaw.template.json` 为本地 `openclaw.json`。
5. 在本地填入真实路径、密钥、通道配置和实际团队数据入口。
6. 按团队情况继续补充 `TOOLS.md` 中的数据源、负责人和更新频率。

## 建议给同事的协作方式

- 调整角色边界、规则文档、模板结构时，先改这个仓库
- 调整本机 token、auth、设备状态时，只改本地 `.openclaw`
- 需要新增板块时，优先先在模板仓库里定义角色，再落到运行目录

## 相关文档

- 初始化步骤见 `docs/SETUP.md`
- 模板化范围与后续清单见 `docs/TEMPLATE_SCOPE.md`
