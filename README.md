# claude-skill-voice-dna

一个用于降低 Claude 写作中 AI 痕迹的 Skill。

基于 Ole Lehmann 关于「写作样本 + 风格规则」的思路整理，并进一步拆分为可维护、可扩展、支持 Reference 按需加载的 Claude Skill 结构。

它不是简单替换词汇，也不是刻意“装得像人类”。

核心目标是恢复更自然的表达节奏，减少模板化写作痕迹，让输出更像真实作者本身。

---

## 功能特性

支持：

- 去除常见 AI 套话与模板表达
- 降低机械化、对称化写作痕迹
- 恢复更自然的人类语言节奏
- 支持自定义 Voice Samples
- 支持 Reference 按需加载
- 多种写作模式切换（默认 / 长文 / 精简）
- 可维护的模块化 Skill 结构

---

# 项目结构

整个仓库采用模块化拆分，而不是把所有 Prompt 堆在一个文件里。

这样更容易维护，也方便按需扩展。

```bash
claude-skill-voice-dna/
│
├── SKILL.md
│   # Skill 主入口（调度中心）
│   # Claude 优先读取这个文件
│   # 负责加载 references、templates，以及整体行为控制
│
├── README.md
│   # 项目说明文档
│   # 介绍结构、安装方式、使用方法、自定义扩展
│
├── references/
│   # 规则层（Reference Layer）
│   # 存放可复用风格规则，支持按需加载
│   │
│   ├── voice-rules.md
│   │   # 写作规则
│   │   # 控制段落节奏、句长变化、动作型表达、信息密度
│   │
│   ├── banned-phrases.md
│   │   # 禁止表达
│   │   # 去除 AI 套话、营销味、机械化连接词
│   │
│   ├── rewrite-patterns.md
│   │   # 重写策略
│   │   # 控制去模板化、人类感、精简结构
│   │
│   └── voice-samples-template.md
│       # 自定义 Voice Samples
│       # 用户可追加旧文章、邮件、博客等样本
│       # 用于提取个人写作 DNA
│
├── templates/
│   # 模板层（Template Layer）
│   # 根据任务类型切换不同写作模式
│   │
│   ├── default-rewrite.md
│   │   # 默认改写模式
│   │   # 适合日常润色、AI 味清理、轻度重写
│   │
│   ├── longform-writing.md
│   │   # 长文模式
│   │   # 适合博客、分析、方案、说明文
│   │
│   └── concise-mode.md
│       # 精简模式
│       # 适合总结、短说明、高密度表达
│
└── examples/
    # 示例层（Example Layer）
    # 帮助快速理解 Skill 输出效果
    │
    ├── before-after.md
    │   # 改写前后对比
    │   # 展示 AI 味清理效果
    │
    └── custom-sample.md
        # 自定义样本示例
        # 教用户如何添加自己的 Voice Samples
```
# 如何安装 Skill

先把仓库拉到本地：

```bash
git clone https://github.com/xiaocheny214/claude-skill-voice-dna.git
```

进入项目目录：

```bash
cd claude-skill-voice-dna
```

确认目录结构完整：

```bash
claude-skill-voice-dna/
└── SKILL.md
```

`SKILL.md` 是 Claude Skill 的主入口文件。

---

## 第一步：找到 Claude Skills 目录

Claude Code 会自动读取默认的 Skills 目录。

根据系统不同，路径通常如下：

### macOS / Linux

```bash
~/.claude/skills/
```

---

### Windows（PowerShell）

```powershell
$HOME\.claude\skills\
```

通常实际路径类似：

```powershell
C:\Users\你的用户名\.claude\skills\
```

---

## 第二步：复制 Skill 到默认目录

把整个仓库复制进去。

最终结构应该是：

### macOS / Linux

```bash
~/.claude/skills/
└── voice-dna/
    ├── SKILL.md
    ├── references/
    ├── templates/
    └── examples/
```

---

### Windows

```powershell
C:\Users\你的用户名\.claude\skills\
└── voice-dna\
    ├── SKILL.md
    ├── references\
    ├── templates\
    └── examples\
```

注意：

Skill 文件夹名建议保持简洁稳定，例如：

```bash
voice-dna
```

不要：

```bash
claude-skill-voice-dna-v2-final-new
```

Claude 会把目录名识别为 Skill 名的一部分。

---

## 第三步：重启 Claude Code

复制完成后，重启 Claude Code。

Claude 会重新扫描：

```bash
~/.claude/skills/
```

并自动加载 Skill。

不需要额外安装命令。

---

# Skill 加载机制

Claude 会读取：

```bash
SKILL.md
```

这是整个 Skill 的入口。

然后按需加载：

```text
SKILL.md
   ↓
references/
   ↓
templates/
   ↓
voice samples（如果存在）
   ↓
生成最终输出
```

也就是 Reference Loading（按需引用）。

不是每次都把全部规则塞进上下文。

这样：

- 更稳定
- 上下文更干净
- Token 更省
- 扩展性更强

---

# 如何使用 Skill

安装后，在 Claude Code 中直接调用。

---

## 1. 默认调用

```text
使用 voice-dna skill 重写下面内容，让表达更自然。
```

适合：

- AI 味清洗
- 日常润色
- 轻度重写

---

## 2. 长文模式

```text
使用 voice-dna 的 longform 模式重写这篇文章。
```

适合：

- 博客
- 分析
- 提案
- 技术说明

---

## 3. 精简模式

```text
使用 voice-dna 的 concise mode 重写，减少修饰，直接表达。
```

适合：

- 总结
- 说明文
- 高信息密度写作

---

# 如何更新 Skill

如果仓库有更新：

进入 Skill 目录：

```bash
cd ~/.claude/skills/voice-dna
```

拉取最新版本：

```bash
git pull
```

然后重启 Claude Code。

---

# 如何卸载 Skill

直接删除目录：

### macOS / Linux

```bash
rm -rf ~/.claude/skills/voice-dna
```

### Windows（PowerShell）

```powershell
Remove-Item -Recurse -Force $HOME\.claude\skills\voice-dna
```


# 如果它帮到了你

这个 Skill 最初只是我为了解决 Claude 写作里过重的 AI 痕迹而整理的一个小工具。

后来逐步拆成了可维护的 Skill 结构，也希望它能帮到更多人。

如果你觉得它有用，欢迎点一个 ⭐ Star。

这会是继续更新它的动力。
# Test Feature
