# 2025-2026 顶会大模型后训练论文整理

## Overview

这份清单聚焦 2025-2026 年顶会中与大模型后训练直接相关的论文，主要来源为 ICLR 2025、NeurIPS 2025、ICLR 2026 的官方 OpenReview 论文页。主题覆盖：

- SFT / instruction tuning / data-efficient fine-tuning
- RLHF / online RL / off-policy RL / RLVR / self-play RL
- DPO、SafeDPO、Token-level DPO、动态偏好优化等偏好优化范式
- reward model、generative verifier、process/reasoning reward
- reasoning model 的 post-training 数据配方、test-time/inference-aware training


## 论文清单

| # | 论文 | 顶会/年份 | PDF | 项目/代码 | 大概做法 |
|---|---|---:|---|---|---|
| 1 | Advantage Alignment Algorithms | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/1668aadc796a27dbd82ead44b99d16f2e3a43645.pdf) | [Paper](https://openreview.net/forum?id=QFO1asgas2) | 从多智能体/博弈视角提出 advantage alignment，把交互中有利于双方的动作 advantage 对齐，用更轻量的 opponent shaping 机制提升合作和稳健性。可作为 alignment/RLHF 中“偏好不只是标量奖励”的理论补充。 |
| 2 | Iterative Nash Policy Optimization: Aligning LLMs with General Preferences via No-Regret Learning | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/49e7914476dbafb4681bc4d500f07a951058447e.pdf) | [Paper](https://openreview.net/forum?id=Pujt3ADZgI) | 将 RLHF 放在一般偏好而非 Bradley-Terry 标量奖励假设下处理，把策略优化建模为两人博弈。INPO 让策略通过 no-regret self-play 逼近 Nash policy，直接用偏好数据优化。 |
| 3 | More RLHF, More Trust? On The Impact of Preference Alignment On Trustworthiness | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/b6841566cfe34141b1dd3f6aca52c81246dfe56c.pdf) | [Paper](https://openreview.net/forum?id=FpiCLJrSW8) | 系统分析 RLHF/偏好对齐对 trustworthiness 的影响，不只看 helpfulness，也看真实性、安全性、校准等维度。结论强调“更多 RLHF”不一定单调提升所有可信属性。 |
| 4 | Reasoning Elicitation in Language Models via Counterfactual Feedback | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/267beda691f61b38a9441477ebf61983f07aa736.pdf) | [Paper](https://openreview.net/forum?id=VVixJ9QavY) | 用 counterfactual feedback 诱导语言模型形成更强推理机制。先设计兼顾 factual/counterfactual 的指标，再用若干 fine-tuning 方法让模型在反事实问答中泛化更好。 |
| 5 | ReGenesis: LLMs can Grow into Reasoning Generalists via Self-Improvement | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/0f5acd1a57d199942a7ac8efc3dc19df441efaf2.pdf) | [Paper](https://openreview.net/forum?id=YUYJsHOf3c) | 让 LLM 自己从抽象推理指导生成具体 reasoning path，作为后训练数据，不依赖人工或更强教师模型。核心是“从抽象到具体”的自我合成轨迹，提升 OOD 推理泛化。 |
| 6 | Rethinking Reward Modeling in Preference-based Large Language Model Alignment | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/c86736447d5c66dec8140360ab743a130d9ff219.pdf) | [Paper](https://openreview.net/forum?id=rfdblE10qm) | 重新审视 preference-based alignment 中 reward model 的建模假设、训练目标和评估方式。重点讨论 reward model 是否真的学到偏好，以及它在 RLHF/DPO 风格后训练中的局限。 |
| 7 | Spread Preference Annotation: Direct Preference Judgment for Efficient LLM Alignment | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/d532e5072a02970b546a7e129fec61230042c66b.pdf) | [Paper](https://openreview.net/forum?id=BPgK5XW1Nb) | 改进偏好标注方式，不只做二选一 pairwise comparison，而是更直接、更高效地收集 preference judgment。目标是降低 alignment 数据标注成本并提升偏好信号质量。 |
| 8 | Training Language Models to Self-Correct via Reinforcement Learning | ICLR 2025 Oral | [OpenReview](https://openreview.net/pdf/933985f70410dda1d58d271d6f55f69812e8c962.pdf) | [Paper](https://openreview.net/forum?id=CjwERcAU7w) | 提出 SCoRe，多轮 online RL 训练模型在自己的错误分布上自我纠错。相比离线 SFT 纠错轨迹，RL 能避免分布错配和行为塌缩，提高数学和代码任务自纠错能力。 |
| 9 | Asynchronous RLHF: Faster and More Efficient Off-Policy RL for Language Models | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/d0759a26adbc702480d4dafff3b0bc31aa5c6240.pdf) | [Paper](https://openreview.net/forum?id=FhTAG591Ve) | 将 RLHF 的生成和学习解耦，异步生成新样本、同时用旧样本训练。研究 off-policy 程度对性能的影响，发现 online DPO 对离策略数据较稳健，可提升训练吞吐。 |
| 10 | Bootstrapping Language Models with DPO Implicit Rewards | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/ac26d610b7c8257221b73b41bd7121613e86782b.pdf) | [GitHub](https://github.com/sail-sg/dice) | DPO 训练后隐含一个 reward model。DICE 利用当前模型的 DPO implicit reward 自动构造新的偏好数据，再迭代 DPO，实现不依赖外部反馈的自举式 self-alignment。 |
| 11 | BOND: Aligning LLMs with Best-of-N Distillation | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/a95974c6ddbf80c3786547203e88d56fba3e34a8.pdf) | [Paper](https://openreview.net/forum?id=0tAXMiSufG) | Best-of-N 推理效果强但推理贵。BOND 将 Best-of-N 选择出来的分布蒸馏进策略，用 Jeffreys divergence 匹配 BoN 分布，使模型在单次生成时接近 BoN 效果。 |
| 12 | DELIFT: Data Efficient Language model Instruction Fine-Tuning | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/a90372465680c53ab839a4a33b8e45e77de9f374.pdf) | [Paper](https://openreview.net/forum?id=Fty0wTcemV) | 面向 instruction tuning、task fine-tuning、continual fine-tuning 三阶段的数据选择。用 pairwise utility 衡量样本对其他样本的帮助，再用子模函数选子集，减少冗余 SFT 数据。 |
| 13 | Exploratory Preference Optimization: Harnessing Implicit Q*-Approximation for Sample-Efficient RLHF | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/3a72320613fda3d2449f2ac0a8578489853f4206.pdf) | [Paper](https://openreview.net/forum?id=QYigQ6gXNw) | XPO 在 online DPO 目标中加入探索 bonus，鼓励模型走出初始策略覆盖范围，从而更高效地收集有信息量的偏好反馈。理论上把 DPO 与 KL-regularized MDP/Q* 近似联系起来。 |
| 14 | Generative Verifiers: Reward Modeling as Next-Token Prediction | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/b1d84910d45ea689f1c089639edb67b49797c70c.pdf) | [Paper](https://openreview.net/forum?id=Ccwp4tFEtE) | 把 verifier/reward model 从判别式打分器改成生成式 next-token prediction。GenRM 能输出验证推理、利用 CoT 和 majority voting，在数学/算法题 Best-of-N 选择中优于传统 reward model。 |
| 15 | Inference-Aware Fine-Tuning for Best-of-N Sampling in Large Language Models | ICLR 2025 Poster | [OpenReview](https://openreview.net/pdf/3274f331a8e9f86bc72c72c6562f2f607d1b5639.pdf) | [Paper](https://openreview.net/forum?id=77gQUdQhE7) | 训练时直接考虑 Best-of-N 推理策略，而不是只优化单样本生成。提出 BoN-aware imitation/RL fine-tuning，让模型学会生成“可被 verifier 选中”的多样候选。 |
| 16 | Absolute Zero: Reinforced Self-play Reasoning with Zero Data | NeurIPS 2025 Spotlight | [OpenReview](https://openreview.net/pdf/fed932448b66316fd6823fb9a3103e478989bfd5.pdf) | [Paper](https://openreview.net/forum?id=neZSGqhxDa) | 提出 Absolute Zero Reasoner：模型自己提出代码/数学推理任务，并用代码执行器验证任务与答案，以 verifiable reward 做 self-play RL。特点是零外部训练数据。 |
| 17 | DAPO: Improving Multi-Step Reasoning Abilities of Large Language Models with Direct Advantage-Based Policy Optimization | NeurIPS 2025 Spotlight | [OpenReview](https://openreview.net/pdf/be1c0b5313f1e34cb0858d1d966b8d6e19d6afd6.pdf) | [Paper](https://openreview.net/forum?id=77eEDRhPkQ) | DAPO 是 step-level offline RL 方法，用 critic 预测每一步推理正确性，提供比 outcome reward 更密集的 advantage 信号。Actor/Critic 分开训练，避免 PPO/AC 类方法的不稳定。 |
| 18 | Less is More: Improving LLM Alignment via Preference Data Selection | NeurIPS 2025 Spotlight | [OpenReview](https://openreview.net/pdf/25b5723d978db683d8fcf5771f228fa4d71571b7.pdf) | [Paper](https://openreview.net/forum?id=R2ZJSjLDJC) | 不是改 DPO loss，而是做偏好数据选择。用外部 reward margin 和 DPO implicit reward margin 选高质量偏好样本，只用少量 UltraFeedback 数据就提升 AlpacaEval 等表现。 |
| 19 | InfiFPO: Implicit Model Fusion via Preference Optimization in Large Language Models | NeurIPS 2025 Spotlight | [OpenReview](https://openreview.net/pdf/f4520d671b2e16d30997ffc361f5a1dfd6a9feeb.pdf) | [Paper](https://openreview.net/forum?id=ZwBtDbuzjY) | 把模型融合引入 preference optimization。用多个源模型的序列概率构造融合 reference model，再做 DPO 风格偏好优化，让 pivot model 同时吸收源模型能力和人类偏好。 |
| 20 | Checklists Are Better Than Reward Models For Aligning Language Models | NeurIPS 2025 Spotlight | [OpenReview](https://openreview.net/pdf/490597cf8f353f8b01b8474e2f98c045eba8f5f4.pdf) | [Paper](https://openreview.net/forum?id=RPRqKhjrr6) | 用 checklist 替代或增强 reward model：把复杂偏好拆成可检查条件，让 alignment 信号更可解释、可控，也减少 reward model 黑箱误判对训练的影响。 |
| 21 | The Art of Scaling Reinforcement Learning Compute for LLMs | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/c8cd1de9eac796cc9307b68a53ccfc3978f74f3f.pdf) | [Paper](https://openreview.net/forum?id=FMjeC9Msws) | 大规模系统研究 LLM RL compute scaling，拟合 RL compute-performance 曲线，分析 loss aggregation、normalization、curriculum、off-policy 等设计。提出可预测扩展的 ScaleRL 配方。 |
| 22 | TROLL: Trust Regions Improve Reinforcement Learning for Large Language Models | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/cbc7c9421e3d6ee2d6f2e1db46a78c90a79d2dbb.pdf) | [Paper](https://openreview.net/forum?id=X9D5MVpPJ9) | 替换 PPO-style clipping，使用离散可微 trust region projection，在重要 token logits 上施加 token-level KL 约束，使 LLM RL 更新更稳定、更快。 |
| 23 | SafeDPO: A Simple Approach to Direct Preference Optimization with Enhanced Safety | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/316f85a1cf0c2e7c193e15109dfe60548d2e888e.pdf) | [Paper](https://openreview.net/forum?id=PJdw4VBsXD) | 在 DPO 中加入安全对齐目标，只引入一个额外超参数，不需要单独训练 reward/cost model，也不需要 fine-tuning 期间采样。目标是在保持 helpfulness 的同时增强安全性。 |
| 24 | Token-Importance Guided Direct Preference Optimization | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/ee7ba5337c7269bc77a2b118b14ca9e61057952b.pdf) | [Paper](https://openreview.net/forum?id=cMEnMVvMw9) | 认为 DPO 忽略不同 token 的重要性。TI-DPO 用梯度估计 token importance，并用 triple loss 同时靠近 preferred response、远离 rejected response，提高稳定性和生成多样性。 |
| 25 | Semi-Supervised Preference Optimization with Limited Feedback | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/f60e4bd40fa5a1c86fac5a5e08466ec66dbd9c76.pdf) | [Paper](https://openreview.net/forum?id=ghwxbTx7do) | SSPO 使用少量成对偏好标签和大量未配对响应。理论上证明存在 reward threshold 可区分 winner/loser，再伪标注未配对数据，降低偏好数据采集成本。 |
| 26 | OpenThoughts: Data Recipes for Reasoning Models | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/968ae4b700f3ec12372a803e39d5510d0ab3cfd7.pdf) | [Project](https://openthoughts.ai) | 开源 reasoning model 后训练数据配方。通过 1000+ 控制实验优化数据生成流水线，构造 OpenThoughts 系列数据和 OpenThinker 模型，研究推理 SFT 数据如何影响模型能力。 |
| 27 | LoongRL: Reinforcement Learning for Advanced Reasoning over Long Contexts | ICLR 2026 Oral | [OpenReview](https://openreview.net/pdf/0a0c0c8ab93ec3714654ed7bda540223e1934750.pdf) | [Paper](https://openreview.net/forum?id=o29E01Q6bv) | 针对长上下文推理做 RL。KeyChain 把短 multi-hop QA 合成为长上下文任务，模型必须计划、检索、推理、复查；在 16K 训练后泛化到 128K 长上下文。 |
| 28 | Uni-DPO: A Unified Paradigm for Dynamic Preference Optimization of LLMs | ICLR 2026 Poster | [OpenReview](https://openreview.net/pdf/e2925b64be08b5c9931e8bcb65dc0e43197b7a3d.pdf) | [Paper](https://openreview.net/forum?id=G7DBGlgjjp) | 提出统一的动态偏好优化框架，关注偏好优化过程中数据、参考模型或优化信号随训练阶段变化的问题。可理解为对静态 DPO 的动态化扩展。 |

## 按训练范式归类

### SFT / 数据配方

DELIFT、OpenThoughts、ReGenesis 属于 SFT 和 reasoning data recipe 方向。DELIFT 关注怎么少用数据做 instruction tuning；OpenThoughts 系统研究推理数据如何生成和筛选；ReGenesis 则让模型自己从抽象推理原则合成训练轨迹。

### DPO / 偏好优化

DICE、XPO、Less is More、InfiFPO、SafeDPO、TI-DPO、SSPO、Uni-DPO 都在 DPO 或 preference optimization 上扩展。它们分别从自举隐式 reward、探索、数据选择、模型融合、安全约束、token 重要性、半监督偏好和动态偏好优化等角度改进标准 DPO。

### RLHF / RLVR / 推理 RL

SCoRe、Asynchronous RLHF、Absolute Zero、DAPO、ScaleRL、TROLL、LoongRL 属于 RL 后训练主线。它们关注自我纠错、异步离策略 RLHF、零数据 self-play、step-level advantage、RL compute scaling、trust region、长上下文 RL 等问题。

### Reward Model / Verifier

Rethinking Reward Modeling、GenRM、Checklists Are Better Than Reward Models、Spread Preference Annotation 主要围绕 reward/preference 信号本身。趋势是从黑箱 scalar reward，走向更可解释、更细粒度、更贴近推理过程的监督信号。

## 阅读建议

如果要快速建立脉络：

1. 先读 DPO 原线扩展：DICE、XPO、Less is More、SafeDPO、TI-DPO。
2. 再读 RL 推理：SCoRe、Absolute Zero、DAPO、TROLL、ScaleRL。
3. 看数据配方：DELIFT、OpenThoughts、ReGenesis。
4. 看 reward/verifier：Rethinking Reward Modeling、GenRM、Checklists。
5. 最后看前沿问题：INPO、SSPO、LoongRL、Uni-DPO。

