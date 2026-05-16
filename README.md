# 联立方程加农炮 · Labrynth Cannons

游戏王（Yu-Gi-Oh）卡牌 **联立方程加农炮（Simultaneous Equation Cannons / SEC）** 的火力计算辅助工具，主要服务于 **拉比林斯（Labrynth）** 卡组玩家。

A firing-aid calculator for the Yu-Gi-Oh card **Simultaneous Equation Cannons (SEC)**, built primarily for **Labrynth** deck users.

**在线使用 / Live:** https://slimpigs.github.io/labrynth-cannons/

---

## 中文

### 这是什么

这张卡的效果可以简化成一个二元一次方程：

- `2X + Y = 场上 + 双方手卡的卡片总数`
- 目标怪兽的阶级 / 等级 `= X + Y`

其中 `X` 是要除外的 Xyz 怪兽的阶级，`Y` 是要除外的融合怪兽的等级，都来自你的额外卡组。

实际效果分两步：

1. **除外阶段**：从额外卡组除外 2 张同阶级的 Xyz（也就是 `X` 的一对）和 1 张融合（`Y`）。
2. **回收阶段**：从已除外卡区返回 1 张 Xyz 和 1 张融合到额外卡组，被破坏的怪兽阶级 / 等级 = 这两张返回卡的阶级 / 等级之和。

所以可以选择：
- **默认回收 X+Y**：返回除外的 1 张 `X` 和 1 张 `Y`，结果是 1 张 `X` 留在除外区。
- **代入 C+Y**：返回除外区中其他阶级 `C` 的 Xyz 和这次除外的 `Y`，结果是这一对 `X` 全部留在除外区，但之前除外的 `C` 回到额外卡组。

### 计算器功能

- **场况输入**：场上卡数、己方手卡、对手手卡，下方实时显示总数 `T`。
- **弹药库**：每个阶级 / 等级一个芯片，三状态循环：
  - `○` 没有 → `●` 额外卡组（金色，新鲜弹药）→ `⚷` 除外区（紫色，曾经用过）→ 没有。
  - Xyz 默认两个点位（一对），融合默认一个点位（单张）。
- **开炮方案**：列出当前 `T` 下所有有效的 `(X, Y)` 组合，每个方案显示主目标 `X+Y` 以及通过除外区代入得到的 `C+Y` 选项。
- **开炮按钮**：每个方案下方有一个 `⫸ 开炮` 按钮，点击后自动按照默认情况更新状态；点击代入 `C+Y` 选项可触发代入开炮（除外区的 `C` 会回到额外卡组）。
- **假设场况微调**：快速按钮加减场上 / 手卡数；下方的 `T ± 3` 表格可点击直接跳转。
- **语言切换**：右上角 `EN / 中` 切换中英文。
- **本地存储**：场况、弹药库和语言选择会保存到浏览器 `localStorage`，下次打开自动恢复。

### 使用步骤

1. 打开[计算器页面](https://slimpigs.github.io/labrynth-cannons/)。
2. 在 **弹药库** 区域确认你的额外卡组：默认是 Xyz 阶级 3、4、5、6（成对）+ 融合等级 1-6（各 1 张），可点击芯片调整。
3. 在 **场地与手卡** 区域输入当前场况。
4. 查看 **开炮方案** 列表：每张方案卡显示要除外的 Xyz 和融合，以及可以摧毁的目标阶级 / 等级。
5. 选择一个方案点击 `⫸ 开炮 · 除外 1 X`，或点击下方的 `C + Y` 代入选项，状态会自动更新。
6. 如果当前场况没有方案，看 **假设场况微调** 区域：哪些场况 `T ± 3` 下能开炮。

### 技术细节

- **单文件**：整个工具就是一个 HTML 文件（包含 CSS 和 JS），托管在 GitHub Pages。
- **零网络请求**：除了字体（Google Fonts），所有计算都在你的浏览器里完成。
- **零遥测**：没有任何分析、追踪、上报。
- **本地存储**：用 `localStorage` 记忆你的设置，可以随时清除浏览器数据来重置。

### 设计说明

UI 主题为 **赛博加农炮（Cyber Cannon HUD）**，深蓝钢铁面板配霓虹色能量（青色 = 新鲜弹药、品红 = 目标 / 开炮、紫色 = 除外区 / 代入）。字体使用 Orbitron（标题）+ Rajdhani（正文）+ JetBrains Mono（数字），呈现战术指挥屏风格。

---

## English

### What this is

The Yu-Gi-Oh card **Simultaneous Equation Cannons** boils down to a system of two equations:

- `2X + Y = total cards on the field and in both players' hands`
- Destroyed monster's Rank / Level `= X + Y`

Where `X` is the Rank of an Xyz monster you banish and `Y` is the Level of a Fusion monster you banish — both from your Extra Deck.

The actual card effect has two steps:

1. **Banish step:** banish 2 Xyz of Rank `X` (a pair) + 1 Fusion of Level `Y` from your Extra Deck.
2. **Return step:** return 1 Xyz + 1 Fusion from the banished zone to your Extra Deck, then destroy a monster on the field whose Rank or Level equals the sum of the returned cards' Ranks / Levels.

So you can choose:
- **Return X+Y (default):** return the freshly banished `X` and `Y`. Net effect: 1 copy of `X` stays banished.
- **Substitute with C+Y:** return a different banished `C` (an Xyz of a different rank already in your banished zone) plus this firing's `Y`. Net effect: the entire pair of `X` stays banished, BUT the previously-banished `C` migrates back to Extra Deck.

### Calculator features

- **Field state input:** field count, your hand, opponent's hand. Total `T` is shown live.
- **Ammo pool:** one chip per rank / level, three-state cycle:
  - `○` not owned → `●` Extra Deck (gold pip, fresh ammo) → `⚷` Banished (purple pip, spent once) → not owned.
  - Xyz defaults to 2 pips (a pair); Fusion defaults to 1 pip (a single).
- **Firing solutions:** lists every valid `(X, Y)` pair for the current `T`, each card shows the primary `X+Y` target plus any `C+Y` substitutions enabled by your banished zone.
- **Fire button:** every solution card has a `⫸ FIRE` button that applies the default state change; substitution pills `C+Y` are also clickable to apply that variant (the X pair fully banishes, C migrates back to Extra).
- **What-if fluctuations:** quick buttons to nudge field/hands by ±1; the `T ± 3` adjacency grid is click-to-jump.
- **Language toggle:** top-right `EN / 中` switches between English and Chinese.
- **Local storage:** field state, ammo pool, and language all persist in `localStorage` across sessions.

### How to use

1. Open the [calculator page](https://slimpigs.github.io/labrynth-cannons/).
2. In the **Ammo pool** section, confirm your Extra Deck — defaults are Xyz ranks 3, 4, 5, 6 (paired) + Fusion levels 1–6 (single). Click chips to adjust.
3. Enter the current field state in **Field & Hands**.
4. Read the **Firing solutions** list: each card shows what you'll banish + what you can destroy.
5. Pick a solution and click `⫸ FIRE · BANISH 1 X` for the default, or click a `C + Y` substitution pill for the substitution variant. State updates automatically.
6. If no solutions exist for your current state, check **What-If Fluctuations** to see which `T ± 3` totals could fire.

### Technical details

- **Single file:** the entire tool is one self-contained HTML file (with inline CSS and JS), served via GitHub Pages.
- **Zero network requests:** apart from Google Fonts, every computation runs locally in your browser.
- **Zero telemetry:** no analytics, no tracking, no callbacks.
- **Local storage:** browser `localStorage` persists your settings — clear your browser data to reset.

### Design notes

Theme is **Cyber Cannon HUD** — deep navy steel panels with neon energy accents (cyan = fresh ammo, magenta = target / firing, purple = banished / substitution). Fonts: Orbitron (display) + Rajdhani (body) + JetBrains Mono (numbers), evoking a tactical command readout.

---

## License / 许可

MIT — do whatever you want, including commercial use. The Yu-Gi-Oh card and Labrynth archetype are trademarks of Konami; this tool is an unofficial fan-made aid.

MIT 许可 — 随意使用，包括商业用途。游戏王及拉比林斯系列卡片为 KONAMI 公司的注册商标，本工具为非官方玩家自制辅助。
