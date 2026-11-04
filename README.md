# 英语阅读困难解决 · 长难句主干训练 Skill

一个纯提示词（instructions-only）的开源 Skill：把"长难句读不懂"变成每天能练一遍的动作——**先自己找主干，再看答案**。

## 1. 项目解决什么问题

英语阅读读不懂，多数时候不是词不认识，而是**句子主干被修饰成分埋住了**：从句、非谓语、插入语一件套一件，读到最后忘了谁修饰谁。常见的失败练法是"看解析"——解析看懂了，下次还是找不到。

这个 Skill 反过来做：它不给解析，先逼你自己判断"主语是谁、主句谓语是哪个、哪些是修饰成分"，你交卷之后它才核对、标注、翻译。练的是**判断主干的能力**，不是"看懂解析的能力"。

## 2. 主要功能

- **按类型出题**：非谓语拉长句 / 定语从句 / 宾语从句 / 状语从句 / 同位语从句 / 插入句 / 混合并列复合句，7 类可单选，也可混搭。
- **出题只给句子**：一次 1 句，35–60 词的真题阅读风格长句（点名四六级/考研/雅思时按该考试难度放宽到 30–60 词）；不拆分、不加粗、不注释、不翻译、不预告考点。
- **等你作答才批改**：判你标的主语、主句谓语对不对，明确说出差在哪（例如"你标的谓语在从句里"）。
- **分三级纠错，不一次喂答案**：第 1 次判错只指方向；同一句连续 2 次判错才给一条小提示（如"留意真正的谓语在哪里，非谓语不能做主句谓语"）；第 3 次仍错或你放弃，才公布主干。
- **逐处标注修饰成分**：按原句顺序列出每一处从句、非谓语短语、介词短语、插入语、同位语、并列成分，写明修饰谁，并统计"你漏了几处"。
- **整句通顺翻译**：主干清楚了才给中文，先直译骨架再顺成中文。
- **主干小测**：最后只问 1 个能在主干里找到答案的问题，只考主干信息，不考细节和态度推断。
- **防重复与难度适配**：同一会话不出同一句；句库用完按同类型现造；点名四六级/考研/雅思时按该考试阅读难度出句。

## 3. 安装方法

这个 Skill 只有三个文本文件，没有脚本、不需要装依赖。仓库根目录就是技能目录，clone 下来即可直接当技能用：

```
english-reading-difficulty-skill/   ← 仓库根 = 技能根
├── SKILL.md                    # 主指令：三步工作流、出题禁令、判错与提示规则
├── agents/openai.yaml          # 展示名、简介、默认开场语（供读取该文件的客户端使用）
├── references/sentence-bank.md # 句库：七类各 2 句，含主干/修饰/翻译/主干小测/提示
├── README.md
├── LICENSE
└── .gitignore
```

任选一种：

1. **clone 到 Agent 的 skills 目录**：
   ```bash
   git clone https://github.com/August279/english-reading-difficulty-skill.git \
     <你的 skills 目录>/english-reading-difficulty-skill
   ```
   例如豆包工作区的 `.../workspace/.user_skills/`，或 `~/.claude/skills/`、你所用 Agent 对应的 skills 目录。目录名用 `english-reading-difficulty-skill`（与 `SKILL.md` 的 `name` 一致），clone 后无需改动结构。
2. **不安装，直接给 Agent 读**：把 `SKILL.md`（以及出题时要用的 `references/sentence-bank.md`）交给任意支持读文件的 Agent/模型，它就能按这套规则陪练。

标识说明：`SKILL.md` 里 `name: english-reading-difficulty-skill` 用英文，是因为 Skill 规范与校验脚本要求 lowercase-hyphen-case；中文只出现在标题、说明和句库里。触发靠 `description` 里的场景词——长难句、找主干、句法分析、句子结构拆解、英语阅读读不懂、分析这句话的成分，以及启动口令“开始长难句练习”。

## 4. 使用方法

1. **触发**：说“开始长难句练习”，或“练一句长难句”“帮我分析这句话的成分”“我英语阅读总是读不懂长句”之类的话；也可以直接说“练定语从句”“来一句插入语”。
2. **第 1 步｜选类型**：Skill 会列出 7 个编号让你选，可单选可混搭（如"2 和 6"）；说"随便"它会替你选并说明选了什么。
3. **第 2 步｜自己找主干**：它只给一句英文，你要打字发回三样东西——主语（主句的）、谓语（主句的）、修饰成分（能找几处写几处，注明修饰谁、是什么成分）。不确定也照写，写错才有的可改。
4. **第 3 步｜看批改**：拿到的是一份【主干核对】+【修饰成分】+【全句翻译】+【主干小测】。小测答完，它会问"再来一句？同类型 / 换类型 / 结束"。

几个实用口令：`换一句`、`太简单了` / `太难了`、`来真题原句`、`我放弃了，看答案`、`直接翻译`（它会先说明这是主干训练，你坚持就照做）。

## 5. 输入输出示例

**用户**：练定语从句。

**AI**（只给句子，不给任何提示）：

> **练习类型**：定语从句
> **句子**：
>
> > The assumption on which most of the early research was built — that children learn language simply by imitation — began to collapse once studies appeared which showed that infants respond to grammatical patterns they had never heard before.
>
> 请先自己找出并打字发给我：1 主语（主句的）2 谓语（主句的）3 修饰成分（注明修饰谁、什么成分）

**用户（第 1 次，错）**：主语 the assumption，谓语 was built。

**AI**：主干还没找对。你标的谓语在从句里，不是主句的谓语。再找一次。

**用户（第 2 次，仍错）**：主语 children，谓语 learn。

**AI**（同一句连续 2 次判错 → 只给一条提示，不给答案）：留意这个句子真正的谓语在哪里，非谓语不能做主句谓语。再看一次破折号那一段之外的部分还缺什么。

**用户（第 3 次，对）**：主语 the assumption，谓语 began。

**AI**（一次性输出批改）：

> 【主干核对】标准主干：主语 the assumption ｜ 谓语 began（began to collapse）；你的答案一致；判定：✅ 完全正确
> 【修饰成分】你漏了 6 处：`on which … was built` → 定语从句，修饰 assumption；`that children learn language simply by imitation` → 同位语从句，说明 assumption 的内容；`once studies appeared` → 时间状语从句；`which showed that …` → 定语从句，修饰 studies；`that infants respond to …` → 宾语从句，作 showed 的宾语；`they had never heard before` → 省略关系词的定语从句，修饰 patterns
> 【全句翻译】早期大多数研究赖以建立的那个假设——儿童只靠模仿就能学会语言——在出现了一些研究之后开始瓦解，这些研究表明，婴儿会对他们从未听过的语法模式作出反应。
> 【主干小测】开始瓦解的是什么？（请只根据主干回答）
> 再来一句？同类型 / 换类型 / 结束。

答对主干会直接判 ✅；主语对、谓语错这类"只对一半"也算判错，会进入上面的重试流程。并列句/复合句有多个主句时，AI 会按 ①② 分行逐个核对。

## 附：自检

```bash
# 在仓库根目录执行；Windows 若遇编码问题，先设 PYTHONUTF8=1
python quick_validate.py .
```

预期输出：`Skill is valid!`（`quick_validate.py` 是常见的 Skill frontmatter 校验脚本，随你所用 Agent 的 Skill 工具链提供，本仓库不打包。）

句库为真题阅读风格的自建/改写句，**不标注具体出处**；如需真题原句，直接用 `来真题原句` 口令，Skill 会改从真题篇章取句。

## 许可证

[MIT License](LICENSE) © 2026 英语阅读困难解决-skill contributors
