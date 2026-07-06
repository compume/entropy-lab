# 熵增实验室架构文档

## 概述

熵增实验室（Entropy Lab）是一个**单 HTML 文件**的物理模拟游戏，核心设计理念是**零依赖、开箱即玩**。所有代码（HTML + CSS + JavaScript）集中在一个文件中，无需构建工具或 npm 依赖。

---

## 核心架构

```
┌─────────────────────────────────────────┐
│            index.html                   │
│  ┌─────────────────────────────────┐    │
│  │  HTML Structure                 │    │
│  │  - home-screen (首页)           │    │
│  │  - level-select-screen (选关)   │    │
│  │  - game-screen (游戏界面)       │    │
│  │  - 各种弹窗模态框               │    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │
│  │  CSS Styles (~400 lines)        │    │
│  │  - 响应式布局（移动端/桌面端）  │    │
│  │  - 暗色主题                     │    │
│  │  - 粒子颜色系统                 │    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │
│  │  JavaScript (~4200 lines)       │    │
│  │  ├── 配置层 (CONFIG)            │    │
│  │  ├── 物理引擎                   │    │
│  │  ├── 渲染系统                   │    │
│  │  ├── 关卡系统                   │    │
│  │  ├── UI 交互                    │    │
│  │  └── 存档系统                   │    │
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

---

## 数据流

```
用户输入 (鼠标/触摸/键盘)
    ↓
事件处理器 (bindEvents)
    ↓
游戏状态更新
    ↓
物理引擎 (updatePhysics) ──→ 粒子位置/速度/温度
    ↓
熵计算 (calcShannonEntropy)
    ↓
渲染 (render) ──→ Canvas 2D
    ↓
胜负判定 (checkWinCondition)
    ↓
UI 更新 (updateEntropyDisplay)
```

---

## 核心模块详解

### 1. 配置层

```javascript
const CONFIG = {
    CELL_SIZE: 4,           // 每格像素大小
    GRID_W: 150,            // 网格宽度（格）
    GRID_H: 125,            // 网格高度（格）
    MAX_PARTICLES: 3000,    // 最大粒子数
    FPS: 60,
    // ...
};
```

### 2. 物理引擎

采用**格子化（Grid-based）**方案，每个格子存储：

| 数组 | 类型 | 说明 |
|------|------|------|
| `grid` | `Uint8Array` | 粒子类型（0=空, 1=沙, 2=气, 3=液, 4=有机物） |
| `velocityX` | `Float32Array` | X 方向速度 |
| `velocityY` | `Float32Array` | Y 方向速度 |
| `temperature` | `Float32Array` | 温度 |
| `barrierGrid` | `Uint8Array` | 隔板（0/1） |

物理更新流程（每帧）：
1. **外力作用**：重力、浮力、搅拌力、热运动
2. **碰撞处理**：粒子-粒子、粒子-隔板
3. **状态更新**：位置、速度、温度
4. **熵计算**：基于粒子分布的香农熵

### 3. 熵计算

```javascript
function calcShannonEntropy(regionData) {
    // 统计各类型粒子数量
    const counts = { sand: 0, gas: 0, liquid: 0, organic: 0 };
    // 计算香农熵: H = -Σ p(x) * log2(p(x))
    let entropy = 0;
    for (const type in counts) {
        const p = counts[type] / total;
        if (p > 0) entropy -= p * Math.log2(p);
    }
    return entropy;
}
```

### 4. 生命核心系统（第二章）

```javascript
let lifeCore = {
    x, y,           // 位置
    energy,         // 能量
    radius: 20,     // 同化半径
    moveSpeed: 0.3  // 移动速度
};
```

- **同化**：将周围粒子转化为"生命"（绿色）
- **消耗**：每帧消耗能量
- **进食**：吃有机物恢复能量
- **排泄**：每吃 2 个有机物排出 3 个沙子

### 5. 红色猎手系统

```javascript
let predator = {
    x, y,
    speed: 0.35,
    trackRadius: Math.hypot(CONFIG.GRID_W, CONFIG.GRID_H),
    killRadius: 8
};
```

- **追踪**：自动追踪生命核心
- **捕食**：接触即杀死生命核心
- **路径**：可被隔板阻挡

---

## 关卡系统设计

```javascript
const CHAPTERS = [
    {
        name: '创世',
        levels: [
            { name: '破界', time: -1, objective: '...', checkWin: (g,a,b) => a > 0.6, initState: 'level1' },
            // ...
        ]
    },
    {
        name: '生命',
        levels: [
            { name: '天启', time: -1, objective: '...', checkWin: (g,a,b) => g > 0.8, initState: 'life_feed' },
            // ...
        ]
    }
];
```

- `time`: `-1` 表示不限时
- `checkWin`: 胜负判定函数（全局熵 g, A区熵 a, B区熵 b）
- `initState`: 初始状态标识符，对应 `setupInitialState()` 中的实现

---

## 扩展指南

### 添加新粒子类型

1. 在 `PARTICLE_TYPES` 中定义常量
2. 在 `TYPE_COLORS` 中定义颜色
3. 在 `updatePhysics()` 中实现运动规则
4. 在 `spawnParticle()` 中确保生成正确
5. 在关卡中通过 `unlockedTools` 控制解锁时机

### 添加新关卡

1. 在 `CHAPTERS` 中追加关卡对象
2. 在 `setupInitialState()` 中实现初始状态
3. 在 `hintTexts` 中添加提示语

---

## 性能优化建议

| 优化方向 | 具体措施 |
|----------|----------|
| 渲染 | 减少 `fillRect` 调用，使用批量绘制 |
| 物理 | 使用 `TypedArray` 操作网格 |
| 熵计算 | 增量计算，避免全量遍历 |
| 内存 | 避免每帧创建临时对象 |

---

## 浏览器兼容性

- **必须支持**：Canvas 2D、ES2020、localStorage
- **推荐浏览器**：Chrome 90+ / Firefox 90+ / Safari 15+ / Edge 90+
- **最低分辨率**：支持 320px 宽度移动端
