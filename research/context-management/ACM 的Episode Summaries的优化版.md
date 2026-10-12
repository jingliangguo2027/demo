问题：尽可能避免 recursive summary但是如果是长任务，那么每次压缩都使用全部上下文，那么这个内容非常非常多，巨大影响压缩效果
解决方案：
ACM 方案的优化版！
1. Raw Event Log 在当前 session 存续期间保存；删除 session 时，原文、摘要和相关索引一并删除，不作为跨 session 的全局记忆。
2. 历史记录每次触发压缩时（任务完成，上下文到达上限，etc..)，都生成一个新的Episode
3. 每个Episode 独立压缩：Raw E6 → E6，根源避免 recursive compression：acm 做法，完全无上下文压缩
4. Episode 不是无上下文压缩：压 E6 时提供能够基本完整表示当前状态的上下文：Rules + Current State + relevant previous episodes 作为 read-only conditioning context，如果Episode 6 中有不明确的信息，而且在之前的索引中看到类似信息，可以调用工具按需取特定上下文。：gjl 难道真是科研天才？
5. Current State 应该 recursive compression，例如 Goal / Decisions / Completed / Pending / Constraints。
6. Episode Summary 同时承担索引作用，可以记录 entities / files / decisions / depends_on / unresolved 等信息。：这里也需要trade off 长度和信息详细长度，因为 E 也可能非常多
7. 模型处理问题时若需要旧细节时，调用工具按需调取上下文，可以是压缩版或者完整版：E summary → retrieve E → 必要时 retrieve raw
Episode 太多以后不能把所有 E 都塞进去，需要进一步做 Hybrid Retrieval / hierarchical index。：这个是更拓展的做法，毕竟上下文是可以无限的，不可能总是记住，暂时可以不处理



