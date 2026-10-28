# Varla KOL 邮件总控台 / Varla KOL Command Center

**简体中文** | [English](README.en.md)

在本地网页集中识别 KOL 邮件、分类任务、检索知识、预览回复和检查组件状态。

[下载完整项目包](https://github.com/hezonglinhzl-creator/varla-electric-mobility-skills-and-tools/raw/main/packages/skill-varla-kol-command-center.zip) · [全部项目](https://github.com/hezonglinhzl-creator/varla-electric-mobility-skills-and-tools)

## 功能特性

- KOL、售前、物流和售后四类任务
- 预览、人工确认和暂停
- 本地知识主存储与低频飞书检查

## 这个包里有什么

| 内容 | 位置 |
| --- | --- |
| KOL 邮件总控台程序 | [varla-kol-command-center](apps/varla-kol-command-center/README.md) |
| Skill 指令 | [SKILL.md](skill/varla-kol-command-center/SKILL.md) |

## 下载和解压

1. 在本仓库点绿色 **Code → Download ZIP**，或者点上方“下载完整项目包”。
2. 下载完成后右键 ZIP，选择**全部解压**，打开能看到此 README 的文件夹。
3. 保留整个目录；先按下一节准备程序，再安装和使用对应 Skill。

安装时还会在目标 SKILL.md 旁写入 PACKAGE-LOCATION.json，记录完整包和程序的真实位置。保留整个解压目录；搬家后重新运行安装器。默认保留已有 Skill 内容，只刷新程序位置映射。

## 1. 先准备程序

### KOL 邮件总控台程序 (`varla-kol-command-center`)

Windows、Python 3.11+；Gmail/回复/合同/飞书组件需各自配置。

先进入 `apps/varla-kol-command-center`。本地 WebUI、四类邮件路由、知识检索、回复预览、人工确认与暂停。

1. 先配置可选环境变量 VARLA_KOL_DATA_DIR（数据目录）、VARLA_KOL_REPLY_ROOT（回复程序路径）和 VARLA_KOL_EXPECTED_ACCOUNT（核验邮箱），再准备自己的 Gmail 授权。默认数据目录为 %LOCALAPPDATA%/VarlaKOLCommandCenter。
2. 原一键入口是 `START_KOL_COMMAND_CENTER.bat`；它依赖本机 Codex 捆绑 Python，不存在时用下面的手动方式。
3. 手动：在本目录运行 `python -m venv .venv`，再运行 `.\.venv\Scripts\python.exe -m pip install -r requirements.lock`。
4. 运行 `.\.venv\Scripts\python.exe -m uvicorn app.main:app --host 127.0.0.1 --port 8791`。
5. 打开本地地址，先看系统自检。配置缺失时先修复，不直接点击邮件识别。

本地地址：`http://127.0.0.1:8791/`

[查看完整程序与浏览器插件安装说明](apps/varla-kol-command-center/README.md)

公开分发版后台垃圾邮件清理默认关闭；仅设置 VARLA_ENABLE_JUNK_CLEANUP=true 才启动定时线程。识别/手动清理按钮仍可能修改邮箱。config.example.json 仅供参考，程序读取启动环境变量；Gmail OAuth 文件实际位于数据根目录 gmail-credentials.json 与 gmail-token.json。未提供业务知识时可打开设置界面，但回复必须转人工。

## 2. 再安装 Skill

1. 回到解压后的项目根目录，双击 `安装Skill.cmd`。
2. 安装器把 `skill/varla-kol-command-center` 复制到 `%USERPROFILE%\.codex\skills\varla-kol-command-center`。遇到同名 Skill 会跳过，留意窗口结果。
3. 重新打开 Codex，新建对话，使用下面的 Skill 名称和示例。
4. 公司策略禁止脚本时，可先阅读 install.ps1，或手动把整个 Skill 目录复制到同一目标位置。

## 3. 第一次怎么用

| 准备项 | 内容 |
| --- | --- |
| 输入 | 本机 Gmail、回复助手、合同更新器与飞书组件配置。 |
| 输出 | 本地任务列表、待审核回复和执行审计。 |

```text
使用 varla-kol-command-center，先做系统自检和组件配置检查，告诉我哪些可用；不要扫描或修改邮箱。
```


## 当前限制与常见问题

首次迁移要配置外部组件路径。识别和垃圾邮件清理可能写邮箱，开始前阅读程序里的详细说明。页面打开不代表各组件都连接成功。

| 问题 | 怎么处理 |
| --- | --- |
| 找不到 Skill | 检查安装窗口结果和目标 SKILL.md，重新打开 Codex 并新建对话。 |
| 程序启动失败 | 在程序目录打开 PowerShell 运行本文命令，让错误保留在窗口，再对照对应程序 README。 |
| 网页看不到插件 | 确认选中直接包含 manifest.json 的目录、网站受支持，并刷新网页。 |
| 外部服务不可用 | 配置自己的授权并检查资源权限；保留本地结果，不把失败说成同步/发送成功。 |

## 隐私与验证范围

这是程序源码与 Skill 分发包，不附带真实账号、OAuth 令牌、客户/KOL 台账、合同、订单、邮箱导出或业务媒体。服务需使用自己的配置。已检查文档和包内入口；此次文档核对没有执行真实下单、发邮件或发布内容。
