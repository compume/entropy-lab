# 🔬 熵增实验室 | Entropy Lab

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-3.6.9-blue.svg)]()

> 基于**香农熵**的物理模拟游戏，两章十四关，在粒子世界中体验热力学第二定律的奥秘。

---

## 🎮 在线体验

| 平台 | 链接 |
|------|------|
| 🌐 **Cloudflare Pages**（推荐） | 👉 **[点击即玩](https://entropylab.pages.dev/)** |
| 📄 **GitHub Pages** | 👉 [点击即玩](https://compume.github.io/entropy-lab/) |

或本地直接打开 `index.html` —— 零依赖，开箱即玩。

---

## 📸 游戏截图

*（欢迎 PR 补充精美截图 / GIF）*

### 核心玩法
- 操控 **四种粒子**：惰性沙、活性气体、中性液体、有机物
- 使用工具：搅拌、加热、冷却、自由隔板、橡皮擦
- 控制**系统熵值**，完成各种挑战任务
- 第二章引入**生命核心**与**红色猎手**，策略深度升级

---

## 🚀 快速开始

### 方式一：直接打开（推荐）

```bash
# 克隆仓库
git clone https://github.com/compume/entropy-lab.git
cd entropy-lab

# 直接打开
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

### 方式二：本地服务器

```bash
npx serve .
# 浏览器打开 http://localhost:3000
```

### 方式三：VS Code Live Server

安装 [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) 插件，右键 `index.html` → "Open with Live Server"。

---

## 🎮 操作说明

### 工具快捷键

| 快捷键 | 功能 |
|--------|------|
| `1` | 投放惰性沙（灰色） |
| `2` | 投放活性气体（红色） |
| `3` | 投放中性液体（青色） |
| `4` | 搅拌 |
| `5` | 加热 |
| `6` | 冷却 |
| `7` | 自由隔板（按住滑动绘制） |
| `8` | 投放有机物（黄色） |
| `9` | 橡皮擦（擦除隔板） |

### 手势操作（移动端）

- **双指捏合**：缩放画布
- **单指拖动**：平移视图（放大时）或投放粒子
- **上下滑动**：查看控制面板

---

## 📂 项目结构

```
entropy-lab/
├── index.html              # 游戏主入口（单文件，开箱即玩）
├── bgm.mp3                 # 背景音乐（compume 原创）
├── LICENSE                 # MIT 许可证（代码）
├── README.md               # 本文件
├── CONTRIBUTING.md         # 贡献指南
├── CREDITS.md              # 素材版权说明
├── package.json            # 项目元信息
├── .gitignore              # Git 忽略规则
├── docs/
│   └── ARCHITECTURE.md     # 架构文档
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md
    │   └── feature_request.md
    └── PULL_REQUEST_TEMPLATE.md
```

> **设计理念**：单 HTML 文件架构，无需构建工具，零依赖，即开即玩。

---

## 🧬 游戏章节

### 第一章：创世（6 关）
| 关卡 | 名称 | 核心玩法 |
|------|------|----------|
| 1 | 破界 | 搅拌增加 A 区熵值 |
| 2 | 混沌 | 搅拌增加 B 区熵值 |
| 3 | 扩散 | 加热融化隔板 |
| 4 | 交融 | A/B 双区同时达到高熵 |
| 5 | 多元 | 混合多种粒子 |
| 6 | 阅后即焚 | 极高熵挑战 |

### 第二章：生命（8 关）
引入**生命核心**（绿色，以有机物为食）和**红色猎手**（追踪捕食核心）：

| 关卡 | 名称 | 核心玩法 |
|------|------|----------|
| 1 | 天启 | 投喂生命核心 |
| 2 | 围城 | 加热融化牢笼 |
| 3 | 囚笼 | 迷宫逃脱 |
| 4 | 克制 | 精确控制熵值 < 0.5 |
| 5 | 守护 | 用隔板保护生命核心 |
| 6 | 守护 II | 有限隔板（200个）策略防御 |
| 7 | 精准 | 在指定熵区间内猎杀 |
| 8 | 平衡 | 维持熵值区间 20 秒 |

---

## 🏗️ 技术栈

- **渲染**：HTML5 Canvas 2D
- **物理**：自定义粒子物理引擎（格子化 + 速度场）
- **熵计算**：实时香农熵（Shannon Entropy）
- **存档**：localStorage
- **音频**：HTML5 Audio API
- **架构**：单文件 HTML（零依赖）

---

## 🤝 如何贡献

欢迎 Fork、PR、提 Issue！详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

快速贡献方向：
- 🧪 添加新粒子类型
- 🗺️ 设计新关卡
- 🎵 添加音效 / BGM
- ⚡ 性能优化
- 📝 完善文档

---

## 📄 许可证

- **代码**：MIT License —— 详见 [LICENSE](LICENSE)
- **背景音乐** `bgm.mp3`：[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) —— compume 原创，详见 [CREDITS.md](CREDITS.md)
- **其他素材**：Emoji 图标为 Unicode 标准，无版权限制

---

## 🌟 特别说明

- **存档系统**：游戏进度保存在浏览器本地（localStorage），清除浏览器数据会丢失进度
- **音频文件**：`bgm.mp3` 为作者 **compume** 原创音乐，采用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可，详见 [CREDITS.md](CREDITS.md)
- **浏览器兼容**：推荐 Chrome 90+ / Firefox 90+ / Safari 15+ / Edge 90+

---

Made with 💙 and entropy.
