# 贾钦基个人简历网页 Design System

## 0. Research Log (greenfield only)
- Embedded refs: 根目录 `求职汇报.pptx` → 采用其“教育背景—项目实践—论文成果—博士研究—能力定位”的信息架构；视觉上取其克制的学术蓝与工程图纸式分区，不复制 PPT 版式。
- Lazyweb: skipped — 本任务有明确的本地内容参考，不需要外部产品检索。
- Imagen drafts: skipped — 用户需要可直接部署的静态简历页，不需要概念图流程。

## 1. Atmosphere & Identity
一页式学术工程履历，感觉应当稳健、清晰、可信。签名元素是“蓝图网格 + 章节编号”：用细线、编号和蓝色标记把复杂的研究与工程经历整理成可以快速扫描的结构。

## 2. Color

### Palette
| Role | Token | Light | Dark | Usage |
|---|---|---|---|---|
| Surface/primary | `--surface-primary` | `#F6F8FB` | `#111923` | 页面背景 |
| Surface/secondary | `--surface-secondary` | `#FFFFFF` | `#172331` | 内容卡片 |
| Surface/elevated | `--surface-elevated` | `#FFFFFF` | `#1D2B3A` | 重点信息 |
| Text/primary | `--text-primary` | `#17202B` | `#F3F6FA` | 标题、正文 |
| Text/secondary | `--text-secondary` | `#526172` | `#B8C5D2` | 说明文本 |
| Text/tertiary | `--text-tertiary` | `#5F6D7A` | `#A7B6C4` | 元数据 |
| Border/default | `--border-default` | `#D8E1EA` | `#304252` | 卡片、分隔线 |
| Border/subtle | `--border-subtle` | `#E9EEF3` | `#243442` | 细分隔 |
| Accent/primary | `--accent-primary` | `#1D5D8F` | `#78B9E8` | 链接、重点 |
| Accent/hover | `--accent-hover` | `#164A73` | `#A4D5F4` | 悬停、焦点 |
| Accent/soft | `--accent-soft` | `#E7F1F8` | `#203C51` | 标记背景 |
| Status/success | `--status-success` | `#2D6A4F` | `#78C39B` | 已发表 |
| Status/warning | `--status-warning` | `#966B20` | `#E6C27A` | 在审、返修 |

### Rules
- 采用“边框 + 色调变化”的深度策略，不使用重阴影。
- 蓝色只用于链接、状态和研究主题标记，不铺满大面积背景。
- 所有颜色必须来自本表中的 CSS token。

## 3. Typography

### Scale
| Level | Size | Weight | Line Height | Usage |
|---|---:|---:|---:|---|
| Display | `clamp(40px, 7vw, 76px)` | 700 | 1.02 | 首屏姓名 |
| H1 | `36px` | 700 | 1.15 | 章节标题 |
| H2 | `24px` | 700 | 1.25 | 卡片标题 |
| H3 | `18px` | 700 | 1.4 | 项目/论文标题 |
| Body/lg | `18px` | 400 | 1.75 | 首屏简介 |
| Body | `16px` | 400 | 1.75 | 正文 |
| Body/sm | `14px` | 400 | 1.6 | 辅助信息 |
| Caption | `12px` | 600 | 1.4 | 标签、年份 |
| Overline | `11px` | 700 | 1.3 | 章节编号 |

### Font Stack
- Primary: `"Noto Sans SC", "PingFang SC", "Microsoft YaHei", sans-serif`
- Editorial: `Georgia, "Times New Roman", serif`
- Mono: `"SFMono-Regular", Consolas, monospace`

## 4. Spacing & Layout
- Base unit: 4px。
- Main max width: 1180px。
- Grid: 12 列，桌面 24px gutter；移动端单列。
- Breakpoints: 640px / 768px / 1024px / 1280px。
- Section rhythm: 80px 桌面、56px 移动端；卡片内边距 24px。

## 5. Components

### Section Header
- **Structure**: 编号 + 小标题 + 主标题 + 描述。
- **Variants**: default / compact。
- **Spacing**: section rhythm, 16px 内部间距。
- **States**: static。
- **Accessibility**: 使用真实 heading 层级，编号不承担唯一语义。
- **Motion**: 进入时 opacity + translateY。

### Info Card
- **Structure**: 卡片标题、元数据、正文或列表。
- **Variants**: education / project / publication / research。
- **Spacing**: 24px padding, 16px item gap。
- **States**: default / hover / focus-within。
- **Accessibility**: 不把整张卡伪装成按钮；链接使用明确文本。
- **Motion**: hover 只改变 border-color 和 translateY。

### Tag
- **Structure**: inline text label。
- **Variants**: blue / green / amber / neutral。
- **Spacing**: 4px 8px。
- **States**: static。
- **Accessibility**: 不用颜色作为唯一信息来源。
- **Motion**: none。

## 6. Motion & Interaction
- Standard: 240ms ease-out，用于卡片 hover/focus。
- Emphasis: 520ms cubic-bezier(0.16, 1, 0.3, 1)，用于首屏与区块进入。
- 只动画 transform 和 opacity；尊重 `prefers-reduced-motion`。
- 唯一的交互动作是导航锚点、邮箱/电话链接和外部论文链接。

## 7. Depth & Surface
- Strategy: mixed，但以 borders + tonal-shift 为主。
- 页面背景使用极淡蓝灰，内容卡片使用白色；不使用厚重阴影。
- 蓝图网格为低对比度背景纹理，只服务于“工程/研究”身份，不影响文本对比度。

## 8. Accessibility Constraints & Accepted Debt
- WCAG 2.2 AA；正文对比度目标 4.5:1；所有链接有可见 focus；键盘可访问；支持 reduced motion。
- Accepted debt: 简历中的邮箱在 PDF 与 PPT 中存在差异，当前采用 PPT 中的 `jax@hnu.edu.cn`；发布前由本人确认。
