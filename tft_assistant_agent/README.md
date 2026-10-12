# DSH 上下文 SDK 项目

本项目开发可嵌入 DSH（DeepSeek Harness）的上下文管理 SDK，用于长会话中的历史压缩、任务状态维护、历史检索和模型输入组装。

当前包含本地迁入的 DSH 源码与上下文管理设计资料，SDK 功能尚未实现。

## 项目入口

- [产品需求](docs/产品需求.md)：项目目标、首版范围、DSH 接入要求与验收条件。
- [DSH 源码](dsh/)及其[中文说明](dsh/README.zh.md)。
- [上下文 SDK 设计](research/context-management/上下文SDK设计.md)：接口与技术方案草案。
- [研究资料索引](research/context-management/README.md)。

## 目录

```text
dsh/         DSH 源码、依赖与原有构建产物
docs/        本项目产品需求
research/    上下文管理研究与设计资料
```

DSH 源码由当前 Git 仓库统一管理；迁入版本为 `76fda729799fe9b3848dbe2c211d4b231032b81e`。原 DSH Git 历史保存在 `.migration-backup/dsh.git`，该备份目录不纳入版本控制。DSH 的许可证与第三方声明见 [LICENSE](dsh/LICENSE) 和 [THIRD_PARTY_NOTICES.md](dsh/THIRD_PARTY_NOTICES.md)。

## 从源码运行 DSH

本地迁入版本要求 Node.js `^22.19.0 || >=24.0.0`，使用 `pnpm@11.7.0`。

```bash
cd dsh
pnpm install
pnpm run build
pnpm dsh web
```

模型配置与使用说明见 [DSH 中文说明](dsh/README.zh.md)；修改 DSH 时遵循 [DSH 开发规则](dsh/AGENTS.md)。
