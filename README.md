---
title: Gravity Homework 7
emoji: 🌍
colorFrom: blue
colorTo: green
sdk: static
pinned: false
---

# 作業 7 · 重力測站資料約化

Gravity Station Data Reduction — 地球物理作業整理。

把一個重力測站的觀測值，經過理論重力、自由空氣修正與布蓋修正，
一步步化成自由空氣異常與布蓋異常；並比較陸地與海面上同一觀測值的差異。

## 內容

- **水彩風格網頁**：[`index.html`](index.html)（單一檔案、無外部依賴）
- **中英對照整理**：[`作業7.md`](作業7.md)
- **原始題目**：[`作業7.png`](作業7.png)
- **專案規則**：[`AGENTS.md`](AGENTS.md)

## 重點結果

| 項目 | (a) 陸地 | (b) 海面 |
| --- | --- | --- |
| 自由空氣異常 | −33.8 mGal | −184.3 mGal |
| 布蓋異常 | −88.4 mGal | −205.4 mGal |

> 數值依 GRS80 正常重力公式、ρ = 2.67 g/cm³、ρ_w = 1.03 g/cm³ 計算，僅供驗算。
