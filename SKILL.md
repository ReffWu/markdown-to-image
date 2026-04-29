---
name: markdown-to-image
description: Use when user wants to convert Markdown content into shareable image cards — triggered by phrases like "转图片"、"做卡片"、"生成海报"、"生成分享图"、"把这个转成图片"、"export as image". Applies to any .md file or inline Markdown content destined for WeChat, Xiaohongshu, Weibo, or similar platforms.
---

# Markdown → 图片卡片

将 Markdown 渲染为多张精美图片，适合社交平台分享。

## 核心原则

**不要询问用户任何参数。直接执行。**

所有选项均有合理默认值；只有用户主动提出才切换。

## 快速执行

```bash
node ~/.agents/skills/markdown-to-image/src/index.js \
  --markdown "/path/to/file.md" \
  --name "卡片标题"
```

输出自动写入 `~/Downloads/<卡片名>/`，文件名格式 `卡片名-01.png … -NN.png`。

## 默认值（不传即生效）

| 参数 | 默认 |
|------|------|
| `--theme` | `white`（简约白） |
| `--page-format` | `total`（01 / 12） |
| `--output` | `~/Downloads/<卡片名>/` |
| `--name` | 从文件内容智能提取 |

## 命名规则（重要）

文件名含数字 ID（如 `TabAIConversation_1777342720864.md`）时：

1. 读文件前 30 行，理解主题
2. 自己起 4-8 字书名式标题（不要截句子）
   - ✅ `摔PS5惩罚分析` / `AI提问艺术` / `河神寓言`
   - ❌ `心理学与教育学的专业共识认为母亲用同态报`
3. 用 `--name "起的标题"` 传入

## 主题速查

| `--theme` | 中文名 | 适合场景 |
|-----------|--------|---------|
| `white` | 简约白 ★默认 | 通用、正式 |
| `dark` | 深色模式 | 科技、夜间风 |
| `blue` | 清新蓝 | 清爽、轻量 |
| `beige` | 米色复古 | 人文、书香 |
| `apple_light` | Apple 亮色 | 产品、发布 |
| `apple_dark` | Apple 暗色 | 产品暗色版 |
| `glass_light` | 毛玻璃亮 | 现代感强 |
| `glass_dark` | 毛玻璃暗 | 高级感 |
| `editorial` | 编辑风格 | 杂志、专栏 |
| `midnight` | 午夜黑 | WWDC 风格 |
| `ocean` | 海洋蓝 | 深蓝渐变 |
| `sunset` | 落日橙 | 暖色渐变 |

## 页码格式

```bash
--page-format default    # 01, 02, 03
--page-format total      # 01 / 12, 02 / 12  ← 默认
--page-format brackets   # (1/12), (2/12)
```

## 完整示例

```bash
node ~/.agents/skills/markdown-to-image/src/index.js \
  --markdown "/Users/wuruifu/Downloads/TabAIConversation_1777407553373.md" \
  --name "摔PS5惩罚分析" \
  --theme white
```

输出：`~/Downloads/摔PS5惩罚分析/摔PS5惩罚分析-01.png` … `*-NN.png`

## 常见错误

| 错误 | 正确做法 |
|------|---------|
| 询问用户要哪个主题 | 直接用 `white`，完成后可提示切换 |
| 用文件名乱码当卡片名 | 读内容，自己起标题 |
| 手动传 `--output` | 省略，自动输出到 Downloads |
| 截句子当标题 | 起书名式短标题（4-8 字） |
