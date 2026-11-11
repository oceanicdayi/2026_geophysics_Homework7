# 專案說明與工作規則 / Project Guide

> 本檔（`AGENTS.md`）是本專案給人與 AI 助理共同遵循的說明書。
> 任何修改、部署或自動化操作前，請先讀完本檔。

---

## 一、專案目標 / Project Goal

把地球物理作業 7（Gravity Station Data Reduction，重力測站資料約化）整理成一份
**清楚、易讀、可公開展示**的成品，並發布到兩個平台：

1. **Hugging Face Space**（靜態網頁展示）
2. **GitHub**（原始碼與版本管理，可搭配 GitHub Pages）

核心要求：

- 內容正確：公式、數值、單位與題意需忠於原題（`作業7.png`）。
- 中英對照：文字以繁體中文為主，保留英文原文與專有名詞。
- 視覺一致：水彩風格、柔和配色、紙張質感，適合閱讀與列印。
- 零依賴：單一 HTML 檔即可開啟，不依賴 CDN、伺服器或建置流程。

---

## 二、檔案角色 / File Roles

| 檔案 | 用途 | 是否可公開 |
| --- | --- | --- |
| `index.html` | 水彩風格成果網頁（主要交付物） | ✅ 可 |
| `作業7.md` | 題目中英對照、說明、公式與知識整理 | ✅ 可 |
| `作業7.png` | 原始題目圖片（內容來源） | ✅ 可（僅 GitHub） |
| `ref/p1.png`、`ref/p2.png` | 手稿插圖（已內嵌於 `index.html`） | ✅ 可（僅 GitHub） |
| `AGENTS.md` | 本說明與規則 | ✅ 可 |
| `.env` | 部署憑證與目標位置 | ❌ **絕對不可** |
| `.gitignore` | 排除機敏與暫存檔 | ✅ 可 |

---

## 三、機敏資料規則 / Secrets Rules（最重要）

`.env` 內含上傳所需資訊，屬於**機敏資料**，只存在本機。

**永久禁止：**

- ❌ 將 `.env` 提交到 Git、推上 GitHub、上傳到 Hugging Face Space。
- ❌ 把 `.env` 的「值」複製到 `index.html`、`作業7.md`、`AGENTS.md`、README、程式碼、註解、log 或截圖。
- ❌ 在指令輸出、終端機訊息或對話中印出 token 全文。
- ❌ 把 token 寫進 Git remote URL（例如 `https://<token>@github.com/...`）。
- ❌ 將 `.env` 改名後上傳（`.env.txt`、`env.md` 等都不行）。

**必須做到：**

- ✅ `.gitignore` 第一行就排除 `.env` 與 `.env.*`。
- ✅ 每次 `git add` 前後都用 `git status` 確認沒有 `.env`。
- ✅ 上傳 Hugging Face 時使用排除規則（`--exclude ".env"`）。
- ✅ 若懷疑憑證外洩，立即到平台撤銷（revoke）並更新 `.env`，不要只刪檔案。
- ✅ 文件中提到憑證時，只寫變數名稱，不寫內容。

### 環境變數（僅列名稱與用途，嚴禁填入值）

| 變數名稱 | 用途 |
| --- | --- |
| `hugging_face_token` | Hugging Face 寫入權限 token |
| `hugging_face_space` | Hugging Face Space 的 repo id（例如 `user/space-name`） |
| `github_token` | GitHub Personal Access Token |
| `github_repo` | GitHub repository（`owner/repo` 或 URL） |

---

## 四、內容規則 / Content Rules

1. **唯一事實來源**：題目文字以 `作業7.png` 為準；`作業7.md` 為整理版；`index.html` 為展示版。
2. **同步修改**：若修正公式、數值或題意，必須同時更新 `作業7.md` 與 `index.html`，不可只改其中一份。
3. **數值標註**：理論重力、修正量與異常值需註明所採公式與假設（GRS80、ρ = 2.67 g/cm³、ρ_w = 1.03 g/cm³）。
4. **單位**：重力一律使用 mGal；高程使用 m；密度使用 g/cm³。
5. **語言**：繁體中文（台灣用語）為主；英文原文、專有名詞與公式保留英文。
6. **不得捏造**：不新增原題沒有的數據；補充說明需標示為「補充」或「參考」。
7. **圖片**：`作業7.png` 為唯讀來源，不得覆寫、裁切或刪除。

---

## 五、網頁規則 / Web Page Rules

1. `index.html` 必須是**單一自足檔案**：
   - 不引用外部 CDN、外部字型、外部 JS。
   - 樣式與裝飾（含水彩暈染、紙張紋理）一律用內嵌 CSS / SVG。
   - 圖片使用相對路徑；若未嵌入，需確保同層檔案存在。
2. 編碼固定 **UTF-8**，`<html lang="zh-Hant">`，包含 `viewport` meta。
3. 必須支援：
   - 桌機（≥ 1024px）與手機（≤ 480px）版面。
   - 列印（`@media print` 關閉背景裝飾）。
   - `prefers-reduced-motion`（關閉漂浮動畫）。
4. 無障礙基本要求：語意化標籤、標題層級正確、裝飾元素 `aria-hidden="true"`。
5. 不得加入追蹤碼、分析腳本、廣告或任何外部請求。
6. 修改後需實際開啟確認：版面無溢出、表格不重疊、公式可讀。

---

## 六、部署規則 / Deployment

### 1. GitHub

- 根目錄即為網站根目錄（`index.html` 在根層）。
- 建議開啟 GitHub Pages：Settings → Pages → Deploy from branch → `main` / `root`。
- 首次推送前檢查：

```bash
git status                 # 確認沒有 .env
git check-ignore -v .env   # 應顯示被 .gitignore 忽略
```

- 提交訊息格式：`feat: ...`、`fix: ...`、`docs: ...`。

### 2. Hugging Face Space（Static SDK）

- Space 類型：**Static**。
- 必要條件：
  - 根目錄需有 `index.html`。
  - 根目錄需有 `README.md`，且包含 YAML front matter：

```yaml
---
title: Gravity Homework 7
emoji: 🌍
colorFrom: blue
colorTo: green
sdk: static
pinned: false
---
```

- 上傳指令（排除機敏檔）：

```bash
hf upload <space_id> . --repo-type space --exclude ".env" --exclude ".git/**" --exclude "作業7.png" --exclude "ref/**"
```

- **二進位檔限制**：Hugging Face 對 binary 檔案改用 Xet 儲存，直接 commit 會被拒絕。
  因此 `作業7.png` 與 `ref/*.png` **只放在 GitHub**；`index.html` 已將手稿插圖以 base64 data URI 內嵌，
  Space 不需要任何圖片檔也能完整顯示。
- 上傳後到 Space 的 **Files** 分頁確認清單中沒有 `.env`。

### 3. 發布前檢查清單 / Pre-release Checklist

- [ ] `git status` 與 Space 檔案清單都沒有 `.env`
- [ ] `index.html` 直接雙擊可正常顯示（斷網亦可）
- [ ] 中英對照與 `作業7.md` 一致
- [ ] 五個子題與 (b) 小題皆有對應說明
- [ ] 表格、公式在手機寬度不溢出
- [ ] 沒有外部網路請求（可用瀏覽器 DevTools → Network 檢查）
- [ ] `作業7.png` 仍在專案中且未被修改

---

## 七、協作方式 / Working Agreement

- AI 助理修改檔案前，先確認是否涉及 `.env`；**一律不得讀取後輸出其內容**（僅可確認鍵名）。
- 不刪除、不覆寫與本次任務無關的檔案。
- 產生暫存檔（截圖、預覽圖）請命名為 `_preview_*` 或 `_crop_*`，並在完成後刪除。
- 任何新增檔案都要在本檔的「檔案角色」表中補列。
- 若指令可能外洩憑證（例如把 token 放在命令列參數），改用環境變數或互動式登入。
