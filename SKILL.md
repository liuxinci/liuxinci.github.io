---
name: homepage
description: 刘新慈个人主页 — 读取项目记忆、设计决策和修改指南
whenToUse: 当需要修改或了解个人主页项目时使用
model: opus
---

# 刘新慈个人主页 — 项目记忆

## 项目概述

刘新慈（智能建造/华东交通大学）的学术个人主页，参考 [zqyuan.com](https://zqyuan.com/) 与 [cen-jun.com](https://cen-jun.com/) 风格，单文件 HTML，部署到 [liuxinci.github.io](https://github.com/liuxinci/liuxinci.github.io)。

- **文件路径**：`index.html`
- **技术栈**：纯 HTML + CSS + JS，零依赖，零构建
- **预览方式**：浏览器直接打开 `index.html`（需本地 HTTP 服务以加载视频）

## 核心设计决策

### 配色（简洁学术风）
| 用途 | 颜色 | 说明 |
|------|------|------|
| 背景 | `#fafafa` | 浅灰白 |
| 卡片 | `#fff` | 白色 + 细边框 |
| 强调/链接 | `#2563eb` | 蓝色 |
| 奖项徽章 | `#fef3c7` / `#b45309` | 金色 |
| 文字 | `#333` | 深灰 |

### 布局
- 顶部固定导航（About · Projects · Research · Modeling · Honors · Misc · Skills）
- Hero 横幅：`media/hero/school.jpg` 背景 + `media/profile/photo.png` 头像 + 简介
- 主内容区 max-width 960px 居中，横向 publication 卡片布局
- Interests / Education 参考 cen-jun.com 排版
- Projects / Research 参考 zqyuan.com Publications 卡片（缩略图 + 标题 + 徽章 + TLDR）

### 动效
- IntersectionObserver 滚动渐入
- pub-item hover 阴影
- 科研视频 autoplay muted loop（离屏暂停）

## 内容结构（按时间倒序）

### 页面板块
1. **About** — 简介 + Interests + Education
2. **Projects** — Interview → BIMBASE → Fundus
3. **Research** — NeRF/3DGS 大创 + 自动播放视频
4. **Mathematical Modeling** — 4 篇论文 PDF 链接
5. **Honors** — 并列网格排列
6. **Miscellaneous** — 个人兴趣
7. **Skills** — 技能标签

## 媒体目录结构

```
media/
  hero/school.jpg
  profile/photo.png
  project/
    interview/screenshot-{1-4}.png   # 4=架构图(2026-06-15)
    bimbase/overview.png, truss.png, platform.png
    fundus/a46b47d9-....png (架构图), + 2 张展示图
  research/
    3dgs/car.mp4, train.mp4
    physgaussian/sofa*.mp4, vasedeck.mp4
    sketch-generative/bike.mp4, dolphin*.mp4, sking.mp4
  papers/
    cumcm-smoke.pdf, apmc-pet-industry.pdf,
    icm-spacecraft.pdf, huashu-scenic-route.pdf
```

## 修改指南

### 添加项目
复制 `.pub-item` 结构，在 `galleries` JS 对象中添加对应图片数组。

### 添加科研视频
在 `#research` 的 `.video-grid` 中添加：
```html
<div><video src="media/research/xxx/file.mp4" autoplay muted loop playsinline preload="auto"></video><div class="video-label">name</div></div>
```

### 添加数模论文
在 `.model-list` 中添加 `.model-item`，PDF 放入 `media/papers/`。

### 添加荣誉
在 `.honor-grid` 中添加 `.honor-chip`。

## 简历数据源
最新版：`简历/硕士申请-华东交通大学-刘新慈-简历.pdf`
