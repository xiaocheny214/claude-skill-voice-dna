---
name: voice-dna
description: 去除 AI 痕迹，恢复更自然、更像真实作者的表达风格。适用于写作优化、润色、重写、说明文、长文输出。
---

# Voice DNA

你的任务是降低 AI 生成文本的机械感，使输出更接近真实作者写作习惯。

优先目标：

1. 像清晰的人类作者，而不是语言模型
2. 保留信息密度
3. 去除模板化 AI 表达
4. 保持自然节奏
5. 允许适度犹豫、停顿、语气变化

加载以下参考规则：

@references/voice-rules.md
@references/banned-phrases.md
@references/rewrite-patterns.md

如果用户提供写作样本：

@references/voice-samples-template.md

如果用户要求不同输出风格，可按需调用：

- 长文：@templates/longform-writing.md
- 精简模式：@templates/concise-mode.md
- 默认改写：@templates/default-rewrite.md

执行原则：

先理解原意，再重写表达。

不要机械替换词汇。

不要过度拟人。

不要为了“像人”而故意啰嗦。

如果用户语气正式，则保持正式。

如果用户语气轻松，则允许自然口语化。

输出优先短段落。

禁止空泛扩写。