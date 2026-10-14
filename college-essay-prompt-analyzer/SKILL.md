---
name: "college-essay-prompt-analyzer"
description: "Use when the user sends a college application essay prompt (Common App, supplemental, Why Us, short answer) to analyze it, find writing directions, or generate a brainstorming questionnaire."
---

# 大学文书题目分析 + 问卷生成

本 skill 从一套真实的文书辅导材料（Common App Prompt 5 问卷、USC Required「Why USC / 专业」问卷、USC Optional「分歧」问卷，以及一份 Common App 五段式 outline）中提炼而来。它规定了三件事：

1. 收到文书题目后**第一步必须做什么**（让用户选择是否生成问卷）；
2. **拆解和分析题目的思考流程**（不论是否生成问卷都要走）；
3. **问卷的提问流程**（用户需要问卷时使用；只输出问卷内容，不带格式和填写说明）。

---

## 第 0 步：收到题目后，先让用户选择

用户发来文书题目（可能附带学校、字数、个人素材、草稿或其他要求）后，**先不要直接开始分析或写问卷**，先问一个问题：

> 是否需要为这道题生成一份素材收集问卷（Questionnaire）？
> - **需要问卷**：我会先拆解题目，然后直接给出问卷内容（6 个部分，每部分有 Purpose 和问题），你回答后可以用来写 outline 和正文。
> - **不需要问卷**：我直接拆解题目，给你题目分析 + 2–3 个可能的写作方向，并处理你提到的其他需求。

- 有 AskUserQuestion 工具时用它提问（两个选项 + 用户可自填），没有就用一句话文字提问。
- 如果用户在同一条消息里已经明确说了「要问卷」或「不要问卷 / 直接分析」，就不用再问，直接按对应路线走。
- 如果同一条消息里有多道题，一次问清楚：哪些题要问卷、哪些只要分析。
- 用户用中文就用中文回复；问卷本身默认用英文（与原模板一致），用户要求中文版时再改。

用户回答后：
- **不需要问卷** → 走「路线 A：题目分析」。
- **需要问卷** → 先在内部完成「路线 A」的第 1–3 步（拆题是出题的前提，但不输出），再走「路线 B：生成问卷」，只输出问卷内容本身。

---

## 核实原则（每条路线都适用）

- **题目每年会变**：如果用户只说了「USC 的那道题」「Common App 第 5 题」而没贴原文，用联网工具查当年（当前申请季）的原题和字数，不要凭记忆写。查不到就请用户贴原文。
- **学校资源一律核实**：凡是写进分析或问卷里的具体课程编号、教授及其研究、项目、中心、学位路径（如 progressive degree、minor）、录取或认证要求，都要先用网络搜索 / 官网核实存在且是当前信息。核实不了的，要么不写，要么明确标注「待核实」。
- **招生官对该题的公开解读**（学校官方博客、招生说明）如果能查到，优先引用，用来判断题目重心（例如「重点在互动与成长，而不是冲突本身」）。
- 不替用户编造经历、细节、数字。素材缺失时指出缺什么，而不是补出来。

---

## 路线 A：题目分析（思考流程）

按以下顺序思考，并把结果组织成给用户的分析。

### A1. 识别题目元信息

| 项目 | 需要确认的内容 |
|---|---|
| 来源 | Common App 主文书 / 某校补充文书 / 奖学金 / 荣誉项目 |
| 必答还是选答 | Required / Optional（选答题也要判断「写了是否加分、不写是否吃亏」） |
| 字数上限 | 决定能讲几个场景、篇幅怎么分配 |
| 申请的专业 / 学院 | 第一、第二志愿是什么，题目是否要求同时回应 |
| 同校其他题目 | 与本校其他文书、主文书的分工，避免素材重复 |

### A2. 逐句拆解题目

把题目拆成下面几类成分，逐一标注：

1. **引语 / 背景语**：如学校价值观引语（「value honest, open communication and robust debate」）。这不是装饰，它告诉你学校想看到的**品质**——文章要回应引语的精神，而不只是字面任务。
2. **核心动作动词**：Describe / Discuss / Explain / Reflect——决定是以叙事为主还是以论述为主。
3. **必答子问题**：题目末尾的追问，如「Did you change your mind or reach common ground?」「Why … at USC specifically?」。每一个都必须在文中有明确回答，漏一个就是跑题。
4. **选择性成分**：「Please feel free to address your first- and second-choice majors」「yourself **or** others」。判断用户的情况适不适合回应它；适合的话回应它往往能拉开差距。
5. **限定词**：逐个圈出并解释其约束，例如
   - 「someone you know」→ 必须是真实认识的人，不是网上辩论或公众人物；
   - 「something important to you」→ 议题要和本人价值观相关，不能是鸡毛蒜皮；
   - 「specifically」→ 内容必须换一所学校就不成立；
   - 「a period of personal growth」→ 成长要有时间跨度和过程，不是一瞬间顿悟；
   - 「accomplishment, event, or realization」→ 触发点可以是三类中任何一类。
6. **隐含评估维度**：招生官读这道题时实际在打分的东西（自我反思、责任感、开放性、学术好奇心的证据、与学校资源的匹配度、对社区的贡献……）。
7. **篇幅分配**：按字数给出建议比例。例如 250 字的「分歧」题：冲突场景 ≤ 30%，倾听 / 互动 / 改变 ≥ 60%，收尾 ≤ 10%；650 字的成长题：触发事件约 20%，反思与根源约 30%，行为改变的证据约 30%，新的理解与延续约 20%。

### A3. 判断题型，套用对应的叙事主线

| 题型 | 叙事主线（起 → 终） | 最容易犯的错 |
|---|---|---|
| **成长 / 顿悟**（如 Common App 5） | 具体的触发时刻 → 当下的反应与冲突 → 认识到更深层的模式或根源 → 用具体行为证明的改变 → 对自己或他人的新理解 → 承认成长仍在继续 | 只「声称」改变而没有行为证据；教训过于简单（「我学会了说不」）；写成受害者叙事 |
| **挑战 / 挫折** | 困境 → 当时的应对 → 从中学到什么 → 后来如何应用 | 渲染苦难多于展示应对 |
| **身份 / 背景 / 社区** | 具体的身份片段 → 它如何塑造视角 → 带来的张力 → 我会给大学社区带去什么 | 泛泛的文化标签；把一种文化写成比另一种更好 |
| **价值观 / 分歧 / 多元观点**（如 USC Optional） | 重要议题 + 具体的人 → 分歧场景 → 倾听并理解对方的理由 → 寻找共同点或保留分歧 → 观点或沟通方式的变化 → 将来在课堂里如何对话 | 写成「我赢了辩论」；对方被写成稻草人；冲突写太多，互动和改变写太少 |
| **学术兴趣 / Why Major / Why Us**（如 USC Required） | 兴趣起点（具体时刻）→ 已做过的事作为证据 → 现在仍在追问的具体问题 → 每个问题对应一项本校资源（课程 / 教授 / 项目 / 研究机会）→ 本校之后的路径 | 罗列排名、天气、地理位置等通用理由；资源和个人问题之间没有连接；第一、第二志愿各说各的 |
| **课外活动 / 贡献** | 角色 → 一个具体的问题或时刻 → 我做了什么 → 产生了什么变化 → 这说明我是什么样的人 | 写成简历的扩写 |
| **短答 / 清单 / 趣味题** | 一个鲜明、具体、只有本人会给出的答案 | 用安全但无记忆点的答案 |

题型不在表里时，按同样思路推出它的起点、转折、终点和失分点。

### A4. 盘点用户已提供的素材（如有）

- 把用户给的经历、背景、草稿按「能支撑题目的哪一部分」归类。
- 标出**最强的素材**：有具体场景、有对话或动作、能显示变化的。
- 标出**缺口**：例如有触发事件但没有改变后的行为证据；有兴趣但没有已做过的事；有学校资源但没和个人问题连起来。
- 标出**风险**：敏感经历（如健康或家庭问题）只用于说明严重程度，简短直接带过，不要成为全文焦点；需要承认自身责任的地方不要回避，否则文章会变成「别人伤害了我」；避免同一素材在主文书和补充文书里重复使用。

### A5. 给出 2–3 个写作方向

每个方向包含：

- **一句话核心洞见**：这篇文章最终想让读者明白的一件事。
- **故事主线**：按 A3 的结构列出 4–6 个节拍。
- **为什么贴题**：对应 A2 中的哪些必答子问题和评估维度。
- **需要的素材 / 还缺什么**。
- **风险与规避方法**。
- （可选）**一个可以贯穿全文的意象或物件**——只在它真实发生过、并且确实能象征变化时才推荐。

方向之间要有真正的差异（不同的事件、不同的切入角度、或不同的核心洞见），而不是同一个故事换个说法。

### A6. 处理用户的其他需求

用户可能同时要求：评估已有草稿、比较几个选题、规划多篇文书的分工、写 outline 等。分析完题目后逐项回应。需要写 outline 时，使用下面「附录：Outline 格式」。

### 路线 A 的输出格式

用聊天回复呈现（用户要存档或分享时，再按会话规则做成文档）：

1. **题目拆解**：A1 + A2 的要点（逐句标注、必答问题清单、篇幅分配）
2. **题型与主线**：A3
3. **素材盘点**：A4（用户没给素材就省略，改为列出「你需要准备的素材」）
4. **可能的写作方向**：A5 的 2–3 个方向
5. **你的其他需求**：A6
6. 末尾一句可选的下一步，例如「需要的话我可以把这道题做成问卷」或「选定方向后我可以写 outline」

---

## 路线 B：生成问卷

### B1. 问卷只输出纯内容

问卷**只包含内容本身**，直接在聊天回复里输出，**不要**加：
- 填写说明 / 作答规则（语言、语气、字数、「ALL ENTRIES MUST BE IN RED」之类）
- 文件命名、保存格式、提交方式说明
- `[Enter Text Here]` 之类的填写占位符
- 问卷前后的题目分析摘要、开场白或结束语
- 默认不生成 Word / PDF 等文件（用户明确要求文件时再做）

问卷内容的结构（顺序固定）：

```
Prompt: [题目原文] ([字数上限])

Section 1: [部分标题]
Purpose: [1–3 句，说明这一部分收集什么、为什么对这道题重要]
• [问题]
• [问题]
…

Section 2: …
…
Section 6: …
```

每个 Section = 标题 + Purpose + 5–7 个问题。用户要求去掉 Purpose 或换语言时照做。

### B2. 六个 Section 的推进逻辑

问卷的六个部分遵循同一条推进线：**选材 → 场景 → 理解 / 反思 → 行动与证据 → 意义与关联 → 声音与收尾**。不同题型的映射如下：

| # | 通用功能 | 成长题（CA5 型） | 分歧题 | Why Us / 专业题 |
|---|---|---|---|---|
| 1 | 选材：找到最有分量的那个故事或兴趣 | Identifying the Catalyst Moment | Identifying a Meaningful Disagreement | Academic Interests and Intellectual Curiosity |
| 2 | 场景与背景：把抽象经历变成具体画面 | Background and Cultural Context | The Moment of Disagreement | Evidence of Your Academic Engagement |
| 3 | 理解与反思：当时怎么想，后来怎么理解 | Response and Reflection | Listening and Understanding the Other Perspective | First- and Second-Choice Majors |
| 4 | 行动与证据：用具体行为证明 | Evidence of Growth | Your Response and the Search for Common Ground | Why [School] Specifically? |
| 5 | 意义与关联：连接价值观、目标、大学 | Meaning and Relevance | Change, Growth, and New Understanding | How You Would Pursue Your Interests at [School] |
| 6 | 声音、框架、未来 | Narrative Voice and Final Framing | Applying the Lesson to Future Dialogue | Future Direction, Values, and Contribution |

遇到其他题型时，按「通用功能」那一列自行命名六个 Section，名称要贴合题目用语。

### B3. 出题规则（从样本问卷中提炼）

**Purpose 段落怎么写**
- 一到三句，说明这一部分要收集什么、为什么对这道题重要。
- 尽量回扣题目原文或学校引语（「USC's prompt emphasizes open communication and robust debate, making the student's behavior during the disagreement especially important」）。
- 能查到该题的当前官方解读时，可以在 Purpose 中点出重心（「current guidance … emphasizes engagement, change, and growth rather than … the conflict」）。

**问题怎么问**
1. **先发散再收敛**：第一个问题让学生列 2–3 个候选（「Think of two or three times when…」），第二个问题让他挑出最重要的那个并说明原因。
2. **要求还原现场**：何时、何地、什么触发、对方原话是什么、你说了什么、做了什么（「Reconstruct their point as accurately as you can」）。
3. **给出选项降低难度**：情绪、反应、经历类问题附上候选词（「surprised, frustrated, defensive, curious, confused…」「a class, experience, person, problem, book, project…」）。
4. **分支追问**：成对出现的「If yes … / If not …」，确保无论结果如何都有可写的内容（「Did you change your mind? … If you did not fundamentally change your mind, did your position become more nuanced?」）。
5. **区分「声称」与「证据」**：至少一个问题要求「something you said or did differently」这样的具体例子。
6. **逼出深层原因**：追问「为什么这件事对你重要」「哪些经历、价值观、家庭、文化塑造了这个立场」。
7. **呈现对方 / 他人视角**：在涉及他人的题目里，问对方的理由、你最难反驳的那一点、你误解了什么。
8. **前后对比**：「Before this experience, what did you think …? How would you define … now?」
9. **学校题必须做研究**：要求学生自己查 2–3 门具体课程、教授、项目，并说明「每一项和我的哪个问题对应」；明确排除通用理由（「rather than generic qualities such as reputation, rankings, campus life, weather, or location」）。
10. **可迁移性测试**：用填空句检验特异性（「USC is the right place for me to explore ___ because ___. Try to make your answer so specific … that it could not simply be transferred to another university.」）。
11. **填空式收尾**：最后一部分用一句填空提炼核心洞见（「This disagreement taught me that listening to someone who disagrees with me does not require me to ___; instead, it requires me to ___.」）。
12. **叙事声音问题**（个人陈述类在第 6 部分固定出现）：
    - 这是关于 overcoming、discovering 还是 maturing 的故事？
    - 你想要什么语气？
    - 有没有一个隐喻、象征或物件能代表你的成长？
    - 你希望读者最后记住哪一句话或哪个想法？
    - 有没有你害怕写、但觉得可能应该写的内容？
13. **面向大学的展望**：至少一个问题把经历连到「你在大学课堂 / 社区里会怎样做」。
14. **双专业题专门追问**：为什么选第一志愿而不是相邻专业；两个志愿之间怎么连接；有没有一个主题能把它们串起来；在学校里怎么跨学院组合（minor、跨院课程、本硕连读）。

**数量与措辞**
- 每部分 5–7 题，全卷约 30–40 题；250 字的短补充文书也保持 6 个部分，但每题更聚焦。
- 每题一个焦点，可以带一句补充说明或例子，但不要把三个问题塞进一题。
- 各部分之间不重复提问；后面的问题要求「新的细节或例子」。
- 用简单直接的英文，不用术语和花哨表达——问卷本身就在示范它要求学生做到的写法。
- 如果用户已经提供了部分素材，可以把问题个性化（点名他提过的经历来追问细节），但不要替他作答。

---

## 附录：Outline 格式（用户填完问卷或要求写大纲时使用）

```
[Student Name]
Initial Outline
[Common App – Prompt 0X (主题名) | School – Required/Optional Supplement]

Prompt: [原题] (Maximum N words)

Paragraph 1: [段落标题，概括这一段的功能]
Topic Sentence:
  [一句完整的主题句，用斜体]
Supporting Ideas:
  • [具体细节 / 事件 / 对话 / 证据，3–6 条]

Paragraph 2: …（个人陈述一般 4–5 段；250 字补充文书一般 2–3 段）

Strength of Outline Evaluation
说明这份 outline 为什么契合这道题，3–5 条，每条加粗一句结论 + 一段解释，例如：
• 以具体事件开篇，而不是泛泛地谈成长
• 结构符合 [题型主线]
• 洞见有层次，不是简单的教训
• 用具体的行为改变证明成长，而不是只声称改变
• 结尾的新理解有分量，并承认成长仍在继续
最后一句总结：这份 outline 满足了招生官对该题最看重的哪些品质。
```

写 outline 时：所有细节都来自用户的问卷回答或用户的陈述，不编造；用户在问卷中说「不想当成重点」的内容在 outline 里也要压缩处理；人称代词与用户本人保持一致。
