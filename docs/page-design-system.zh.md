# Stateboard GitHub Page 设计系统

英文版是 canonical：[`page-design-system.md`](page-design-system.md)。

本文档记录 `docs/index.zh.html` 的页面 UI 规则。它是 Stateboard GitHub Page 的中文镜像。

## 方向

页面采用报纸头版模型，吸收 Washington Post 当前首页的结构语言：编辑化 masthead、强分割线导航、多栏主版面、右侧 briefing 栏、紧凑表格和高对比衬线字体。

这是 Stateboard 自己的页面。不要复制外部 logo、masthead 字形、文章内容、图片、订阅 UI、广告或任何专有视觉资产。

## 原则

- Stateboard 是项目状态层，不是普通 todo assistant。
- 首屏必须出现 masthead、一句话价值主张、`复制 prompt`、`查看 GitHub`、`安装 skill`、产品状态板预览和开始使用栏。
- 使用报纸密度：强规则线、窄 gutter、清楚分栏、紧凑摘要和表格。
- 产品承诺必须有边界。所有集成声明都要说明层级或运行环境依赖。
- 页面保持静态：不引入外部字体、框架、分析脚本或远程图片依赖。唯一允许的 JavaScript 是 quickstart prompt 的小型内联复制处理器。
- 语言切换必须是独立控件组。不要把 `EN / 中文 / 日本語 / 한국어 / ES` 混到文档、路线图或 GitHub 链接里。

## Tokens

### 字体

- Masthead：`Georgia`, `"Times New Roman"`, `Times`, `ui-serif`, `serif`。
- 多语言衬线 fallback：加入 `"Songti SC"`, `"STSong"`, `"Noto Serif CJK SC"`, `"Hiragino Mincho ProN"`, `"Yu Mincho"`, `"Nanum Myeongjo"`。
- UI sans：system sans，并加入 `PingFang SC`, `Microsoft YaHei`, `Hiragino Sans`, `Yu Gothic`, `Apple SD Gothic Neo`。
- 等宽：`ui-monospace`, `SFMono-Regular`, `Menlo`, `Consolas`, `"Liberation Mono"`, `monospace`。
- Masthead 尺寸：
  - desktop: `168px`
  - medium: `138px`
  - tablet: `112px`
  - mobile: `66px`
  - 窄屏 mobile: `58px`
- 不使用 viewport 连续缩放字号，也不使用负字距。
- CJK UI 标签必要时使用比英文更轻的 sans 字重，避免中文、日文、韩文因为 faux-heavy 渲染出现糊边。

### 色彩

- Canvas: `#f7f5ee`。
- Paper: `#fffdfa`。
- Ink / strong rule: `#111111`。
- Muted text: `#5d5a52`。
- Quiet text: `#7c776d`。
- Line: `#cac4b7`。
- Soft line: `#e3ded3`。
- Status green: `#15774f`。
- Status amber: `#b36812`。
- Status blue: `#2e638f`。

强调色只用于状态和集成层级。避免紫色、靛蓝渐变、装饰 blob、柔软 SaaS 卡片和 generic AI 风格。

## 布局

- 容器：`min(1390px, calc(100% - 32px))`。
- Header 结构：
  - dateline / utility row
  - 超大居中 masthead
  - 三个 action 的操作栏
  - sticky section nav
- Topline 分组：
  - 左侧：edition state
  - 中间：短 publication line
  - 右侧：utility links 和独立 language switcher
- 头版网格：
  - 左侧 lead story
  - 中间状态板预览
  - 右侧开始使用栏
- 次级网格：
  - 四个紧凑 brief 列：不是 todo、workflow、quickstart、integration tiers
- Quickstart：
  - 深色等宽 prompt 面板，允许横向滚动
- Integration tiers：
  - 编辑说明 + 可横向滚动表格

## 组件

### Language Switcher

- 语言切换位于 `.language-switcher`，与 `.utility-links` 之间用细竖线分隔。
- 当前公开语言页：
  - English: `index.html`
  - 简体中文: `index.zh.html`
  - 日本語: `index.ja.html`
  - 한국어: `index.ko.html`
  - Español: `index.es.html`
- 当前语言使用 `aria-current="page"`。
- 每个语言页都要包含五种语言和 `x-default` 的 `hreflang` alternate。

### Action Rail

- 始终展示 `复制 prompt`、`查看 GitHub`、`安装 skill`。
- 使用开源 outline 图标的 code-native SVG。右侧 rail 使用 Heroicons 风格的 24x24 outline glyph：无填充、`stroke: currentColor`、圆形端点和转角。
- 链接黑色、居中，并用竖线分隔。Action rail 下方不要再加双线分割。
- 移动端堆叠成三行。

### Board Preview

- 状态板是核心产品 artifact，不是装饰图。
- 使用紧凑 ledger 表格展示活跃项目、最新证据、下一步和同步边界。
- 行内容要体现 evidence-first、一个项目对应有限动作、以及分层同步边界。
- 移动端允许状态板在内部横向滚动，但整页不能横向溢出。

### Right Rail

- 使用报纸 briefing 栏展示 `Prompt 入口`、`Skill`、`Markdown fallback`、`规划中 adapters`。
- 每个条目包含一个无外框 stroke icon、短标题、一段紧凑说明和一个链接。
- 不要把可安装 workflow 命名为 `Codex skill`；公开页面统一叫 `Skill`，避免 Claude 和其他 AI assistant 用户误以为只能在 Codex 使用。

### Quickstart Prompt

- 保持真实 prompt 可见、可复制。
- Prompt 头部必须使用真正的 `<button>`，一键复制当前可见 prompt 文本；不要使用被动的 `copy-ready` 标签。
- 使用深色等宽代码面板。
- 用 `white-space: pre` 保留格式，并允许横向滚动。
- 未确认频率和具体时间时，不要声称会创建自动化。

### Integration Tiers

- 明确描述 `当前`、`Tier 1`、`Tier 2` 和 `Tier 3/4`。
- 区分任务同步、日历同步、通知投递和 fallback export。
- 不写笼统平台支持声明。

## 响应式

- 验证 `390px`、`768px` 和 `1440px`。
- Masthead 必须可读，不能撞边。
- Masthead 副标题使用更宽的 balanced text measure，避免中文、日文、韩文和西班牙语被拆成单字或单词孤行。
- 中文、日文、韩文长 story headline 和正文必须在自身分栏内换行，使用 `overflow-wrap: anywhere`、`word-break: normal` 和 `line-break: strict`。不要在长 CJK 文案上使用 `keep-all`，否则桌面端会跨栏重叠，窄屏会裁切。
- 西班牙语正文使用 `hyphens: auto` 处理较长单词。
- 小屏 section nav 可横向滚动。
- 表格和 prompt block 可以在自身容器内横向滚动。
- 普通正文必须自然换行，不能溢出。
- 右侧 rail 从侧栏折叠为两列，再折叠为一列。
- 四列 brief grid 折叠为两列，再折叠为一列。

## 实现规则

- 源文件：
  - `docs/index.html`
  - `docs/index.zh.html`
  - `docs/index.ja.html`
  - `docs/index.ko.html`
  - `docs/index.es.html`
  - `docs/page-design-system.md`
  - `docs/page-design-system.zh.md`
  - `prompts/stateboard-sync-prompt.md`
  - `prompts/stateboard-sync-prompt.zh.md`
  - `prompts/stateboard-sync-prompt.ja.md`
  - `prompts/stateboard-sync-prompt.ko.md`
  - `prompts/stateboard-sync-prompt.es.md`
  - `docs/prompts/stateboard-sync-prompt.md`
  - `docs/prompts/stateboard-sync-prompt.zh.md`
  - `docs/prompts/stateboard-sync-prompt.ja.md`
  - `docs/prompts/stateboard-sync-prompt.ko.md`
  - `docs/prompts/stateboard-sync-prompt.es.md`
- 英文页是 canonical；中文页镜像结构和行为。
- 日文、韩文、西班牙语页面镜像同一版式，但必须保留各自语言的阅读节奏，不能盲目继承英文换行行为。
- HTML/CSS 保持单文件自包含。
- 如果视觉 token 或组件规则变化，必须同步更新本文档和英文版。

## Review Checklist

- Masthead 和 ruled navigation 有编辑化报纸感。
- 首屏包括三个 action link 和产品状态板预览。
- 语言切换与文档 / 路线图 / GitHub 在视觉上分组明确。
- 页面避免 generic SaaS card、渐变、blob 和过度圆角 UI。
- 图标共享同一套 24px / 2px stroke 视觉系统。
- 右侧 rail 图标无外框；action rail 下方无双线分割。
- 状态板预览明确表达证据、优先级、下一步和同步边界。
- 集成声明保持分层和有边界。
- 代码块和表格不会导致整页横向溢出。
- 复制按钮复制的内容必须和各语言页面中可见的 prompt 文本一致。
- 中文、日文、韩文、西班牙语页面的 hero / subhead 不出现明显单字或单词孤行，并且 story、rail、table 文本都不能跨出自己的分栏边界。
- `git diff --check` 通过。
