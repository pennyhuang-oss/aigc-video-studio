# AIGC 工具鏈規格

---

## 工具一覽

| 素材類型 | 主要工具 | 備選 | 選擇理由 |
|---------|---------|------|---------|
| 靜態場景圖 | Midjourney v7 | DALL-E 3 | 品質最穩定，豎屏 `--ar 9:16` 支援完整 |
| 圖生動態 B-roll | Kling AI 2.0 | Wan 2.1 | 動態自然，攝影感強 |
| 攝影機運動補間 | Sea Dance 2 | Kling AI（備選）| 起終點受控，不像 Kling 隨機詮釋 |
| UI 操作動態 | Wan 2.7 | ScreenFlow | 讓靜態 Mockup「像真人在操作」 |
| GFX + 字幕 | After Effects + Motion Bro | — | 品牌字幕標準化 |
| AI 背景音樂 | Suno AI | Udio | 免版稅，分段情緒生成 |
| TTS 旁白 | ElevenLabs（繁中）| Azure TTS | 台灣腔調自然度最高 |
| 口型同步 | HeyGen | — | 繁體中文優化 |
| 角色一致性 | ComfyUI + IP-Adapter | — | Fixed Seed 人臉鎖定 |

---

## 四個工作流

### 工作流 A：Sea Dance 2（首尾幀補間）

**適用條件：** 鏡頭有明確攝影機運動（TILT / PUSH / PULL），起終點可定義為兩張靜態圖。

**流程：**
1. Midjourney 生成起始幀（相同 Fixed Seed）
2. Midjourney 生成結束幀（相同 Fixed Seed）
3. Sea Dance 2 輸入兩幀，設定運動類型 + 強度 + 速度曲線
4. 生成 3 個候選，選最佳

**常用運動類型：**
- Tilt Up（垂直仰角）
- Push In（垂直軸推進）
- Very Subtle Push In（微推）

**強度建議：**
- 深夜靜謐場景：0.3~0.4（低）
- 情緒轉折段：0.35~0.45（中低）
- 情感高峰段：0.25~0.35（極慢推）

---

### 工作流 B：Wan 2.7（UI 操作動態）

**適用條件：** 鏡頭內容是軟體介面展示，需要模擬游標移動 / 點擊 / 滑桿操作。

**UI 截圖要求（向工程師 / 設計師取得）：**
- PNG，無壓縮
- 9:16 豎屏比例，或能裁切為 1080×1920
- 去識別化（使用 Mock-up 數字）
- 游標在起點靜止狀態

**Action Prompt 寫法要點：**
- 描述操作的「節奏和意圖」，不只是動作本身
- 加入真人操作的「猶豫感」：cursor slows down near target, pauses for 0.5s as if deciding
- 有目的感：deliberately moves toward [element] as if this number is significant

**五要素判斷生成結果：**
1. 游標移動有猶豫感（非等速直線）
2. 目標附近有確認停頓（0.3~0.8 秒）
3. 點擊有「按下 + 回彈」視覺感
4. 滑桿拖動有目標感（非無方向）
5. 整體感是「熟悉操作」而非「刻意演示」

---

### 工作流 C：Midjourney + Kling AI（標準人物採訪）

**適用條件：** 有 CHAR 角色出鏡的靜止採訪畫面，或不需要攝影機運動的 B-roll。

**Midjourney 豎屏必加參數：**
```
--ar 9:16 --style raw --v 7
```

**構圖控制語（必加）：**
```
subject positioned in upper portion of frame, generous empty lower third
for text overlay, vertical composition optimized for mobile viewing
```

**Negative Prompt 基底：**
```
smooth skin, perfect skin, flawless, airbrushed, watermark, logo, text overlay,
CGI, 3D render, cartoon, anime, blurry, low quality, subject centered too low,
face obscured by bottom frame, horizontal composition, widescreen format
```

**Kling AI 動態化 Prompt 方向：**
- 採訪鏡頭：自然說話動態，微小頭部律動，允許自然呼吸
- SOT 鏡頭：送 HeyGen 口型同步前先確認臉部清晰度
- 不用動態的場景：Kling 輕微環境動態即可（葉子晃動、燈光呼吸感）

---

### 工作流 D：After Effects（GFX + 品牌動畫）

**適用條件：** 需要動態文字、計數動畫、品牌 CTA 片尾、靜態圖定格。

**字幕規格：**
- 字體：Noto Sans TC Bold
- 安全區：距邊框 ≥150px
- 位置：畫面下方 25%（1440px 以下）
- 字號：≥52pt（1080p 輸出）
- 顏色：白色 + 品牌強調色底板

**CTA 片尾規格（最後 10 秒）：**
- 背景：品牌主色（全屏）
- URL：≥80pt，Semi-Bold，置中
- 只允許一個動作 / 一個連結
- 不加多餘動效干擾視線

---

## CHAR 角色一致性管理（Fixed Seed 流程）

**三輪生成流程：**

**第一輪 — 探索性（20~30 張）**
- 使用開放性 Prompt，生成候選臉
- 重點確認：年齡感、臉型、標誌性特徵

**第二輪 — 收斂性（從候選精修）**
- 調整 Prompt，向候選臉靠近
- 逐步收斂到目標外觀

**第三輪 — 六基準圖（對應情緒溫度）**
- 情緒 50/55/75/78/85/90 各一張
- 確保不同情緒看起來是同一個人

**Fixed Seed 鎖定三個必過條件：**
- A：相同 Seed 在 5500K 和 3800K 下，臉部輪廓辨識度 ≥ 80%
- B：情緒 55 和 85 並排，不會讓人覺得是不同人
- C：特殊臉部特徵（黑眼圈 / 鬍渣等）加入後，整體不顯過度病態

**IP-Adapter 強度設定：**
- 主採訪特寫（MCU / CU）：0.88
- 半身 B-roll：0.82
- 背影 / 手部特寫：不需 IP-Adapter

---

## 音樂分段策略（Suno AI）

不建議使用單一曲風貫穿全片。依情緒段落分別生成：

| 情緒段落 | 時間點（90~120 秒影片）| Suno Prompt 方向 |
|---------|----------------------|----------------|
| 痛點建立 | 0~30 秒 | subtle tension, minimalist electronic, low tempo |
| 轉折發現 | 30~50 秒 | building curiosity, gentle uplifting, tempo increase |
| 使用產品 | 50~90 秒 | confident modern corporate, steady rhythm |
| 結果收尾 | 90~120 秒 | warm resolution, optimistic, light and clean |

各段獨立生成後，After Effects 手動剪接，段落間 0.5~1 秒淡入淡出。

---

## 版權清單（每個專案開工前確認）

| 素材 | 工具 | 需確認項目 |
|------|------|----------|
| 靜態圖 | Midjourney | 帳號方案為 Pro 以上（商業授權）|
| 動態 B-roll | Kling AI 2.0 | 商業版授權；輸出需標示 AI 生成 |
| 攝影機補間 | Sea Dance 2 | 帳號存取權限；商業授權 |
| UI 動態 | Wan 2.7 | 商業授權範圍（與 Wan 2.1 分開確認）|
| 音樂 | Suno AI | Pro 計劃商業授權 |
| TTS | ElevenLabs | Creator 方案；確認月份用量配額 |
| 口型同步 | HeyGen | 確認繁中語音；月份用量配額 |
| 產品 UI | 自有產品 | 由工程師確認哪些畫面可公開 |
