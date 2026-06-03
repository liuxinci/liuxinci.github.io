---
name: homepage
description: 刘新慈个人主页 — 读取项目记忆、设计决策和修改指南
whenToUse: 当需要修改或了解个人主页项目时使用
model: opus
---

# 刘新慈个人主页 — 项目记忆

## 项目概述

刘新慈（智能建造/城市地下空间工程学生）的学术个人主页，单文件 HTML，模仿 [qiang-zou.github.io](https://qiang-zou.github.io/) 风格，最终部署到 GitHub Pages。

- **文件路径**：`AllDocument\个人主页介绍\index.html`
- **技术栈**：纯 HTML + CSS + JS，零依赖，零构建
- **预览方式**：浏览器直接打开 `index.html`

## 核心设计决策

### 配色（肉色系暖调）
| 用途 | 颜色 | 说明 |
|------|------|------|
| 背景 | `#FDF8F4` | 极浅米白 |
| 卡片 | `#FAF0E6` | 亚麻色 |
| 主色 | `#D4A574` | 暖沙色 |
| 强调 | `#C4956A` | 焦糖色 |
| 导航 | `#F5E6D3` | 浅肉色 |
| 文字 | `#4A4A4A` | 深灰 |

### 布局
- CSS Grid 双栏布局：左侧固定侧边栏（280px）+ 右侧主内容
- 侧边栏 `margin-left: -10px` 向左微调
- 响应式断点：860px（平板切换单栏）、600px（手机）
- 导航栏固定顶部，毛玻璃效果

### 动效
- IntersectionObserver 滚动渐入（`.section` → `.visible`）
- 卡片 hover 上浮 + 阴影
- 导航链接 hover 变色

## 内容结构

### 页面板块（按导航顺序）
1. **关于我** — 简短自我介绍
2. **教育经历** — 时间轴样式，GPA 4.20/5.0，排名 1/42
3. **科研经历** — 1个 NeRF 项目卡片 + 2个视频组
4. **项目经历** — 2个项目卡片（各含一个 card-video）
5. **个人技能** — 标签云
6. **竞赛奖项/校级荣誉/知识产权** — 三项列表

## 视频系统

### 视频弹窗（Modal）
- `#videoModal` + `#modalVideo`（视频） + `#modalImage`（图片）
- 点击 `.video-thumb` 或 `.card-video` 触发
- `data-src` 属性指定媒体路径
- 图片需加 `is-image` class
- ESC 或点击背景关闭

### 科研视频组（video-group）
```
科研经历
  └─ project-card (NeRF项目描述)
  └─ video-group "Physgaussian"
       └─ video-thumbs (4列)
            ├─ sofa.mp4
            ├─ sofa_softvib.mp4
            ├─ sofa_strongvib.mp4
            └─ vasedeck.mp4
  └─ video-group "sketch-generative"
       └─ video-thumbs (4列)
            ├─ bike.mp4
            ├─ dolphin.mp4
            ├─ dolphin0.mp4
            └─ sking.mp4
```

### 目录结构
```
media/
  physgaussian/
    sofa.mp4          (1.7MB)
    sofa_softvib.mp4  (1.8MB)
    sofa_strongvib.mp4 (2.2MB)
    vasedeck.mp4      (4.0MB)
  sketch-generative/
    bike.mp4          (32KB)
    dolphin.mp4       (599KB, 已从桌面更新)
    dolphin0.mp4      (46KB)
    sking.mp4         (32KB)
```

## 修改指南

### 添加/修改视频
1. 把视频文件放入 `media/` 对应目录
2. 在 `index.html` 科研部分的 `video-thumbs` 中添加：
```html
<div class="thumb-item">
  <div class="video-thumb" data-src="media/你的目录/你的文件.mp4">
    <video src="media/你的目录/你的文件.mp4#t=0.5" preload="metadata" muted playsinline></video>
    <div class="play-overlay"><span class="play-arrow">▶</span></div>
  </div>
  <div class="thumb-label">显示名称</div>
</div>
```
3. 如果是图片：加 `is-image` class，用 `<img>` 替换 `<video>`
4. 每行4个会自动换行，如需5列给 `video-thumbs` 加 `thumbs-5` class

### 添加项目
复制 `.project-card` 结构，`card-video` 可选。

### 添加奖项
在对应列表中添加 `<li>`：
```html
<li><span class="year">2025.12</span> 奖项名称</li>
```

## 对话历史要点

- 去掉了"实践经历"板块
- 科研经历与项目经历分开（科研1个宽卡片 + 项目2个卡片）
- video-thumbs 从5列改回4列（删掉了 dolphin.png 去重）
- dolphin.mp4 最后一次更新来源：`d:\Users\MR\Desktop\科研\sketch-generative\`
- ▶ 播放图标保留半透明白色圆形样式

## 后续待办
- [ ] 替换头像（当前为占位 ✦ 符号）
- [ ] 替换社交媒体链接（GitHub/B站/邮箱）
- [ ] 填写真实邮箱、联系方式
- [ ] 部署到 GitHub Pages
