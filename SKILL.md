---
name: newspaper-typesetting
description: 把学生文章/报纸内容排成现代报刊风格的 canvas TSX 或 HTML。适用于"排版太丑了，参考这些图片重新排"、"把这几篇文章做成报纸/杂志内页"、"把这个 tsx 报纸导出成 PDF"等请求。核心方法：大标题压图、巨型字母衬底、斜切色块、传统大报四种版式模板 + 可复用组件 + 避坑清单。融合了 GitHub 上 Newspaper-UI（Chomsky 报头字/Bebas Neue/双线刊头栏）与 khabar.css（照片黑白印刷化处理/CSS 变量令牌）的技巧。
---

# 现代报刊排版 Skill

把若干篇文章排成一份好看的报纸/杂志内页。按下面四种模板排。不要把未获授权的学生原稿、姓名或照片放进公开仓库。

## 什么时候用

- 用户给了文章正文 + 参考报纸截图，要求"重新排版"
- 用户说现在的排版"太丑/太土/像 Word 文档"
- 需要在 Cursor canvas（`cursor/canvas` 组件）或普通 HTML 里做报刊内页
- 需要把排好的版面导出 PDF / 长图

## 总原则：版式 = 信息层级

丑的排版通常死于三件事：**均匀的网格**（所有元素一样大，没有焦点）、**装饰性边框**（蕾丝、双线、四角纹样——显廉价）、**图片卑微地缩在角落里**。

好看的排版只做一件事：制造强烈的层级对比——

1. **一个巨大的视觉焦点**：96px 大标题 / 满幅照片 / 巨型字母，三选一
2. **一个纯色的功能色块**：dek（副题）、数据表、引言，各配一个栏目色
3. **大量留白**：文章之间隔 60–80px，比任何装饰都高级
4. **正文永远朴素**：衬线 13px、行高 20px、两端对齐，不要动它

栏目色：每篇文章一个 ink 色（粉 `#C85898` / 赤陶 `#B04A1E` / 蓝 `#2E79B5`），标题、色块、小标题、首字下沉都用它。

## 四种版式模板

### 模板 A：大图压题版（适合采访 / 特写 / 游记）

参考：《LUGARES》Tepozotlán 旅行版——大标题、满幅照片、彩色圆形信息点、多栏正文。

```
┌──────────────────────────────────────────┐
│ KICKER ———————— 栏目名+细线 ———— 刊名页码  │
│ NORTH            ← 84–96px 无衬线 900   │
│ PROFITS             ← 第二行用深色同族色   │
│ ┌──────────── 满幅照片 400px ──────────┐  │
│ └──────────────────────────────────────┘  │
│ ▍粉色 dek 色块（中英文副题，白字）          │
│ 图说(左)                    WORDS—作者(右) │
│ 竖照片(5fr) │ 首段下沉首字 + 2×2 圆形气泡(7fr)│
│ 三栏正文，Q— 问题小标题(栏目色大写)         │
└──────────────────────────────────────────┘
```

### 模板 B：巨型字母衬底版（适合评论 / 深度 / 文化）

参考：De Morgen「5.000 woorden」——超大衬线标题、巨型字母衬底、边栏小栏目、大号引言收尾。

```
┌──────────────────────────────────────────┐
│ KICKER ———————————————————— 刊名页码       │
│ 超大衬线标题(50px serif) │ 折纸色块装饰     │
│ 斜体副题+作者署名        │ □FIELD GUIDE 框 │
│ T A G S ← 300px 巨型字母 8% 透明度衬底     │
│ 四栏正文压在字母上（columnCount:4）        │
│ 信息图(5fr) │ 双栏正文(7fr)               │
│ ▍大号引言(21px斜体) │ 结论段 + 小字落款     │
└──────────────────────────────────────────┘
```

### 模板 C：斜切运动版（适合生活方式 / 体育 / 科技）

参考：《SEPEDA》自行车版——斜切照片插入纯色标题块、数据侧栏表、大图收尾。

```
┌──────────────────────────────────────────┐
│ KICKER ———————————————————— 刊名页码       │
│ 斜切照片(clip-path)╱ 蓝块白字大标题         │
│  ROAD|POOL          FIELD                 │
│  (斜边插入色块)     / NOTES(50%白)         │
│  图说                                        │
│ 双栏正文(8fr) │ THE SPLIT 编号表(4fr)      │
│               │ IN THE BAG 装备表          │
│ 通栏大图(原始比例,勿裁) + 右对齐图说        │
└──────────────────────────────────────────┘
```

### 模板 D：传统大报版（适合头版 / 整期合刊 / 正式感）

参考：GitHub `Aravinth1525/Newspaper-UI`（The Hindu 风格）——古典报头、双线刊头栏、竖线分栏。

```
┌──────────────────────────────────────────┐
│ ┌─boxed─┐    THE RECORD     ┌─boxed─┐    │
│ │live   │  ← Chomsky 报头字  │作者信息│    │
├──────────────────────────────────────────┤
│ 日期 · 期号 · 价格   ← 上下各一条 1px 细线 │
├──────────────────┬───────────────────────┤
│ 侧文(flex column│ 主文章                  │
│  wrap 双栏)     │ 82px Bebas 标题+大图    │
│ ────────────────┤ 正文                   │
└──────────────────┴───────────────────────┘
```

要点：
- **报头（nameplate）**：`font-family: Chomsky`（开源哥特/花体字，报纸名专用，去 GitHub 下载 woff）；左右各放一个 1px 线框小盒子（live / 期号 / 天气），这是大报报头的经典结构
- **刊头栏（nav bar）**：`border-top: 1px solid; border-bottom: 1px solid` 夹着日期/栏目名——双细线是大报的标志，比任何花纹都"贵"
- **正文分栏**：`display:flex; flex-direction:column; flex-wrap:wrap; max-height:xxx` + 子元素 `width:50%`，得到报纸式"先填满一栏再流下一栏"的效果；栏间用 `border-right: 1px solid` 竖细线分隔。这是 CSS `columnCount` 之外的纯 flex 替代方案
- **纸色**：`background: #FFFFFD`（比纯白暖一丁点）；`html { font-size: 140% }` 做整体字号缩放

## 可复用组件代码（canvas TSX，HTML 同理）

字体常量和主题：

```tsx
const SERIF = 'Palatino, "Palatino Linotype", "Iowan Old Style", "Times New Roman", serif';
// DISPLAY 栈：有网时第一个 Bebas Neue 生效（真正的窄体展示字，比 Arial Narrow 高级得多）
const DISPLAY = '"Bebas Neue", "Helvetica Neue", "Arial Narrow", Arial, sans-serif';
// 经典报头字（模板D）：Chomsky，开源，woff 文件从 GitHub 下载后 base64 内联
// 纸色：#FFFFFD
// ink 色每篇一换：#C85898 / #B04A1E / #2E79B5
```

正文（永远长这样，别改）：

```tsx
function Graf({ children }: { children: string }) {
  const theme = useHostTheme();
  return (
    <Text style={{
      fontFamily: SERIF, fontSize: 13, lineHeight: "20px",
      textAlign: "justify", color: theme.text.primary, margin: 0, hyphens: "auto",
    }}>{children}</Text>
  );
}
```

下沉首字（float + 行高 34px 是关键——行高大了会挤歪第三行）：

```tsx
<span style={{ float: "left", fontFamily: SERIF, fontSize: 44, lineHeight: "34px",
  fontWeight: 700, color, paddingRight: 8, paddingTop: 3 }}>{first}</span>
```

刊头行（栏目线，每篇顶部都有）：

```tsx
<Row align="baseline" justify="space-between">
  <Text weight="bold" style={{ fontFamily: DISPLAY, color: ink, letterSpacing: 3,
    textTransform: "uppercase", fontSize: 11, margin: 0 }}>{left}</Text>
  <Text size="small" style={{ fontFamily: DISPLAY, color: theme.text.tertiary,
    letterSpacing: 2.4, textTransform: "uppercase", fontSize: 10, margin: 0 }}>{right}</Text>
</Row>
<div style={{ borderTop: `1px solid ${color}`, marginTop: 6 }} />
```

大标题（模板 A/C 用；Bebas Neue 天生窄体高挑，字重填 normal 即可）：

```tsx
<div style={{ fontFamily: DISPLAY, fontWeight: 900, fontSize: 96, lineHeight: "0.96",
  letterSpacing: -3, textTransform: "uppercase", color: ink }}>NORTH</div>
```

圆形信息气泡（模板 A 的信息点）：

```tsx
<div style={{ width: 168, height: 168, borderRadius: "50%", background: color,
  display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center",
  textAlign: "center", padding: 20, boxSizing: "border-box", color: "#fff" }}>
  <div style={{ fontFamily: DISPLAY, fontWeight: 800, fontSize: 12.5, letterSpacing: 1.4,
    textTransform: "uppercase" }}>{title}</div>
  <div style={{ width: 18, borderTop: "1px solid rgba(255,255,255,0.7)", margin: "7px 0" }} />
  <div style={{ fontFamily: SERIF, fontStyle: "italic", fontSize: 10.5, lineHeight: "13.5px" }}>{text}</div>
</div>
```

数据侧栏表（模板 C，仿报纸 DETAIL STAGE 表）：

```tsx
<div style={{ background: theme.bg.elevated, borderTop: `3px solid ${color}`,
  borderBottom: `1px solid ${theme.stroke.secondary}`, padding: "12px 0 10px" }}>
  <Text weight="bold" style={{ fontFamily: DISPLAY, fontSize: 12, letterSpacing: 2,
    textTransform: "uppercase", color, margin: "0 0 6px" }}>{title}</Text>
  {rows.map(([k, v], i) => (
    <div key={i} style={{ display: "flex", gap: 10, alignItems: "baseline", padding: "6px 0",
      borderTop: i === 0 ? "none" : `1px solid ${theme.stroke.secondary}` }}>
      <span style={{ fontFamily: DISPLAY, fontWeight: 800, fontSize: 15, color, minWidth: 18 }}>{k}</span>
      <span style={{ fontFamily: SERIF, fontSize: 12.5, lineHeight: "17px" }}>{v}</span>
    </div>
  ))}
</div>
```

大报分栏（模板 D，flex 替代 columnCount，栏序为先填满一栏再下一栏）：

```tsx
<div style={{ display: "flex", flexDirection: "column", flexWrap: "wrap",
  maxHeight: 1000, borderRight: `1px solid ${theme.stroke.primary}`, paddingRight: 14 }}>
  <div style={{ width: "50%" }}>段落…</div>
  ...
</div>
```

照片黑白印刷化处理（来自 khabar.css——学生报纸照片来源杂、色调乱，**统一转黑白印刷风后整版立刻协调**；按需使用，彩色大图版可不加）：

```css
img {
  filter: grayscale(100%) contrast(1.2) brightness(1.05);
  /* 进阶：mix-blend-mode: color-burn 叠出半调网点感（khabar.css 用法），注意需要底色配合 */
}
```

设计令牌（来自 khabar.css 的 CSS 变量思想——把每篇的 ink/wash/纸色提成常量，全篇引用，别散落硬编码）：

```tsx
const TOKENS = {
  paper: "#FFFFFD",
  articles: [
    { ink: "#C85898", inkDeep: "#8F2F6B", wash: "#F6E3EE" },   // Interview
    { ink: "#B04A1E", inkLight: "#D97B4A", wash: "#F7E8E0" },  // Opinion
    { ink: "#2E79B5", inkPale: "rgba(255,255,255,0.5)", wash: "#E4EEF6" }, // Lifestyle
  ],
};
```

多栏正文：包一层 `<div style={{ columnCount: 3, columnGap: 24, columnRule: `1px solid ${theme.stroke.secondary}` }}>`，里面放 Stack 包裹的段落。

## 避坑清单（血泪经验）

1. **不要用负 margin + z-index 让文字压图**。在 Cursor canvas 的预览环境里这种叠加会渲染错乱（文字重叠/丢失）。文字压图只用一个父级 `position: relative` 容器内的 absolute 子层；更稳妥的是标题在排版流里、照片紧随其后的"上下结构"，或 absolute 但结构简单。
2. **clip-path 斜切 + 固定高度 + object-fit: cover 不要叠加使用**——会把图片内容裁掉一块，在 canvas 里可能整块被遮。装饰性图表/海报用原始比例（`height: "auto"`），照片才允许 cover 裁剪。
3. **不要**蕾丝/重复花纹边框、双线外框、四角纹样、渐变、阴影、emoji——这些是把版面拉廉价的最快方式。
4. 图片要么 `height: auto` 保持原比例，要么给照片定 `height + objectFit: "cover" + objectPosition` 精确控制裁切区域（人脸通常在 `center 38%`）。
5. 每篇文章一个 ink 色贯穿始终：标题、kicker 线、dek 色块、问题小标题、首字下沉、数据表顶线。全篇颜色不超过这个 ink + 黑白灰。
6. 文章之间 `Stack gap={80}`，靠留白分篇，不要再加报头/分隔装饰。
7. 圆形气泡里文字最多三行；侧栏表每行一栏短句，长了就换行高。
8. 网络字体（Bebas Neue / Chomsky）只在 HTML/浏览器环境可靠；canvas 离线预览可能加载不到，DISPLAY 栈必须保留 Helvetica/Arial Narrow 兜底，排完先在真实 canvas 里看一眼字体是否回退。

## canvas TSX 文件骨架

```tsx
import { Grid, H2, Row, Stack, Text, useHostTheme } from "cursor/canvas";

const SERIF = '...'; const DISPLAY = '...';
const IMG_XXX = "data:image/jpeg;base64,..."; // 图片一律内联 base64

// 组件：Graf / LeadGraf / KickerRow / Caption / Byline / Question / Bubble / SideBox ...

function ArticleOne() { /* 模板A */ }
function ArticleTwo() { /* 模板B */ }
function ArticleThree() { /* 模板C */ }

export default function Paper() {
  const theme = useHostTheme();
  const page = theme.kind === "light" ? theme.fill.secondary : theme.bg.chrome;
  return (
    <div style={{ background: page, color: theme.text.primary, minHeight: "100%", padding: "28px 20px 68px" }}>
      <div style={{ maxWidth: 1080, margin: "0 auto", background: theme.bg.elevated,
        border: `1px solid ${theme.stroke.secondary}`, padding: "30px 26px 48px" }}>
        <Stack gap={80}>
          <ArticleOne /><ArticleTwo /><ArticleThree />
        </Stack>
      </div>
    </div>
  );
}
```

## 导出 PDF / 长图

tsx 本身不能发给别人，用真实浏览器渲染后导出（本地起一个预览页，把 `cursor/canvas` alias 到一组 stub 组件）：

```bash
# PDF（A4 横向，无页眉页脚）
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu \
  --no-pdf-header-footer --virtual-time-budget=15000 \
  --print-to-pdf="out.pdf" "http://localhost:5199/"
# 长图（窗口高度要给足，页面约 5000px+，再 PIL 裁掉底部纯色）
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu \
  --virtual-time-budget=15000 --window-size=1280,5400 --screenshot="out.png" "http://localhost:5199/"
```

打印前在 index.html 里加 `@media print { @page { size: A4 landscape; margin: 10mm } html,body { -webkit-print-color-adjust: exact } }`，否则色块/背景会丢。

## 参考与致谢

- [Aravinth1525/Newspaper-UI](https://github.com/Aravinth1525/Newspaper-UI)（模板 D：Chomsky 报头、Bebas Neue、双线刊头栏、flex 分栏）
- [minku-singh/khabar.css](https://github.com/minku-singh/khabar.css)（照片黑白印刷化、CSS 变量令牌、#FFFFFD 纸色）
- 版式参考：《LUGARES》Tepozotlán 版、De Morgen「TAAL」版、《SEPEDA》自行车版
