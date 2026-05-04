# Setup Guide

## 目标

把这个模板仓库中的“组织层配置”同步到一个新的 OpenClaw 运行目录中，同时确保密钥、设备状态和日志等内容仍然只保留在本地。

## 前置条件

在开始之前，请确保目标机器已经具备：

- OpenClaw 已安装
- 基础 onboarding 已跑通
- 本地 `.openclaw` 根目录已存在
- 你知道目标目录路径，例如 `__OPENCLAW_HOME__`

## 1. 准备目标目录

假设目标 OpenClaw 根目录为：

- `__OPENCLAW_HOME__`

通常你至少应能看到这些目录或文件：

- `__OPENCLAW_HOME__/workspace`
- `__OPENCLAW_HOME__/agents`
- `__OPENCLAW_HOME__/openclaw.json` 或可新建该文件

## 2. 同步工作区文档

将 `templates/workspace/` 下的文件复制到目标目录：

- `templates/workspace/AGENTS.md` → `__OPENCLAW_HOME__/workspace/AGENTS.md`
- `templates/workspace/IDENTITY.md` → `__OPENCLAW_HOME__/workspace/IDENTITY.md`
- `templates/workspace/USER.md` → `__OPENCLAW_HOME__/workspace/USER.md`
- `templates/workspace/SOUL.md` → `__OPENCLAW_HOME__/workspace/SOUL.md`
- `templates/workspace/TOOLS.md` → `__OPENCLAW_HOME__/workspace/TOOLS.md`
- `templates/workspace/HEARTBEAT.md` → `__OPENCLAW_HOME__/workspace/HEARTBEAT.md`

子工作区同理：

- `templates/workspace/operating/*` → `__OPENCLAW_HOME__/workspace/operating/`
- `templates/workspace/financing/*` → `__OPENCLAW_HOME__/workspace/financing/`
- `templates/workspace/financing/workflows/bank-ledger-to-journal/*` → `__OPENCLAW_HOME__/workspace/financing/workflows/bank-ledger-to-journal/`
- `templates/workspace/investment/*` → `__OPENCLAW_HOME__/workspace/investment/`
- `templates/workspace/customer-service/*` → `__OPENCLAW_HOME__/workspace/customer-service/`

如果目标目录还没有某个子工作区，请先创建对应目录。

## 3. 生成本地配置

复制：

- `templates/config/openclaw.template.json` → `__OPENCLAW_HOME__/openclaw.json`

然后在本地填充：

- 实际目录路径
- 模型 API Key
- QQ Bot App ID / Secret
- Gateway token
- 其他本地专属信息

## 4. 本地化必须补齐的内容

模板同步完成后，至少要继续补这几类信息：

- `TOOLS.md` 中的数据源名称、负责人、更新频率
- 各团队的真实业务规则和升级路径
- 机器本地的模型认证状态
- 真实通道配置和访问权限

## 5. 验证建议

建议至少做以下检查：

1. 打开 `openclaw.json`，确认路径占位符已经替换为本机真实路径。
2. 检查 `workspace/` 与各子工作区文档是否已同步到位。
3. 确认敏感字段没有留在模板占位符状态，也没有把真实密钥回写到模板仓库。
4. 启动或重载 OpenClaw 后，确认 agent 列表与角色名已生效。

## 6. 安全提醒

不要把以下内容提交回模板仓库：

- 真实密钥
- 真实设备状态
- 会话历史
- 日志
- 本机路径下的运行态文件
- `auth-state.json`、`auth-profiles.json`

## 7. 建议的复用方式

- 角色与规则文件走 git
- 凭据和运行态只保留在本地
- 真正的业务数据源名称与接入方式写入各工作区 `TOOLS.md`
- 新增业务板块时，优先先在模板仓库定义，再同步到运行目录
