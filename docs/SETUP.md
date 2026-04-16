# Setup Guide

## 1. 准备目标目录

假设目标 OpenClaw 根目录为：

- `__OPENCLAW_HOME__`

## 2. 同步工作区文档

将 `templates/workspace/` 下的文件复制到目标目录：

- `templates/workspace/AGENTS.md` → `__OPENCLAW_HOME__/workspace/AGENTS.md`
- `templates/workspace/IDENTITY.md` → `__OPENCLAW_HOME__/workspace/IDENTITY.md`
- `templates/workspace/USER.md` → `__OPENCLAW_HOME__/workspace/USER.md`
- `templates/workspace/SOUL.md` → `__OPENCLAW_HOME__/workspace/SOUL.md`
- `templates/workspace/TOOLS.md` → `__OPENCLAW_HOME__/workspace/TOOLS.md`
- `templates/workspace/HEARTBEAT.md` → `__OPENCLAW_HOME__/workspace/HEARTBEAT.md`
- 子工作区同理

## 3. 生成本地配置

复制：

- `templates/config/openclaw.template.json` → `__OPENCLAW_HOME__/openclaw.json`

然后在本地填充：

- 实际目录路径
- 模型 API Key
- QQ Bot App ID / Secret
- Gateway token
- 其他本地专属信息

## 4. 安全提醒

不要把以下内容提交回模板仓库：

- 真实密钥
- 真实设备状态
- 会话历史
- 日志
- 本机路径下的运行态文件

## 5. 建议的复用方式

- 角色与规则文件走 git
- 凭据和运行态只保留在本地
- 真正的业务数据源名称与接入方式写入各工作区 `TOOLS.md`
