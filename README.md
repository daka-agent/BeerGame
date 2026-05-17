# 🍺 供应链啤酒游戏 — 牛鞭效应模拟器

> **Beer Distribution Game** — An interactive web simulation of the bullwhip effect in supply chains.

[![GitHub Pages](https://img.shields.io/badge/Play%20Online-GitHub%20Pages-blue?logo=github)](https://daka-agent.github.io/BeerGame/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🎮 在线游玩

**👉 [https://daka-agent.github.io/BeerGame/](https://daka-agent.github.io/BeerGame/)**

无需安装任何软件，打开浏览器即可游玩。

---

## 🌟 游戏简介

**啤酒游戏（Beer Distribution Game）** 是由 MIT 斯隆管理学院开发的经典供应链管理模拟游戏，用于直观演示**牛鞭效应（Bullwhip Effect）**的形成机制。

游戏模拟一条由 4 个角色组成的供应链：

```
消费者 → 零售商 → 批发商 → 分销商 → 工厂
```

消费者需求仅在第 5 回合发生一次小幅跳变（4→8 单位），但这一微小扰动经过供应链层层传导后，会在工厂端引发巨大的订单波动，形成典型的牛鞭效应。

---

## ✨ 功能特色

| 功能 | 说明 |
|------|------|
| 🎯 **单机模式** | 玩家控制任意一个角色，其余由 AI（Order-Up-To 策略）自动决策 |
| 👥 **多人模式** | 同一台电脑上，多个标签页各自控制一个角色，通过 BroadcastChannel 实时同步 |
| 📊 **实时图表** | 每回合更新库存趋势、订单趋势、累计成本折线图（Chart.js） |
| 📋 **游戏总结** | 游戏结束后展示牛鞭系数、总成本排名、角色对比柱状图 |
| 🔔 **需求预警** | 消费者需求发生变化时，实时弹出通知提醒玩家 |

---

## 🕹️ 如何游玩

### 单机模式
1. 打开游戏页面，点击 **"开始单机游戏"**
2. 选择你想扮演的角色（零售商 / 批发商 / 分销商 / 工厂）
3. 每回合查看当前库存、缺货量、收到的订单
4. 在输入框填写本回合的订货量，点击 **"提交订单"**
5. 其余角色由 AI 自动完成，回合自动推进
6. 共 36 个回合，游戏结束后查看总结报告

### 多人模式
1. 第一个玩家打开游戏，点击 **"创建房间"** 并选择角色
2. 将房间号分享给其他玩家（同一台电脑，新标签页打开游戏）
3. 其他玩家输入房间号 **"加入房间"** 并选择角色
4. 所有角色就位后，房主点击 **"开始游戏"**
5. 每回合所有玩家同时提交订单，全部提交后自动进入下一回合

---

## 📐 游戏参数

| 参数 | 值 | 说明 |
|------|-----|------|
| 总回合数 | 36 | 标准游戏长度 |
| 初始库存 | 12 | 每个角色初始库存量 |
| 在途库存 | 4 | 初始在途（已发货未到达）量 |
| 持有成本 | ¥0.5/单位/回合 | 库存积压成本 |
| 缺货成本 | ¥1.0/单位/回合 | 订单积压成本 |
| 补货前置期 | 2 回合 | 下单到收货的延迟 |
| 消费者需求 | 第1-4回合: 4；第5+回合: 8 | 触发牛鞭效应的需求跳变 |

---

## 🧮 AI 决策策略

AI 角色采用 **Order-Up-To（目标库存）** 策略：

```
order = max(0, targetInventory - currentInventory + backlog - inPipeline)
```

其中需求预测使用指数平滑法（α = 0.3）：

```
forecastDemand = α × actualDemand + (1 - α) × forecastDemand
```

---

## 📊 牛鞭系数

游戏结束后自动计算每个角色的**牛鞭系数（Bullwhip Ratio）**：

```
BullwhipRatio(i) = Var(角色i的订单量) / Var(消费者需求)
```

系数越大，说明该角色放大需求波动的程度越高。

---

## 🛠️ 技术栈

- **纯前端单文件**：HTML + CSS + JavaScript（无需后端、无需安装）
- **图表库**：[Chart.js 4.4](https://www.chartjs.org/)（CDN 加载）
- **多人通信**：[BroadcastChannel API](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel)（同设备多标签页）

---

## 📚 参考文献

- Sterman, J. D. (1989). *Modeling managerial behavior: Misperceptions of feedback in a dynamic decision making experiment.* Management Science, 35(3), 321-339.
- Lee, H. L., Padmanabhan, V., & Whang, S. (1997). *The Bullwhip Effect in Supply Chains.* Sloan Management Review.

---

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源协议。

---

*由 WorkBuddy AI 辅助开发 · 供应链管理教学工具*
