# P&L Calendar

本地交易盈亏日历记录工具 — 纯前端、零依赖（除 Tailwind CSS CDN 和 Google Fonts）、数据完全本地存储。

## 功能

- **月度日历视图** — 周日起始，支持上/下月切换，一键回到今天
- **盈亏记录** — 点击工作日日期，弹出 Modal 输入当日 P&L 金额（`$`）和交易备注
- **自动着色** — 盈利绿色、亏损红色、无交易灰色；周末自动置灰不可编辑
- **每周盈亏列** — 日历右侧独立列，显示当周（仅限当前月日期）的累计盈亏
- **当日标记** — 今日日期右上角琥珀色圆点 + 发光圆环，快速定位
- **统计面板** — 本月 / 今年 / 全部总盈亏卡片；高级统计含交易天数、胜率、平均盈利/亏损、盈亏比、最佳/最差日、连续盈亏
- **累计盈亏曲线** — Canvas 手绘折线图，从 0 起点，绿/红色按正负分段着色，零轴跨越精确拆分，仅显示至最后有数据日
- **多账户管理** — 自定义下拉菜单，支持新建、重命名、删除账户，数据完全隔离，刷新后恢复上次账户
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
- [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk)（英文） + [Noto Sans SC](https://fonts.google.com/specimen/Noto+Sans+SC)（中文）
- 图表：Canvas 2D 自绘（无第三方图表库依赖）
- 数据存储：`localStorage`

## 使用方式

直接在浏览器中打开 `index.html` 即可使用，无需安装或构建。

## 数据结构

所有账户数据存储在 `localStorage` 的 `pnlCalendars` 键下：

```json
{
  "默认账户": {
    "2026-05-01": { "pnl": 1250.75, "note": "日内突破交易" },
    "2026-05-02": { "pnl": -450.00, "note": "止损调整不当" }
  },
  "实盘账户": {
    "2026-05-01": { "pnl": 3200.00, "note": "" }
  }
}
```

- `pnlLastAccount` — 记录上次使用的账户名，刷新页面后自动恢复
- `themePreference` — 记录主题偏好（`dark` / `light`）

## 项目结构

```
tradeforge-calendar/
├── index.html            # 主应用文件（内嵌所有 CSS 和 JS）
├── pnl-calendar-spec.md  # 产品规格说明
├── README.md
└── screenshots/
    └── demo.png
```
