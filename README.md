# College Essay Prompt Analyzer

**English** | [中文](README.zh-CN.md)

An AI skill that breaks down U.S. college application essay prompts, suggests writing directions, and generates brainstorming questionnaires. Works with **Claude** and **ChatGPT**.

## What it does

Send a college essay prompt (Common App personal statement, school supplements, Why Us, Why Major, short answers, and more) to the AI. It first asks you one thing: **do you want a questionnaire?**

| Your choice | What the AI gives you |
|---|---|
| **Yes, questionnaire** | A six-section brainstorming questionnaire. Each section has a short Purpose note and 5–7 questions. Only the questionnaire content is output, with no filling instructions or formatting rules. Your answers become the raw material for an outline and a draft. |
| **No questionnaire** | A prompt breakdown, the prompt type, a review of any material you shared, 2–3 genuinely different writing directions, and responses to anything else you asked for (draft feedback, topic comparison, an outline, and so on). |

## How it thinks

Both paths start with the same analysis:

1. **Prompt metadata**: source, required or optional, word limit, intended major, and how it fits with your other essays.
2. **Sentence-by-sentence breakdown**: the school's quoted values, the core verb, required sub-questions, optional parts, qualifiers (such as *someone you know* or *specifically*), what admissions readers are actually evaluating, and a suggested word budget.
3. **Prompt type**: growth, challenge, identity, disagreement, Why Us / Why Major, activity, or short answer, each with its own story arc and most common mistakes.
4. **Material review**: your strongest material, what is missing, and what is risky.
5. **Writing directions**: each with a core insight, story beats, why it fits the prompt, the material it needs, and its risks.

The six questionnaire sections follow one progression: **choosing the story → the scene → understanding and reflection → actions and evidence → meaning and connections → voice and ending**. The question-writing rules include listing several candidates before choosing one, reconstructing what was actually said and done, "If yes / If not" follow-ups, asking for concrete evidence of change, and a fill-in-the-blank test that checks whether a "Why Us" answer would still work for a different school.

The skill also tells the AI to **verify** prompt wording and school details (courses, professors, programs) and to leave out or flag anything it can't confirm. It **never invents experiences** for the student.

## Repository layout

```
college-essay-prompt-analyzer/
├── college-essay-prompt-analyzer/
│   └── SKILL.md                  # The skill itself (works with Claude and ChatGPT)
├── dist/
│   └── college-essay-prompt-analyzer.zip  # Upload package for claude.ai
├── chatgpt/
│   └── project-instructions.md   # Short instructions to paste into a ChatGPT Project
├── examples/
│   └── usage.md                  # Usage examples
├── LICENSE
├── README.md                     # English (default)
└── README.zh-CN.md               # 中文
```

The skill instructions are written in Simplified Chinese. The AI replies in the language you use, and questionnaires are written in English by default.

## Using it with Claude

**Claude on web, desktop, and mobile (claude.ai)**
Requires a Pro, Max, Team, or Enterprise plan with "Code execution and file creation" turned on.
1. Download [`dist/college-essay-prompt-analyzer.zip`](dist/college-essay-prompt-analyzer.zip) (open it and click **Download raw file**), or zip the `college-essay-prompt-analyzer/` folder yourself.
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

## Using it with ChatGPT

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

## Notes

- This skill helps you **think and gather material**. It does not write your essay and will not make up experiences. The final essay should be your own story in your own words.
- Prompts change from year to year. Always check the current wording on the school's site or in the Common App.
- Platform features and plan availability change. See the [Claude Help Center](https://support.claude.com/en/articles/12512180-using-skills-in-claude) and the [OpenAI Help Center](https://help.openai.com) for the latest details.

## License

[MIT](LICENSE) © 2026 Ruoyu Yuan
