# OpenClaw Company Template

这个仓库用于沉淀公司可复用的 OpenClaw 自定义层，不保存任何运行态、设备态或敏感凭据。

## 适用范围

适用于把 OpenClaw 落地到团队协作、财务运营、投资分析等场景时的角色分工、规则文档、模板配置和初始化说明。

## 仓库目标

- 统一沉淀角色分工和工作边界
- 复用主工作区与子工作区的规则文件
- 提供脱敏后的 `openclaw` 模板配置
- 方便其他同事在新机器或新环境复用

## 目录结构

```text
openclaw-company-template/
├── README.md
├── .gitignore
├── docs/
│   └── SETUP.md
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
        └── investment/
```

## 设计原则

- 只提交可复用内容，不提交运行态内容
- 不编造数据，不把占位符当真实配置
- 模板中的所有敏感字段必须保留为占位符
- 角色文档可以复用，密钥和设备状态必须本地化

## 当前角色映射

- `diana-chief-of-staff` → `Diana / Chief of Staff`
- `maya-operations-lead` → `Maya / Operations Lead`
- `iris-finance-operations-lead` → `Iris / Finance Operations Lead`
- `athena-investment-analyst` → `Athena / Investment Analyst`

## 不应提交的内容

- 真实 `openclaw.json`
- API Key、Bot Secret、Gateway Token
- `agents/**/auth-state.json`
- `agents/**/auth-profiles.json`
- `agents/**/sessions/**`
- `devices/**`
- `logs/**`
- `qqbot/sessions/**`
- `exec-approvals.json`

## 推荐使用方式

1. 克隆本仓库。
2. 将 `templates/workspace/` 下的文档同步到目标 OpenClaw 工作区。
3. 复制 `templates/config/openclaw.template.json` 为本地 `openclaw.json`。
4. 在本地填入真实路径、密钥和通道配置。
5. 再按实际团队情况补充 `TOOLS.md` 中的数据源登记。
