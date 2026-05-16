# 联立方程加农炮 · Labrynth Cannons

游戏王（Yu-Gi-Oh）卡牌 **联立方程加农炮（Simultaneous Equation Cannons / SEC）** 的火力计算辅助工具，主要服务于 **拉比林斯（Labrynth）** 卡组玩家。

A firing-aid calculator for the Yu-Gi-Oh card **Simultaneous Equation Cannons (SEC)**, built primarily for **Labrynth** deck users.

**在线使用 / Live:** https://slimpigs.github.io/labrynth-cannons/

---

## 中文

### 这是什么

这张卡的效果可以简化成一个二元一次方程：

- `2X + Y = 场上 + 双方手卡的卡片总数`
- 指定目标怪兽的阶级 / 等级 `= X + Y`
- **效果不是单破怪兽 —— 是横扫对手场上所有的卡。** 选中的怪兽只是用来"对号入座"激活公式的目标。

其中 `X` 是要除外的 Xyz 怪兽的阶级，`Y` 是要除外的融合怪兽的等级，都来自你的额外卡组。

实际效果分两步：

1. **除外阶段**：从额外卡组除外 2 张同阶级的 Xyz（也就是 `X` 的一对）和 1 张融合（`Y`）。
2. **回收阶段**：从已除外卡区返回 1 张 Xyz 和 1 张融合到额外卡组，目标怪兽的阶级 / 等级 = 这两张返回卡的阶级 / 等级之和。当目标成立后，**横扫对手整个场面**。

所以可以选择：
- **默认回收 X+Y**：返回除外的 1 张 `X` 和 1 张 `Y`，结果是 1 张 `X` 留在除外区。
- **代入 C+Y**：返回除外区中其他阶级 `C` 的 Xyz 和这次除外的 `Y`，结果是这一对 `X` 全部留在除外区，但之前除外的 `C` 回到额外卡组。

### 界面布局

整个页面是一屏式 **赛博加农炮终端（Cyber Cannon Terminal）**，分为三栏，不需要滚动：

- **左栏 · 目标瞄准镜（Target Reticle）**：超大 `T` 数字读数 + `−` / `+` 按钮调整。下方是 `T ± 3` 邻近场况预览（可点击跳转）。
- **中栏 · 弹药库（Ammunition Magazine）**：Xyz / 融合芯片库，标题旁有 `↻ 重新装弹` 按钮。
- **右栏 · 开炮方案（Firing Solutions）**：顶部紫色发光的 **当前可摧毁的目标** 胶囊条列出所有可达 `R/L` 数值（每个胶囊 `×N` 标明几种打法，可点击高亮对应方案卡）。下方是可滚动的方案卡列表。当有方案时右栏会发出青色光晕，标题旁出现 `就绪 / READY` 脉冲指示灯。

### 计算器功能

- **总卡数输入**：单一字段，把场上 + 双方手卡总数加在一起即可。**默认开局是 `T = 12`**，可用 `−` `+` 按钮或直接输入调整。
- **当前可摧毁的目标条**：方案区顶部，紫色发光胶囊列出每个可达 R/L 数值。`×N` 表示有几种打法。**点击胶囊会高亮所有命中该目标的方案卡**。
- **弹药库（三状态芯片）**：每个阶级 / 等级一个芯片，点击循环切换：
  - `○` 没有 → `●` 额外卡组（金色，新鲜弹药）→ `⚷` 除外区（紫色，曾经用过）→ 没有。
  - Xyz 默认两个点位（一对），融合默认一个点位（单张）。
- **`↻ 重新装弹` 按钮**：弹药库标题旁。新游戏开始时点一下，把所有阶级 / 等级和总卡数都恢复到默认值（Xyz 3-6 成对、融合 1-6 单张、`T = 12`）。
- **开炮方案**：列出当前 `T` 下所有有效的 `(X, Y)` 组合，每个方案显示主目标 `X+Y` 以及通过除外区代入得到的 `C+Y` 选项。
- **开炮按钮**：每个方案下方一个 `⫸ 开炮` 按钮，点击后自动按照默认情况更新状态（一对中 1 张 X 留在除外区）；点击下方紫色 `C + Y` 胶囊可触发代入开炮（这一对 X 完全除外，但之前除外的 `C` 回到额外卡组）。
- **就绪 / 冷却指示灯**：右栏标题旁。当至少有 1 个方案可用时显示 `就绪`（青色脉冲、FIRE 按钮呼吸光晕）；总卡数 > 0 但无方案时显示 `冷却`（品红色）。
- **邻近场况预览**：左栏底部的 `T ± 3` 表格，每格显示该总数下能开几炮，**点击直接跳到那个 T**。
- **语言切换**：右上角 `EN / 中` 切换中英文，**默认中文**。
- **本地存储**：总卡数、弹药库和语言选择会保存到浏览器 `localStorage`，下次打开自动恢复。

### 使用步骤

1. 打开[计算器页面](https://slimpigs.github.io/labrynth-cannons/)。
2. 新游戏开始时点击弹药库右上角的 `↻ 重新装弹`，把所有状态恢复为默认（弹药库满 + `T = 12`）。第一次打开时已经是这个状态，无需操作。
3. 在 **目标瞄准镜** 用 `−` `+` 或直接输入调整 `T`（场上 + 双方手卡的总数）。
4. 看右栏顶部 **当前可摧毁的目标** 胶囊：当前 `T` 下能命中的所有怪兽 R/L 数值一目了然。点击胶囊高亮对应方案卡。
5. 在方案卡上点击 `⫸ 开炮 · 除外 1 X` 触发默认开炮，或点击下方紫色 `C + Y` 胶囊触发代入开炮，状态会自动更新（弹药数会自动调整）。
6. 如果当前 `T` 没有方案，看 **邻近场况预览** 找邻近能开炮的 `T` 值，点击直接跳过去。

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
- Designated target monster's Rank / Level `= X + Y`
- **The effect doesn't just destroy that monster — it wipes ALL cards on your opponent's field.** The targeted monster is the "key" that satisfies the equation and unlocks the wipe.

Where `X` is the Rank of an Xyz monster you banish and `Y` is the Level of a Fusion monster you banish — both from your Extra Deck.

The actual card effect has two steps:

1. **Banish step:** banish 2 Xyz of Rank `X` (a pair) + 1 Fusion of Level `Y` from your Extra Deck.
2. **Return step:** return 1 Xyz + 1 Fusion from the banished zone to your Extra Deck. The target monster's Rank / Level must equal the sum of those returned cards' Ranks / Levels. Once the target is locked in, **the opponent's entire field is wiped out**.

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

**Non-commercial use only.** This tool is licensed under [Creative Commons Attribution-NonCommercial 4.0 (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/). You may use, modify, and share it freely for personal or community/hobby purposes, but **commercial use is not permitted**. The Yu-Gi-Oh card and Labrynth archetype are trademarks of Konami; this tool is an unofficial fan-made aid and is not affiliated with or endorsed by Konami.

**仅限非商业用途。** 本工具采用 [知识共享 署名-非商业性使用 4.0 国际许可（CC BY-NC 4.0）](https://creativecommons.org/licenses/by-nc/4.0/deed.zh) 授权。可以自由使用、修改、分享，**但不得用于任何商业目的**。游戏王及拉比林斯系列卡片为 KONAMI 公司的注册商标，本工具为非官方玩家自制辅助，与 KONAMI 无任何关联，也未经其认可。
