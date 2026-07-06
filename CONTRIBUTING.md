# Contributing to Entropy Lab

欢迎贡献！🧬 感谢你对熵增实验室的兴趣。

## 🚀 快速开始

```bash
# 1. Fork 本仓库（点击右上角 Fork 按钮）
# 2. 克隆你的 fork
git clone https://github.com/YOUR_NAME/entropy-lab.git
cd entropy-lab

# 3. 直接用浏览器打开即可游玩
open index.html
# 或启动本地服务器：
npx serve .
```

---

## 🎯 我想贡献…

### 添加新粒子类型

当前游戏支持四种粒子：惰性沙、活性气体、中性液体、有机物。

如需添加新粒子：

1. 在 `index.html` 的 `PARTICLE_TYPES` 中添加新类型常量
2. 在 `TYPE_COLORS` 中定义颜色
3. 在物理更新循环 `updatePhysics()` 中实现该粒子的运动规则
4. 在 `spawnParticle()` 中确保生成逻辑正确
5. 在关卡数据 `CHAPTERS` 中为新粒子设计解锁关卡

### 添加新关卡

1. 在 `CHAPTERS` 数组中追加关卡对象
2. 在 `setupInitialState()` 中实现新的初始状态
3. 在 `hintTexts` 中添加关卡提示语
4. 设计独特的通关条件和工具限制

### 优化性能

- 优先优化 `gameLoop()` 和 `updatePhysics()` 中的热点代码
- 使用 `Uint8Array` / `Float32Array` 操作网格数据
- 避免在循环中创建临时对象
- 如需对比性能，请提供 before/after 数据

### 添加音效 / 音乐

- 音频文件放入项目根目录（参考现有 `bgm.mp3`）
- 使用 `Audio` API 或 Web Audio API 实现
- 确保音频文件版权清晰或原创
- 更新 `CREDITS.md` 注明来源和许可证

### 修复 Bug

- 先搜索 Issue，确认是否已有相关报告
- 提供复现步骤、浏览器版本、操作系统
- 如可能，附上截图或录屏

---

## 📋 Pull Request 规范

- [ ] 代码在本地浏览器中测试通过（`open index.html`）
- [ ] 移动端触摸操作正常
- [ ] 新功能附带截图或录屏
- [ ] 修改了关卡数据请在 PR 描述中说明设计意图
- [ ] 性能优化请提供 before/after 数据（如帧率、粒子数上限）

### PR 标题格式

```
[类型] 简短描述

# 示例：
[feat] 添加等离子体粒子类型
[fix] 修复移动端缩放异常
[perf] 优化物理计算性能
[level] 新增第3章：量子世界
[docs] 更新 README 截图
```

---

## 🎮 开发提示

### 单文件架构说明

本项目刻意保持**单 HTML 文件**架构，核心优势：
- **开箱即玩**：无需构建工具，直接打开 `index.html`
- **零依赖**：不依赖 npm/webpack/vite 等工具链
- **易于分发**：单个文件即可分享

如需重构为模块化结构，请先在 Issue 中讨论。

### 核心代码位置

| 功能 | 代码区域 |
|------|----------|
| 游戏配置 | `const CONFIG = {...}` |
| 粒子类型 | `const PARTICLE_TYPES = {...}` |
| 关卡数据 | `const CHAPTERS = [...]` |
| 物理引擎 | `updatePhysics()` 函数 |
| 渲染循环 | `gameLoop()` 函数 |
| 存档系统 | `loadProgress()` / `saveProgress()` |

### 浏览器兼容性

- 目标浏览器：Chrome 90+ / Firefox 90+ / Safari 15+ / Edge 90+
- 必须支持：Canvas 2D、ES2020、localStorage

---

## 💬 交流方式

- **Issue**：Bug 报告、功能建议、问题讨论
- **Discussions**：创意分享、玩法讨论、社区作品展示

---

再次感谢你的贡献！🎉
