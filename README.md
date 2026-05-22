# P&L Calendar

本地交易盈亏日历记录工具 — 纯前端、零依赖（除 Tailwind CSS CDN 和 Google Fonts）、数据完全本地存储。

## 功能

- **月度日历视图** — 周日起始，支持上/下月切换，一键回到今天
- **盈亏记录** — 点击工作日日期，弹出 Modal 输入当日 P&L 金额（`$`）和交易备注
- **自动着色** — 盈利绿色、亏损红色、无交易灰色；周末自动置灰不可编辑
- **每周盈亏列** — 日历右侧独立列，显示当周（仅限当前月日期）的累计盈亏
- **当日标记** — 今日日期右上角琥珀色圆点 + 发光圆环，快速定位
- **统计面板** — 本月 / 今年 / 全部总盈亏卡片；可自定义目标盈利金额
- **高级统计** — 交易天数、胜率、盈亏比、盈利因子、恢复因子、每日期望、最大回撤、平均盈利/平均亏损
- **累计盈亏曲线** — Canvas Catmull-Rom 平滑曲线，从 0 起点，绿/红色按正负分段着色，霓虹发光效果，悬停交互；前置无数据区间颜色跟随首个数据日盈亏
- **初始资金** — 可设置初始资金金额，支持锁定/解锁输入框，实时预览当前总资金
- **多账户管理** — 支持新建、重命名、删除账户；账户状态标记（Active 活跃 / Breached 爆仓），状态圆点一目了然；统一编辑弹窗一站式管理名称与状态；Active 账户优先排列
- **智能月份定位** — 切换账户或刷新页面时，自动跳转到该账户最近有盈亏记录的月份
- **主题切换** — 暗色 / 亮色双主题，一键切换，适配所有 UI 元素和图表
- **清空本月** — 一键清除当前月数据，自定义确认弹窗
- **导入 / 导出** — JSON 格式备份与恢复（按账户导出）
- **键盘操作** — `←` `→` 切换月份，`Esc` 关闭弹窗，`Enter` 保存
- **响应式设计** — 桌面优先，移动端友好

## 截图

![P&L Calendar 界面截图](screenshots/demo.png)

## 技术栈

- HTML + CSS + JavaScript（ES6+）
- [Tailwind CSS](https://tailwindcss.com/)（Play CDN）
- [Recursive](https://fonts.google.com/specimen/Recursive)（英文） + [Noto Sans SC](https://fonts.google.com/specimen/Noto+Sans+SC)（中文）
- 图表：Canvas 2D 自绘（无第三方图表库依赖）
- 数据存储：`localStorage`

## 使用方式

直接在浏览器中打开 `index.html` 即可使用，无需安装或构建。

## 数据结构

所有账户数据存储在 `localStorage` 的 `pnlCalendars` 键下：

```json
{
  "默认账户": {
    "status": "Active",
    "_initialBalance": 10000.00,
    "_initialBalanceLocked": true,
    "_profitTarget": 5000.00,
    "2026-05-01": { "pnl": 1250.75, "note": "日内突破交易" },
    "2026-05-02": { "pnl": -450.00, "note": "止损调整不当" }
  },
  "实盘账户": {
    "status": "Breached",
    "2026-05-01": { "pnl": 3200.00, "note": "" }
  }
}
```

- `status` — 账户状态：`"Active"`（活跃）或 `"Breached"`（爆仓），不参与盈亏统计
- `_initialBalance` — 初始资金金额
- `_initialBalanceLocked` — 初始资金是否锁定（锁定后输入框不可编辑）
- `_profitTarget` — 目标盈利金额
- `pnlLastAccount` — 记录上次使用的账户名，刷新页面后自动恢复
- `themePreference` — 记录主题偏好（`dark` / `light`）

## 项目结构

```
tradeforge-calendar/
├── index.html            # 主应用文件（内嵌所有 CSS 和 JS）
├── pnl-calendar-spec.md  # 产品规格说明，可让AI编程通过该文件尽可能复原本项目，视不同的AI情况不同
├── README.md
└── screenshots/
    └── demo.png
```
