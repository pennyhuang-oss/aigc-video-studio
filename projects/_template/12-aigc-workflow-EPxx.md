# [品牌代碼]-EP[XX] — AIGC 製作工作流

**Owner：** 視覺創作 / 導演
**狀態：** 製作中
**最後更新：** YYYY-MM-DD

---

## 工作流定義

本企劃室使用四種標準工作流，根據場景類型選用最適合的工具組合：

| 工作流代碼 | 工具組合 | 主要用途 |
|---------|---------|---------|
| Workflow A | Sea Dance 2 | 攝影機運動控制、首末幀插值 |
| Workflow B | Wan 2.7 | UI 動態 / 介面操作展示 |
| Workflow C | Midjourney v7 + Kling AI 2.0 | 圖生影，主要工作流 |
| Workflow D | After Effects | GFX / 字幕 / 後製合成 |

---

## Workflow A — Sea Dance 2 攝影機控制

### 適用情境
- 需要精確攝影機路徑的鏡頭（推進、搖移、環繞）
- 需要首末幀精確控制的場景

### 操作步驟
1. 準備起始幀與結束幀（PNG，1080×1920）
2. 在 Sea Dance 2 設定攝影機路徑：
   - Zoom In：起始幀完整構圖 → 結束幀裁切放大 110%
   - Pan Left/Right：水平位移
   - Static：鎖定不動，僅添加微動態（推薦用於採訪場景）
3. 時長設定：5s / 10s
4. 生成後檢查：攝影機路徑是否符合腳本設計
5. 匯出：MP4，1080×1920，24fps

---

## Workflow B — Wan 2.7 UI 動態

### 適用情境
- S-C 場景：APP 操作介面展示
- 游標移動、按鈕點擊動畫
- 資料填寫、滾動等 UI 行為

### 操作步驟
1. 準備 UI 截圖（1080×1920 PNG）
2. 在 Wan 2.7 上傳截圖
3. 設定動態指令（Text Prompt）：
   ```
   Cursor moves from top to bottom, taps on [元素名稱] button,
   screen transitions to result page, smooth animation, 5 seconds
   ```
4. 動態強度：Low-Medium（避免 UI 元素扭曲）
5. 生成後確認：
   - UI 文字清晰可讀
   - 動態自然（非跳躍）
   - 無多餘添加元素
6. 匯出：MP4，原始解析度，24fps

### Wan 2.7 常用 Prompt 模板
```
Screen recording style, [操作描述], clean UI animation,
professional product demo, no person, no hand, UI only
```

---

## Workflow C — Midjourney + Kling AI 2.0（主要工作流）

### 適用情境
- S-A 採訪場景
- S-B 痛點場景（人物 + 環境）
- S-D 成果場景
- 所有需要「真實人物」的鏡頭

### 完整操作步驟

**步驟一：Midjourney 靜態圖生成**
1. 在 Midjourney 輸入 Prompt（參考 10-scene-design.md 各場景模板）
2. 必填參數：`--ar 9:16 --v 7`
3. 生成 4 張候選圖（U1-U4）
4. 品質確認標準：
   - 景別符合腳本設計（MCU / CU / ECU）
   - 色溫符合場景類型（S-A: 5000K / S-B: 3800K / S-D: 5500K）
   - 主體位於上方 1/3（構圖鐵律）
   - 無水印、無文字
5. 選定最佳圖 → 點擊 Upscale（U1-U4）
6. 儲存為 PNG，命名：`[鏡號]_mj_base.png`

**步驟二：Base Seed 鎖定（S-A 採訪場景必做）**
1. 選定主採訪場景基準圖後，取得 Seed 值
2. 方法：對機器人回覆的圖片點擊「添加反應」→ ✉ → 查看 Job ID → 使用 `/show` 命令取得 Seed
3. 記錄 Seed 值（格式：4 位整數，例：2847）
4. 後續同角色鏡頭均使用 `--seed [數值]` 確保角色一致性

**步驟三：Kling AI 2.0 圖生影**
1. 登入 Kling AI → Image to Video
2. 上傳步驟一的 PNG 圖
3. 參數設定：
   - Duration：5s（標準鏡頭）或 10s（長鏡頭）
   - Motion Intensity：3-5（中等，避免形變）
   - Camera Movement：根據腳本鏡頭指示
     - `zoom in`：緩慢推進
     - `pan left / pan right`：水平搖移
     - `static`：輕微呼吸感，幾乎靜止
     - `tilt up`：向上傾斜
4. Prompt（可選）：補充動態方向，例如 `subtle natural breathing, slight blink, authentic documentary feel`
5. 生成後品質確認：
   - 主體無明顯形變（手指、五官）
   - 色溫與靜態圖一致
   - 無 Kling 浮水印
   - 動態自然，非機械感

**步驟四：Return Last Frame（跨鏡頭連貫）**
1. 播放生成的影片至最後一幀
2. 截圖儲存（命名：`[鏡號]_last_frame.png`）
3. 作為下一個同場景鏡頭的起始幀
4. 詳細規格參考：10-scene-design.md → Return Last Frame 章節

**步驟五：素材匯整**
1. 所有生成影片移至 `_assets/video/raw/` 目錄
2. 命名格式：`[集數]_[鏡號]_v[版本號].mp4`
   例：`ep01_S03-01_v1.mp4`
3. 更新鏡頭-工具對照表（見下方）

---

## Workflow D — After Effects 後製合成

### 適用情境
- GFX：數字動畫、統計圖表
- 字幕：下方 20% 區域
- 轉場特效
- Logo 動態
- Film Grain 添加（S-D 場景）

### AE 合成規格
| 項目 | 規格 |
|------|------|
| 解析度 | 1080×1920 px |
| 幀率 | 24fps |
| 色彩空間 | sRGB |
| 工作色彩 | 8-bit（標準版），16-bit（精品版）|
| 字幕字體 | [品牌指定字體]，備援：Noto Sans TC |
| 字幕大小 | 42-48pt |
| 字幕位置 | 底部 20% 區域，水平置中 |

### GFX 數字動畫標準參數
```
數字從 0 → 目標值
動畫時長：1.5-2 秒
緩動曲線：Ease Out（快速接近終值，最後 20% 慢速完成）
字型：Bold，顏色：品牌主色
背景：半透明黑色遮罩（可選）
```

---

## 鏡頭-工具對照表

> 此表由 PM 在製作前填入，製作人員按表執行

| 鏡號 | 場景類型 | 工作流 | 工具 | 預計時長 | 腳本描述 | 負責人 | 狀態 |
|------|---------|-------|------|---------|---------|-------|------|
| S01 | S-B | C | MJ v7 → Kling 2.0 | 5s | 深夜帳單 ECU | Vincent | ⬜ 待執行 |
| S02 | S-B | C | MJ v7 → Kling 2.0 | 5s | 疲憊主角 CU | Vincent | ⬜ 待執行 |
| S03 | S-A | C | MJ v7 → Kling 2.0 | 8s | 主角採訪 MCU | Vincent | ⬜ 待執行 |
| S04 | GFX | D | After Effects | 3s | 數字動畫 | AE 剪輯 | ⬜ 待執行 |
| S05 | S-C | B | Wan 2.7 | 5s | UI 介面展示 | Vincent | ⬜ 待執行 |
| S06 | S-A | C | MJ v7 → Kling 2.0 | 6s | 採訪持續 MCU | Vincent | ⬜ 待執行 |
| S07 | S-C | B | Wan 2.7 | 5s | UI 操作細節 | Vincent | ⬜ 待執行 |
| S08 | S-C | D | After Effects | 4s | UI + 數字合成 | AE 剪輯 | ⬜ 待執行 |
| S09 | S-D | C | MJ v7 → Kling 2.0 | 6s | 成果展示 MCU | Vincent | ⬜ 待執行 |
| S10 | S-D | C | MJ v7 → Kling 2.0 | 5s | 滿意表情 CU | Vincent | ⬜ 待執行 |
| S11 | S-D | C | MJ v7 → Kling 2.0 | 5s | 品牌尾板場景 | Vincent | ⬜ 待執行 |

**狀態符號：**
- ⬜ 待執行
- 🔄 製作中
- ✅ 完成
- ❌ 重做

---

## 逐日製作時程（7 工作天模板）

| 日期 | 工作項目 | 輸出物 | 負責人 | 完成條件 |
|------|---------|--------|-------|---------|
| Day 1 | S-A 場景 MJ 生成，選定 Base Seed，鎖定 CHAR-XX | S03 基準圖 x5 張，Seed 值記錄 | Vincent | Seed 已記錄，構圖通過 PM 確認 |
| Day 2 | S-B 場景 MJ 生成 + Kling 動態化 | S01, S02 影片素材 | Vincent | 無形變，色溫 3800K 確認 |
| Day 3 | S-D 場景 MJ 生成 + Kling 動態化 | S09, S10, S11 影片素材 | Vincent | Film Grain 確認，色溫 5500K |
| Day 4 | S-C 場景 Wan 2.7 / AE 合成 | S05, S07 UI 素材，S08 合成 | Vincent + AE | UI 文字可讀，無扭曲 |
| Day 5 | S-A 採訪段 Kling 動態化 + Return Last Frame | S03, S06 影片素材 | Vincent | 角色一致，Last Frame 已截取 |
| Day 6 | 音樂（Suno AI）+ 旁白（ElevenLabs） | 音樂主檔，旁白 WAV，品牌 Stinger | 聲音創作 | 通過 07-audio-design.md 規格 |
| Day 7 | AE 初剪合成，字幕，色溫調整 | 初版影片（版本 A + B） | AE 剪輯 | 通過 QC 清單，送導演審閱 |

---

## 品質驗收標準

### 技術規格（硬性標準，不得妥協）
| 項目 | 標準 |
|------|------|
| 影片解析度 | 1080×1920 px（9:16）|
| 幀率 | 24fps |
| 無水印 | 0 個浮水印 |
| 主體形變 | 輪廓偏移 < 10px |
| 色溫偏差 | 同場景跨鏡頭 < 200K |
| Film Grain | S-D 場景必加 σ=8~12 |
| 音量 | -14 LUFS（最終輸出）|
| 字幕安全區 | 下方 20%，不壓主體 |

### 視覺一致性（主觀評分）
| 項目 | 最低要求 |
|------|---------|
| 角色一致性 | 同一角色跨鏡頭識別度 ≥ 90% |
| 情緒弧線 | S-B 低點 → S-D 高點明顯可感受 |
| 品牌感 | 色調統一，非拼湊感 |
| 完播衝動 | 前 5 秒必須有「繼續看下去」的衝動 |

### 審核流程
1. **G1 素材審核**：製作人員自審 → 提交 PM
2. **G2 一致性驗證**：執行 `coherence/` 目錄下的自動化驗證腳本
3. **G3 導演最終審核**：導演確認整體敘事節奏
4. **G4 品牌負責人確認**：確認品牌形象符合期望
5. **G5 發布準備**：音量標準化，按平台規格輸出

---

## 常見問題處理

### 問題：Kling 生成的主角形變嚴重
**解法：**
1. 降低 Motion Intensity 至 2-3
2. 改用 `static` 攝影機設定
3. 重新生成 Midjourney 基礎圖（選更「穩定」的構圖）

### 問題：跨鏡頭角色差異太大
**解法：**
1. 確認使用了相同的 Seed 值
2. 增加 Prompt 中角色描述的具體性（髮色、服裝、表情）
3. 使用 Return Last Frame 技術銜接

### 問題：Wan 2.7 UI 文字扭曲
**解法：**
1. 降低動態強度
2. 改用靜態 UI 截圖 + AE 手動添加動態
3. 僅動態化背景，UI 主體保持靜態

### 問題：色溫不一致
**解法：**
1. 在 AE 使用「色相/飽和度」或「曲線」調整
2. 批次應用同一個 LUT 統一色調
3. 根本解：在 Midjourney Prompt 中明確標注色溫數值（5000K / 3800K 等）
