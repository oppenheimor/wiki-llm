---
name: Agent 四层体系（2026 初）
description: 把 2026 年初 Agent 生态的能力跃迁拆解为大脑/手脚/组织/进化四层叠乘的分析框架
type: pattern
---

# Agent 四层体系（2026 初）

> 一个用来解释"2026 年初 AI 圈到底变了什么"的分层拆解框架。单看每一层都是渐进式进步，四层叠加的效果是乘出来的。

来源：歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25，微信公众号）

## 问题背景

2026 年春节前后，行业内多篇"奇点已到"的长文爆发——Matt Shumer《Something Big Is Happening》、Dario Amodei《The Adolescence of Technology》、"赛博禅心"《我们，已迈过奇点》、"有机大橘子"《互联网已死，Agent 永生》。这些文章都在说"变化已经发生"，但很少有人把"变化具体是什么"拆清楚。

这个框架的作用是：把 2025 年那种"你问它答"的 AI，和 2026 年那种"你描述意图、Agent 自主拆解任务、组队干活、经验沉淀"的 AI，放在四个正交维度上对照。

## 四层结构

### 第一层：大脑变了（Model）

模型本身的质变：
- **编程能力跨台阶**：[[products/claude-opus-4-6]] 和 GPT-5.3 Codex 在 2026-02-05 同日发布，刷新多个权威编程基准
- **判断力与品味**（Matt Shumer 用词：judgment / taste）：Agent 自己决定该用什么工具、什么时候用、怎么组合
- **独立工作时长**：[[concepts/metr-time-horizon]] 显示"AI 能独立完成的专家级任务时长"每 4~7 个月翻一倍，2025 年 11 月已达约 5 小时
- **长上下文**：Opus 4.6、DeepSeek 都更新到 100 万 token，足以装下整个大型项目
- **AI 参与造自己**：GPT-5.3 Codex 是第一个参与自身创建过程的模型（OpenAI 技术文档承认），Anthropic "大部分代码"由 AI 写成（Amodei），反馈循环"逐月加速"

### 第二层：手脚长出来了（Tools & Context）

Agent 从对话框里走出来，获得操作外部世界的能力：
- **本地运行**：[[products/claude-code]] 等新一代 Agent 跑在用户本机，直接读本地文件（代码、文档、设计稿），上下文属于用户而非厂商，可自由切换底层模型
- **[[concepts/mcp]]（Model Context Protocol）**：即插即用的工具接入标准，Anthropic/OpenAI/Google 三家在 2025 年底联合推动
- **[[concepts/claude-code-skills]]（Skills）**：预定义能力模块，社区可共享，一个资深工程师的经验能被全世界 Agent 加载
- **记忆与身份**：Claude Code 的 `CLAUDE.md`（项目级） → [[concepts/openclaw]] 的 `SOUL.md`/`USER.md`/`MEMORY.md`（人级）
- **旧工具解锁**：ffmpeg、ImageMagick、curl、git、pandoc 等沉淀几十年的命令行工具，门槛被 Agent 抹平
- **GUI 自动化**：OpenClaw 等工具真的会点按钮、填表单，覆盖无 API 无 MCP 的软件
- **物理载体**：车（电动车 + 自动驾驶）可能先于人形机器人把 Agent 带入物理世界
- **多模态**：Nano Banana Pro、Seedance 2.0 等接入 Agent 体系，团队里可以有写代码的、做设计的、剪视频的

### 第三层：能组队了（Organization）

从"一个 Agent 干活"到"一群 Agent 协作"：
- **[[concepts/subagent]]**：主 Agent 派出子 Agent 做探索类子任务，用 token 消耗换上下文清洁（"搜索的本质是压缩"）
- **[[concepts/agent-teams]]**：Team Lead + 多个 Teammate，每个成员独立上下文窗口、独立工具集，并行工作互不干扰。Anthropic 做过 16 个 Opus 4.6 实例组队、从零写出 C 编译器的压力测试（2 万美元、2000 会话周期、10 万行代码）
- **[[concepts/a2a-protocol]]（Agent-to-Agent）**：Google 联合 50+ 企业推出的跨厂商 Agent 通信协议
- **Git Worktree 并行**：用"平行宇宙"方式同时试多个方案，然后选最好的，把试错从串行变并行
- **主动工作**：定时任务（如 OpenClaw 的 `HEARTBEAT.md`）让 Agent 从"你主动找它"变成"它主动盯着"

这一层的关键洞察：当第一层的独立时长从"几小时"变成"几天"甚至"几周"，再叠加 Agent Teams 的并行，度假回来可能整个产品原型已经做好了。

### 第四层：会进化了（Evolution）

解决"Agent 能不能越用越强"的问题：
- **[[products/evomap]] 与 [[concepts/gep-protocol]]**（基因组进化协议）：成功做法被打包成"基因胶囊"，其他 Agent 可继承
- **Skills 与 GEP Gene 的对比**：Skills 像员工手册（写死不变），Gene 像员工攒下的经验（随使用调整、能自修复、长期没用则淘汰）
- **跨领域迁移**：游戏策划的"命名隔离策略"可以被后端工程师的 Agent 匹配到用于解决变量冲突——解决方案来自完全不相关的领域
- **协议不是平台**：平台会被收购关停（OpenClaw 被 OpenAI 收购就是例子），但开放协议下经验归用户所有

## 四层叠乘效应

| 层 | 单独来看 | 叠加后的乘积 |
|---|---|---|
| 大脑 | 每个 Agent 产出质量接近人类专家 | × |
| 手脚 | 每个 Agent 覆盖好几个职能的工具 | × |
| 组织 | 多 Agent 并行、全天候运转 | × |
| 进化 | 经验沉淀、传递、跨领域迁移 | = 乘积 |

作者亲述：一个人一周做出大厂一个月的产品、GitHub 拿到 2000 Star。不是因为更聪明，是因为"模型够强所以质量不打折、工具够多所以不用找设计师和运维、组织够好所以多条线同时推不用开站会、经验能传承所以不用从零开始"。

## 未解决的问题

- **管理成本**：5 个 Agent 同时跑 = 5 份跨领域结果要验收，token 消耗容易失控。GitHub 前 CEO Thomas Dohmke 创办 Entire 公司就在做这个方向
- **安全与信任边界**：什么操作需要用户确认、什么可自动执行，行业还没想清楚
- **Agent 的经济身份**：没有银行账户、没有身份认证，收益归谁、责任归谁、Agent 之间怎么结算，基础设施还不存在

## 现实影响

- **公司会变小**：一个人 + Agent 覆盖以前六七个角色的活。OpenClaw 就是个例子——一个人的周末项目，3 个月拿了 20 万 Star 被 OpenAI 收购
- **教育跟不上**：现行教育训练"执行能力"，Agent 时代需要"判断能力"——两者培养方式完全不同
- **中间层最难受**：大厂白领、中层管理、普通知识工作者最易被替代，又来不及转型成"Agent 指挥官"
- **内容生产"能做"不值钱**：值钱的是"知道该做什么"——品味、判断力、独特视角
- **国家之间的比较优势**：从"人口素质"迁移到"能源效率"（廉价能源 → 廉价算力 → 廉价智能）

## 参考来源

- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（微信公众号，2026-02-25）
- Matt Shumer《Something Big Is Happening》
- Dario Amodei《The Adolescence of Technology》
- METR（AI 能力追踪机构）长期追踪的任务时长指标

## 关联页面

- [[concepts/mcp]]
- [[concepts/subagent]]
- [[concepts/agent-teams]]
- [[concepts/a2a-protocol]]
- [[concepts/gep-protocol]]
- [[concepts/metr-time-horizon]]
- [[concepts/openclaw]]
- [[concepts/claude-code-skills]]
- [[products/evomap]]
- [[patterns/claude-code-config-layers]]
