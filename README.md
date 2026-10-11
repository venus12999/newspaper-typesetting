# 现代报刊排版

给 Cursor 和其他 Agent 用的排版 skill。把几篇文章排成现代报纸或杂志内页，而不是复古报头加花边。

四种版式：

- **大图压题**：大标题压在满幅照片上，适合采访、特写、游记
- **巨型字母**：超大衬字衬在正文后面，适合评论和文化稿
- **斜切色块**：照片斜边插入纯色标题块，适合生活方式、体育、科技
- **传统大报**：双细线刊头栏和竖线分栏，适合头版

正文固定衬线 13px、行高 20px、两端对齐。每篇文章只用一个栏目色：粉 `#C85898`、赤陶 `#B04A1E` 或蓝 `#2E79B5`。

## 安装

```bash
mkdir -p ~/.cursor/skills/newspaper-typesetting
curl -fsSL -o ~/.cursor/skills/newspaper-typesetting/SKILL.md \
  https://raw.githubusercontent.com/venus12999/newspaper-typesetting/main/SKILL.md
```

装好后新开一个对话。说「重新排版」「做成报纸内页」或「导出 PDF」时，Agent 会按 `SKILL.md` 来排。

## 和复古报纸模板的差别

已有的报纸 skill 多半是报头、双线、引文框、泛黄纸。这份 skill 要的是强烈的层级：一个大焦点、一块栏目色、文章之间留白。蕾丝边、四角纹样、渐变和阴影不要用。

## 不会包含的内容

这个仓库只有排版方法。不要把别人的文章、姓名或照片提交进来。

## 致谢

版式参考《LUGARES》Tepozotlán 版、De Morgen「TAAL」版和《SEPEDA》自行车版。传统大报的报头字和分栏做法参考 [Newspaper-UI](https://github.com/Aravinth1525/Newspaper-UI)。纸色和黑白印刷处理的想法参考 [khabar.css](https://github.com/minku-singh/khabar.css)。

## 许可证

[MIT](LICENSE)
