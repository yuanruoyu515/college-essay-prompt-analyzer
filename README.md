# College Essay Prompt Analyzer · 大学文书题目分析器

**中文** | [English](#english)

一个帮助 AI 拆解美国大学申请文书题目、给出写作方向、并生成素材收集问卷的 Skill。可以配合 **Claude** 和 **ChatGPT** 使用。

An AI skill that breaks down U.S. college application essay prompts, suggests writing directions, and generates brainstorming questionnaires. Works with **Claude** and **ChatGPT**.

---

## 中文

### 它能做什么

把一道文书题目（Common App 主文书、学校补充文书、Why Us、Why Major、短答题等）发给 AI，它会先问你：**要不要生成问卷？**

| 你的选择 | AI 会给你 |
|---|---|
| **需要问卷** | 一份分 6 个部分的素材收集问卷。每部分有一段 Purpose 说明和 5–7 个问题，只输出问卷内容本身，没有填写说明或格式要求。你回答完就可以拿去写 outline 和正文。 |
| **不需要问卷** | 题目拆解 + 题型判断 + 素材盘点 + 2–3 个真正不同的写作方向，并回应你提出的其他需求（评估草稿、比较选题、写 outline 等）。 |

### 思考流程

不论选哪一条路线，AI 都会先按同一套流程拆题：

1. **识别题目信息**：来源、必答还是选答、字数、申请的专业、与其他文书的分工。
2. **逐句拆解**：学校引语、核心动词、必答子问题、可选成分、限定词（如 *someone you know*、*specifically*）、招生官实际在看的品质、各部分篇幅分配。
3. **判断题型**：成长 / 挑战 / 身份 / 分歧 / Why Us 与专业 / 课外活动 / 短答，套用对应的故事主线，并指出该题型最常见的失分点。
4. **盘点素材**：哪些素材最强、还缺什么、有什么风险。
5. **给出写作方向**：每个方向包含核心洞见、故事主线、为什么贴题、所需素材和风险。

问卷的六个部分遵循同一条推进线：**选材 → 场景 → 理解与反思 → 行动与证据 → 意义与关联 → 声音与收尾**。出题规则包括：先列候选再挑一个、要求还原当时的对话和动作、用 "If yes / If not" 分支追问、要求用具体例子证明改变、用填空句检验内容是否换一所学校就不成立等。

Skill 还要求 AI **核实**题目原文、课程编号、教授、项目等学校信息，查不到的不写或标注「待核实」，并且**不替学生编造经历**。

### 文件结构

```
college-essay-prompt-analyzer/
├── college-essay-prompt-analyzer/
│   └── SKILL.md                  # Skill 本体（Claude 与 ChatGPT 通用）
├── chatgpt/
│   └── project-instructions.md   # 在 ChatGPT Project 中使用时粘贴的简短指令
├── examples/
│   └── usage.md                  # 使用示例
├── LICENSE
└── README.md
```

### 在 Claude 中使用

**Claude 网页版 / 桌面版 / 手机 App（claude.ai）**
需要 Pro、Max、Team 或 Enterprise 账户，并开启「Code execution and file creation」。
1. 到本仓库的 [Releases](../../releases) 下载 `college-essay-prompt-analyzer.zip`（或自己把 `college-essay-prompt-analyzer/` 文件夹压缩成 ZIP）。
2. 打开 **Settings → Capabilities**，在 **Skills** 区域点 **Upload skill**，选择这个 ZIP。
3. 在对话里直接发文书题目即可，Claude 会自动调用这个 Skill。

**Claude Code**
```bash
git clone https://github.com/yuanruoyu515/college-essay-prompt-analyzer.git
mkdir -p ~/.claude/skills
cp -r college-essay-prompt-analyzer/college-essay-prompt-analyzer ~/.claude/skills/
```
个人 Skill 放在 `~/.claude/skills/<skill-name>/SKILL.md`；只想在某个项目里用的话，放到该项目的 `.claude/skills/` 下。

**没有 Skills 功能的 Claude 账户**
新建一个 Project，把 `SKILL.md` 上传到 Project 知识库，再把 [`chatgpt/project-instructions.md`](chatgpt/project-instructions.md) 里的指令粘贴到 Project instructions（这段指令同样适用于 Claude）。

### 在 ChatGPT 中使用

**方式一：ChatGPT Skills（工作区账户）**
ChatGPT Skills 采用与 Claude 相同的 Agent Skills 格式（`SKILL.md`）。截至 2026 年 10 月，Skills 面向 Business、Enterprise、Edu 等工作区账户开放，可能需要管理员先在工作区设置中启用。在侧边栏的 Skills 页面上传本仓库的 Skill 文件即可。

**方式二：ChatGPT Projects（所有支持 Projects 的账户，包括个人账户）**
1. 新建一个 Project。
2. 在 Project 的文件中上传 `college-essay-prompt-analyzer/SKILL.md`。
3. 打开 **••• → Project settings**，把 [`chatgpt/project-instructions.md`](chatgpt/project-instructions.md) 的内容粘贴到 Instructions。
4. 在这个 Project 里发文书题目。

**方式三：单次对话**
在任意对话里上传 `SKILL.md`，然后说：「请严格按照这个文件里的流程处理我接下来发的文书题目。」再发题目。

> 注：OpenAI 已宣布计划停用自定义 GPT（Custom GPTs），且个人账户目前无法新建 GPT，所以这里不推荐用 GPT 的方式。

### 注意事项

- 这个 Skill 帮你**思考和收集素材**，不替你写文书，也不会编造经历。最终的文书应该是你自己的故事和文字。
- 各校题目每年可能变化，请以学校官网和 Common App 的当年原题为准。
- 各平台的功能和套餐范围可能变化，以 [Claude 帮助中心](https://support.claude.com/en/articles/12512180-using-skills-in-claude) 和 [OpenAI 帮助中心](https://help.openai.com) 的最新说明为准。

### 许可证

[MIT](LICENSE) © 2026 Ruoyu Yuan

---

<a id="english"></a>

## English

### What it does

Send a college essay prompt (Common App personal statement, school supplements, Why Us, Why Major, short answers, and more) to the AI. It first asks you one thing: **do you want a questionnaire?**

| Your choice | What the AI gives you |
|---|---|
| **Yes, questionnaire** | A six-section brainstorming questionnaire. Each section has a short Purpose note and 5–7 questions. Only the questionnaire content is output, with no filling instructions or formatting rules. Your answers become the raw material for an outline and a draft. |
| **No questionnaire** | A prompt breakdown, the prompt type, a review of any material you shared, 2–3 genuinely different writing directions, and responses to anything else you asked for (draft feedback, topic comparison, an outline, and so on). |

### How it thinks

Both paths start with the same analysis:

1. **Prompt metadata**: source, required or optional, word limit, intended major, and how it fits with your other essays.
2. **Sentence-by-sentence breakdown**: the school's quoted values, the core verb, required sub-questions, optional parts, qualifiers (such as *someone you know* or *specifically*), what admissions readers are actually evaluating, and a suggested word budget.
3. **Prompt type**: growth, challenge, identity, disagreement, Why Us / Why Major, activity, or short answer, each with its own story arc and most common mistakes.
4. **Material review**: your strongest material, what is missing, and what is risky.
5. **Writing directions**: each with a core insight, story beats, why it fits the prompt, the material it needs, and its risks.

The six questionnaire sections follow one progression: **choosing the story → the scene → understanding and reflection → actions and evidence → meaning and connections → voice and ending**. The question-writing rules include listing several candidates before choosing one, reconstructing what was actually said and done, "If yes / If not" follow-ups, asking for concrete evidence of change, and a fill-in-the-blank test that checks whether a "Why Us" answer would still work for a different school.

The skill also tells the AI to **verify** prompt wording and school details (courses, professors, programs) and to leave out or flag anything it can't confirm. It **never invents experiences** for the student.

### Repository layout

```
college-essay-prompt-analyzer/
├── college-essay-prompt-analyzer/
│   └── SKILL.md                  # The skill itself (works with Claude and ChatGPT)
├── chatgpt/
│   └── project-instructions.md   # Short instructions to paste into a ChatGPT Project
├── examples/
│   └── usage.md                  # Usage examples
├── LICENSE
└── README.md
```

The skill instructions are written in Simplified Chinese. The AI replies in the language you use, and questionnaires are written in English by default.

### Using it with Claude

**Claude on web, desktop, and mobile (claude.ai)**
Requires a Pro, Max, Team, or Enterprise plan with "Code execution and file creation" turned on.
1. Download `college-essay-prompt-analyzer.zip` from this repo's [Releases](../../releases), or zip the `college-essay-prompt-analyzer/` folder yourself.
2. Open **Settings → Capabilities**, go to **Skills**, click **Upload skill**, and choose the ZIP.
3. Send an essay prompt in any chat and Claude will use the skill.

**Claude Code**
```bash
git clone https://github.com/yuanruoyu515/college-essay-prompt-analyzer.git
mkdir -p ~/.claude/skills
cp -r college-essay-prompt-analyzer/college-essay-prompt-analyzer ~/.claude/skills/
```
Personal skills live at `~/.claude/skills/<skill-name>/SKILL.md`. To use it in one project only, put it under that project's `.claude/skills/` folder.

**Claude plans without Skills**
Create a Project, add `SKILL.md` to the project knowledge, and paste the text from [`chatgpt/project-instructions.md`](chatgpt/project-instructions.md) into the project instructions. That text works for Claude too.

### Using it with ChatGPT

**Option 1: ChatGPT Skills (workspace plans)**
ChatGPT Skills use the same Agent Skills format (`SKILL.md`) as Claude. As of October 2026, Skills are available to workspace plans such as Business, Enterprise, and Edu, and an admin may need to turn them on first. Upload the skill from the Skills page in the sidebar.

**Option 2: ChatGPT Projects (any plan with Projects, including personal plans)**
1. Create a new Project.
2. Add `college-essay-prompt-analyzer/SKILL.md` to the Project's files.
3. Open **••• → Project settings** and paste the contents of [`chatgpt/project-instructions.md`](chatgpt/project-instructions.md) into Instructions.
4. Send your essay prompts inside that Project.

**Option 3: A single chat**
Attach `SKILL.md` to any chat and say: "Follow the process in this file exactly for the essay prompts I send next." Then send the prompt.

> Note: OpenAI has announced plans to retire custom GPTs, and personal accounts can no longer create new ones, so this guide doesn't use them.

### Notes

- This skill helps you **think and gather material**. It does not write your essay and will not make up experiences. The final essay should be your own story in your own words.
- Prompts change from year to year. Always check the current wording on the school's site or in the Common App.
- Platform features and plan availability change. See the [Claude Help Center](https://support.claude.com/en/articles/12512180-using-skills-in-claude) and the [OpenAI Help Center](https://help.openai.com) for the latest details.

### License

[MIT](LICENSE) © 2026 Ruoyu Yuan
