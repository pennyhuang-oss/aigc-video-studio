# AITokenKing 見證影片系列 — 製作架構完整解析記錄

**來源：** https://github.com/firekou/virtual-strategy-lab/tree/main/projects/aitokenking/testimonial-videos  
**解析日期：** 2026-06-25  
**解析者：** Penny（品牌行銷）  
**用途：** 抽象化為「影音製作企劃室」可複用的架構範本

---

## 一、專案概況

| 項目 | 內容 |
|------|------|
| 專案代碼 | ATK-TESTI-001 |
| 類型 | 使用者見證短影片系列（B2B SaaS） |
| 品牌 | AI Token King（aitokenking.com.tw） |
| 集數 | EP.01 ~ EP.06（分批製作） |
| 格式 | 9:16 直式（TikTok / IG / YouTube Shorts）+ 16:9 橫式（LinkedIn） |
| 時長 | 目標 90~120 秒，最長不超過 180 秒 |
| 解析度 | 1080×1920 @ 30fps |
| 音量標準 | -14 LUFS |
| 製作方式 | 全 AIGC（無真人拍攝） |

---

## 二、專案文件結構（GitHub 檔案清單）

```
testimonial-videos/
├── 00-project-overview.md      # 專案總覽、RACI、時程、預算
├── 01-scripts.md               # 5 集完整腳本（旁白稿 + 鏡頭指示）
├── 02-aigc-specs.md            # AIGC 工具鏈、Prompt 庫、成本估算
├── 03-asset-tracker.md         # 素材授權清單
├── 04-qc-report.md             # 各 Gate 品質審核報告
├── 05-publish-tracker.md       # 發布時間與效果追蹤
├── 06-visual-direction.md      # 視覺導演規格書
├── 07-audio-design.md          # 音效設計規格
├── 08-production-log.md        # 每日製作日誌
├── 09-character-bible.md       # 角色聖經（CHAR-01~CHAR-06）
├── 10-scene-design.md          # 場景設計規格
├── 12-aigc-workflow-EP01.md    # EP01 AIGC 生成逐鏡工作流
├── 13~18-notos-production-plan-EP01~05.md  # 各集 Notos 生產計畫
├── 19-ep01-plan-vs-result-gap-analysis.md  # EP01 規劃 vs 成片落差分析
├── 20-witness-video-production-skill.md    # 通用見證影片製作 Skill
├── 21-ep02-production-brief.md # EP02 製作 Brief
├── EP01-storyboard.md          # EP01 分鏡（v2.0 黃金標準）
├── EP01-storyboard-v1.1-as-planned.md      # EP01 原始規劃分鏡（存檔）
├── EP06-character-emotion-profile.md       # EP06 角色情感輪廓
├── EP06-jet-compliance-review.md           # EP06 合規審查
├── meeting-EP01-preproduction-20260517.md  # 前期會議記錄
├── aigc-scripts/               # AIGC 生成腳本目錄
├── assets/                     # 素材目錄
├── coherence/                  # 角色一致性資料
└── output/                     # 輸出成品目錄
```

---

## 三、影片製作架構總流程（5 Phases + 4 QC Gates）

```
Phase 0：專案啟動
  ↓ G0 審核（立案 + 預算確認）
Phase 1：腳本撰寫
  ↓ G1 審核（品質檢核 + 創意總監）
Phase 2：AIGC 素材生成
  ↓ G2 審核（技術規格 + 版權確認）
Phase 3：後期剪輯（字幕 + 特效 + 合成）
  ↓ G3 審核（創意總監 + 品質檢核）
Phase 4：多平台格式輸出 + 最終 QC
  ↓ G4 最終審核（品質得分 ≥ 90 才發布）
發布：各平台上線
```

### Phase 0 — 專案啟動
- 確認四鎖：成片規格、產品真相表、品牌資產表、製作方式
- AIGC 算力成本估算
- RACI 責任矩陣確認
- 預算核決（依金額決定簽核層級）

### Phase 1 — 腳本撰寫
**每集腳本必須包含：**
- 情緒溫度標記（每場景 0~100 值）
- 至少一個可量化的具體改變（金額、時間、人數）
- 主角真實個人動機（非「公司要求」）
- CTA 銜接邏輯（最後 10 秒如何從見證自然引出）

**三段式敘事結構：**
- 第一段（痛點鋪陳，~30~45 秒）：情緒 20 → 65
- 第二段（見證故事核心，~40~80 秒）：情緒 65 → 90
- 第三段（產品展示 + CTA，~20~40 秒）：情緒 90 → 70

### Phase 2 — AIGC 素材生成
**工具鏈：**

| 素材類型 | 主要工具 | 備選工具 |
|---------|---------|---------|
| 靜態場景圖 | Midjourney v7 | DALL-E 3 |
| 圖生動態影片 | Kling AI 2.0 | Wan 2.1 |
| 攝影機運動補間 | Sea Dance 2 | Kling AI（備選）|
| UI 操作動態 | Wan 2.7 | ScreenFlow |
| 文字動畫特效 | After Effects | — |
| AI 背景音樂 | Suno AI | Udio |
| TTS 旁白 | ElevenLabs（繁中）| Azure TTS |
| 口型同步 | HeyGen | — |

**4 個工作流：**
- **工作流 A：Sea Dance 2** — 首尾幀補間（有明確攝影機運動軌跡的鏡頭）
- **工作流 B：Wan 2.7** — UI 操作動態（軟體介面展示鏡頭）
- **工作流 C：Midjourney + Kling AI** — 標準人物採訪鏡頭
- **工作流 D：After Effects** — GFX 動態、品牌動畫、CTA 片尾

**角色一致性（AIGC 人臉鎖定流程）：**
1. 探索性生成 20~30 張候選臉
2. 收斂性精修（從候選臉中選定目標）
3. Fixed Seed 鎖定（Primary + 2 個 Backup）
4. 生成 6 個情緒基準圖（對應不同情緒溫度）
5. ComfyUI + IP-Adapter 掛載（主採訪鏡頭強度 0.88，半身 B-roll 0.82）

### Phase 3 — 後期剪輯
- Kling AI 動態化素材批次生成
- HeyGen 口型同步（SOT 鏡頭）
- After Effects 字幕 + GFX 疊加
- 色溫調色（冷開場 3800K → 中性採訪 5000K → 暖結果段 5500K）
- Suno AI 音樂分段剪接（依情緒段落）

**音樂分段策略：**

| 段落 | 時間點 | Suno Prompt 方向 |
|------|--------|----------------|
| 痛點建立 | 0~30 秒 | subtle tension, minimalist electronic, low tempo |
| 轉折發現 | 30~50 秒 | building curiosity, gentle uplifting, tempo increase |
| 使用產品 | 50~90 秒 | confident modern corporate, steady rhythm |
| 結果收尾 | 90~120 秒 | warm resolution, optimistic, light and clean |

### Phase 4 — 多平台格式輸出

| 平台 | 格式 | 解析度 | 碼率 |
|------|------|--------|------|
| TikTok / IG Reels / YouTube Shorts | MP4 H.264 | 1080×1920 | ≥8 Mbps |
| LinkedIn | MP4 H.264 | 1920×1080 | ≥8 Mbps |

---

## 四、Midjourney 豎屏構圖三大鐵則

> 豎屏不是橫屏裁切，必須從第一個鏡頭就以 9:16 視角構思。

1. **主角永遠在畫面上 1/3**：臉部眼睛落在 Y 軸 576px 以上（1920 高度基準）
2. **字幕在下方 20% 安全區**：字體 ≥52pt，不壓臉部
3. **CTA 最後 10 秒全屏**：深藍底色 #004280，URL 置中 ≥80pt，只有一個動作

**Midjourney 必加豎屏參數：**
```
--ar 9:16 --style raw --v 7
```

**構圖控制語：**
```
subject positioned in upper portion of frame, generous empty lower third
for text overlay, vertical composition optimized for mobile viewing
```

---

## 五、品質驗收標準（QC 四維度）

### 1. CHAR 臉部一致性（三要素測試）
- 下巴輪廓線：臉型不漂移
- 眼鏡框形狀：規格一致
- 鼻樑結構：寬度一致
→ 跨色溫（5000K / 5500K）並排，辨識度 ≥ 80%

### 2. 色溫視覺驗收
- 三段應有視覺差異：深夜藍灰（3800K）→ 採訪中性（5000K）→ 暖白結果段（5500K）
- 並排時能感受到溫度遞升

### 3. Film Grain
- 目標 σ=8~12，暗部可見顆粒，不影響細節辨識
- 若 Midjourney 顆粒不足，After Effects 補加 CC Film Damage

### 4. 品牌一致性（G4 必查）
- 所有畫面內嵌 URL = aitokenking.com.tw（不漏 .tw）
- 所有年份對齊上線年度
- 色碼零容差：背景 #004280、電光藍 #00AAFF

---

## 六、開工前四鎖（見證影片通用 Skill）

> 來自 EP.01 成片 vs 規劃的 40% 落差教訓

### 鎖 1：成片規格
- **比例、時長、fps、平台**，G0 由「真正下指令生產的人」拍板
- EP.01 教訓：規劃假設「9:16 / 130 秒 / 30fps」，成片實際是「16:9 / 78 秒 / 24fps」→ 整份分鏡廢掉

### 鎖 2：產品真相表
開工前必須有：
- 這支片賣什麼（一句話）
- 真實 UI 截圖（非想像）
- 真實定價邏輯
- 真實可用的證明素材

### 鎖 3：品牌資產表
向品牌方取齊：
- 吉祥物用法（EP.01 是柯基戴皇冠浮水印 + 片尾）
- Logo、色票（#004280、#00AAFF）
- 字體規範（Noto Sans TC）
- 網域、slogan、email 格式

### 鎖 4：製作方式
- 全 AIGC / 真人拍攝 / 混合？確認後刪除不適用協定
- EP.01 教訓：決定全 AIGC 後仍保留整套真人採訪流程 → 文件自相矛盾

---

## 七、EP.01 規劃 vs 成片落差分析摘要（四類 35 項）

| 類型 | 數量 | 核心教訓 |
|------|------|---------|
| 【不相符】 | 12 | 9:16→16:9、130s→78s、個人痛點→員工管理、UI 顏色、CTA 底色 |
| 【捨去】 | 8 | S02 手機帳單、S04 混亂動畫、NT$ 金額對比、招牌台詞 |
| 【沒思考到】 | 9 | 品牌吉祥物、真實 UI 長相、真實定位、發票 email、浮水印 |
| 【多講】 | 6 | 14 點情緒數學、逐鏡 IP-Adapter 規格、真人採訪協定（全 AIGC 卻寫）|

**核心洞察：** 成片 90 分，但和規劃只有六成吻合。40% 落差不是執行失誤，是規劃時對「真實產品 / 真實品牌 / 真實規格」認知不足。

---

## 八、RACI 責任矩陣

| 工作項目 | 創意總監 | 編劇 | 影像創作 | 聲音創作 | 後期剪輯 | Vincent（AIGC）| 品質檢核 | 製作統籌 |
|---------|---------|------|---------|---------|---------|----------------|---------|---------|
| 創意方向定案 | R/A | C | C | C | I | C | I | I |
| 腳本撰寫 | C | R/A | I | I | I | I | I | I |
| AIGC 視覺生成 | C | I | R | I | I | R/A | I | I |
| 配樂與音效 | C | I | I | R/A | I | C | I | I |
| 後期剪輯 | C | I | I | I | R/A | I | I | I |
| G1~G4 審核 | A | I | I | I | I | C | R | I |
| 多平台輸出 | I | I | I | I | R/A | C | R | I |
| 進度追蹤 | I | I | I | I | I | I | I | R/A |

---

## 九、預算層級（兌心科技 RACI 決策框架）

| 金額（NT$）| 核決者 |
|-----------|--------|
| ≤ 5,000 | 個別 Agent 自行裁量（L1）|
| 5,001 ~ 50,000 | 部門主管（L2）|
| 50,001 ~ 200,000 | 部門主管 + Jet 連署（L3）|
| > 200,000 | Frank 拍板（L4~L5）|

EP.01 算力成本：NT$4,100~10,530（L1~L2 範圍）  
5 集總預算：≈ NT$52,525（L3，需部門主管 + Jet 連署）

---

## 十、成片可複製的最佳實踐

從 EP.01 成片的加分項（製作端臨場補上，規劃沒寫）：

1. **真實介面截圖 > 抽象 GFX 文字**：Gmail 發票彈窗的說服力遠大於「月結統一發票」標籤
2. **研討會 / 簡報場景**：比「手機搜尋」更自然地帶出產品全貌，且製作感高
3. **全片浮水印吉祥物**：低成本、高記憶點的持續品牌露出
4. **搜尋列打字 CTA**：動態打出網址比靜態大字更有行動暗示
5. **明快剪輯（78 秒）**：B2B SaaS 見證，78 秒對社群完播率可能優於 2 分鐘
6. **數字用「可證明的」**：「便宜 41%」比「從 NT$27,000 降到 NT$16,000」更保險

---

*本記錄基於 GitHub 原始檔案解析，適用於「影音製作企劃室」所有品牌宣傳片製作專案。*
