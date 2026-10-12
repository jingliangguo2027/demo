# 飞书研究文档索引

以下正文文件最初由飞书 Wiki 原文复制；后续已按用户要求进行本地修订，不再保证与飞书原文一致。下表保留原始来源，本次修订未同步回飞书。

| 文件 | 飞书来源 |
| --- | --- |
| [上下文管理设计.md](./上下文管理设计.md) | https://glarkusbgbb2z8f3.usttp.larksuite.com/wiki/PkpSwAVfBi0Q7RkdjnJu5at6tlr |
| [Current Task State设计.md](./Current%20Task%20State设计.md) | https://glarkusbgbb2z8f3.usttp.larksuite.com/wiki/KOCtwdwUQi4h5ekCRx9urFqut0c |
| [ACM 的Episode Summaries的优化版.md](./ACM%20的Episode%20Summaries的优化版.md) | https://glarkusbgbb2z8f3.usttp.larksuite.com/wiki/RcLDwFJ5KiiIv4kaTBAuPjxctQb |
| [文本压缩具体方案.md](./文本压缩具体方案.md) | https://glarkusbgbb2z8f3.usttp.larksuite.com/wiki/U8uLwa2Hhizt00k5e8yuxMTJt3c |

## 本地新增设计

| 文件 | 内容与来源 |
| --- | --- |
| [DSH 上下文 SDK 产品需求](../../docs/产品需求.md) | 首个宿主为 DSH；概述项目目标、首版范围、接入要求与验收条件 |
| [上下文 SDK 设计](./上下文SDK设计.md) | 根据本次对话新增：接口、内部组件、事件和快照契约、异步交接、失败处理；未同步到飞书 |
| [上下文 SDK 调研任务清单](./上下文SDK调研任务清单.md) | SDK 的独立调研任务、指导、依赖关系和预期产出；未同步到飞书 |

## 对话分析落文档核对（2026-09-18）

上一轮并未将全部分析写入文档；本轮补齐以下内容。建议、假设和研究项均不代表已经实现或验证。

| 对话内容 | 对应文档位置 |
| --- | --- |
| 删除 Recent Compressed、四层组装顺序、历史注入与预算 | 总体设计：上下文层、Context Builder 组装建议；SDK 第 4 节 |
| Current Task State 事件驱动更新、任务恢复与版本 | Current Task State 设计全文 |
| 异步压缩边界、等待点、短时提交、失败回退 | 总体设计：异步 Episode 压缩交接建议；SDK 第 5、7 节 |
| 摘要过时与生成失真、证据回查和信任边界 | 文本压缩具体方案：2.4、2.7 |
| 早期模型五权重、分数处理、有效性与新近性 | 总体设计：非首版五权重研究建议；当前首版采用两路固定融合，见 SDK 第 6 节 |
| 旧 TP 阶段快照、任务重开、版本与新 Raw 覆盖 | 文本压缩具体方案第 4 节末尾的历史研究内容；当前首版采用轻量 TP |
| 单 session 范围与全量关联数据删除 | 总体设计：适用范围与生命周期、Session 删除规则；SDK 第 1、7 节 |
| SDK 接口、内部封装、适配器与宿主边界 | SDK 第 1—3、8 节 |
| 评测、诊断、性能和进一步研究 | SDK 第 9 节；调研任务清单全文 |

## 首版检索讨论结论（2026-10-03）

已确认首版只使用关键词召回（lexical）与语义召回（semantic），采用固定融合策略，去重后按 token 预算返回，模型暂不调权。Graph、recency、importance 不参与首版排序；来源引用、新旧版本与有效性判断仍保留。先跑通两路召回，再考虑其他优化；具体融合算法和参数尚待实现与验证。

对应文档：上下文管理设计的“首版两路召回”、上下文 SDK 设计第 1、2、6、8 节、产品需求第 3 节，以及调研任务 R09 / R12。早期五权重设想保留为后续研究内容。

## 轻量 TP 讨论结论（2026-10-03）

已确认采用“功能 / 主题的简单介绍 + 相关 Raw 引用 + 各 Raw 中该功能相关的摘要”，只追加新增材料；主循环、Context Builder 和 Episode 发布不等待独立 TP 后台作业。该方向尚未实现或验证，字段与接口仍为草案。

- 当前结构、登录功能示例、增量更新、隔离、时效与发布修订：文本压缩具体方案第 4 节。
- SDK 接口与数据对象、独立后台发布和删除：上下文 SDK 设计第 2、3、5、7 节。
- 总体职责与任务状态边界：上下文管理设计的“轻量 Task Package”及 Current Task State 设计。
- 产品要求及待验证收益：产品需求第 3–6 节、调研任务 R10。

旧完整任务快照、完成检测与 `version + revision / update` 方案保留为历史研究内容，不作为当前 TP 的更新流程。

早先企业级对比中的全局记忆、跨 session 共享和多租户服务，不属于当前 SDK 的实现目标。session 间数据隔离、来源信任和删除一致性仍需保证。
