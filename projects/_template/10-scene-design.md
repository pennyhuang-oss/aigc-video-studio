# [品牌代碼]-[集數] — 場景設計規格

**Owner：** 視覺創作 / 導演
**狀態：** 草稿
**最後更新：** YYYY-MM-DD

---

## 場景分類系統概述

本文件定義四種標準場景類型（S-A / S-B / S-C / S-D），適用於所有品牌宣傳片的視覺設計。每種類型對應不同的情緒功能，在腳本結構中承擔特定敘事角色。

| 場景代碼 | 名稱 | 敘事功能 | 情緒溫度 | 色溫 |
|---------|------|---------|---------|------|
| S-A | 採訪場景 | 建立信任、角色介紹 | 45-65 | 5000K |
| S-B | 痛點場景 | 製造緊張感、認同感 | 18-40 | 3800K 冷調 |
| S-C | 平台/操作場景 | 展示解決方案 | 55-70 | 4500K 中性 |
| S-D | 成果場景 | 情緒高點、轉化驅動 | 75-95 | 5500K 暖調 |

---

## S-A 採訪場景

### 設計意圖
建立角色可信度與觀眾信任感。採訪形式讓觀眾感受到「真實人物在說話」，降低廣告感，提升認同度。

### 典型景別
- **MCU（Medium Close-Up）**：胸部以上，顯示表情與肢體語言，主要採訪畫面
- **CU（Close-Up）**：臉部特寫，用於強調情緒轉折點
- **OTS（Over The Shoulder）**：偶爾使用，增加臨場感

### 背景設計原則
- 景深虛化（f/1.4-f/2.8 等效）：背景不清晰，主體突出
- 推薦背景元素：書架、辦公室、白板、植栽
- 禁止：純白背景（顯得廉價）、雜亂背景（分散注意力）
- 色彩：背景以中性暖色為主（米白、淺灰、深木色）

### 燈光規格
| 項目 | 規格 |
|------|------|
| 主燈（Key Light）| 左側 45° 入射，色溫 5000K |
| 補光（Fill Light）| 右側，主燈亮度 30-40%，柔化陰影 |
| 輪廓光（Rim Light）| 後方，勾勒主體邊緣，增加立體感 |
| 整體色溫 | 5000K（自然日光感）|
| 情緒溫度 | 45-65（中等正向）|

### Midjourney Prompt 模板（S-A）
```
portrait photography, [角色描述：例如 30s Asian woman, confident expression],
office background with bokeh, warm 5000K lighting, left 45 degree key light,
soft fill light from right, documentary style interview, 9:16 vertical,
ultra realistic, natural skin texture, professional but approachable
--ar 9:16 --v 7
```

### Negative Prompt（S-A）
```
--no cartoon, anime, illustration, watermark, text, logo, studio lighting,
harsh shadows, overexposed, underexposed, distorted face, extra limbs
```

### Return Last Frame 應用
- S-A 主採訪場景建立後，後續同角色採訪鏡頭需截取前一鏡最後一幀作為起始幀
- 確保同一角色跨鏡頭時服裝、背景、燈光一致

---

## S-B 痛點場景

### 設計意圖
製造緊張感與觀眾認同感。讓觀眾感受到「這就是我的困境」，為後續解決方案創造需求張力。痛點場景是完播率的關鍵：前 5 秒必須讓目標受眾強烈認同。

### 典型元素
| 元素 | 視覺呈現 | 情緒意義 |
|------|---------|---------|
| 深夜氛圍 | 黑暗房間、螢幕光 | 焦慮、壓力 |
| 帳單 / 發票 | ECU 手持帳單 | 財務壓力 |
| 手機螢幕 | 通知、數字 | 現代焦慮感 |
| 疲憊表情 | CU 臉部 | 情感認同 |
| 搜尋畫面 | 手機 Google 搜尋 | 迫切需求 |

### 色溫與視覺氛圍
| 項目 | 規格 |
|------|------|
| 色溫 | 3800K 偏冷藍調 |
| 情緒溫度 | 18-40（低點）|
| 對比度 | 高對比（深色背景 + 螢幕光點光源）|
| 飽和度 | 低飽和（desaturated，-20 至 -30%）|
| 可選：黑白或深藍色調 LUT | 強調壓抑感 |

### Midjourney Prompt 模板（S-B 帳單）
```
close up of hands holding phone showing bill or invoice,
late night atmosphere, cold blue light 3800K,
stress and anxiety mood, dark room background,
soft screen glow, documentary style, 9:16 vertical,
ultra realistic, cinematic low key lighting
--ar 9:16 --v 7
```

### Midjourney Prompt 模板（S-B 疲憊表情）
```
close up portrait, [角色描述], exhausted and stressed expression,
late night, blue cold light 3800K, dark background,
documentary style, authentic emotion, 9:16 vertical,
ultra realistic --ar 9:16 --v 7
```

### Negative Prompt（S-B）
```
--no bright colors, happy expression, warm light, sunlight,
cartoon, anime, watermark, text, logo, stock photo style
```

---

## S-C 平台/操作場景

### 設計意圖
具體展示解決方案的使用方式。此場景需兼顧清晰度（觀眾能看清 UI）與真實感（不能像純產品截圖），是說服力最直接的場景類型。

### UI 截圖處理規格
**首選：Edwin 截圖 + Wan 2.7 動態化**
1. 截取實際產品截圖（1080×1920 或裁切為 9:16）
2. 上傳至 Wan 2.7 → 設定游標動態、點擊動畫
3. 輸出：5-8 秒 UI 操作動態影片

**備援：Figma Mockup**
1. 在 Figma 製作手機框架 Mockup
2. 將截圖置入手機框架
3. 添加輕微動態（Figma Smart Animate）
4. 匯出為影片或 GIF

### 色溫與視覺氛圍
| 項目 | 規格 |
|------|------|
| 色溫 | 4500K 中性白 |
| 情緒溫度 | 55-70（解決方案感）|
| 背景 | 乾淨桌面 / 手持手機 / 電腦螢幕 |
| 光線 | 均勻柔光，避免反光 |

### Wan 2.7 UI 動態參數
```
Motion type: cursor movement + tap animation
Duration: 5-8 seconds
Loop: No
Resolution: 1080×1920
Export: MP4 H.264
```

### After Effects 合成規格
- 新建合成：1080×1920，24fps，長度依腳本
- UI 層：置於最上層，縮放至約 85% 寬度（留邊距）
- 手機框架層：次上層，作為遮罩
- 背景層：模糊辦公桌或純色背景
- 動態：UI 從下方 slide in（0.3s ease out）

---

## S-D 成果場景

### 設計意圖
情緒高點，畫面最暖。此場景傳達「問題已解決」的滿足感，是轉化率最直接相關的場景。觀眾應在此場景感受到「如果我使用這個產品，我也能有這種感覺」。

### 典型元素
| 元素 | 視覺呈現 | 情緒意義 |
|------|---------|---------|
| 滿意表情 | 主角微笑 / 放鬆表情 | 情感認同 |
| 成果數字 | 手機截圖顯示數據 | 可信度 |
| 自然光環境 | 白天、窗邊 | 正向能量 |
| 家人 / 同事 | 分享成功 | 社群認同 |

### 色溫與視覺氛圍
| 項目 | 規格 |
|------|------|
| 色溫 | 5500K 暖調（Golden Hour 感）|
| 情緒溫度 | 75-95（高點）|
| 對比度 | 中低對比（柔和、暖和）|
| 飽和度 | 略高（+10-15%），增加活力感 |
| Film Grain | σ=8~12（必須加入，增加紀錄感與真實感）|

### Film Grain 技術規格
| 項目 | 規格 |
|------|------|
| 顆粒強度 σ | 8-12（輕度，不干擾主體）|
| 顆粒大小 | 1-2px |
| 顆粒動態 | 每幀隨機（非靜態圖案）|
| 顏色 | 亮度顆粒（僅 Y 通道），非彩色顆粒 |

**After Effects Film Grain 添加方式：**
1. 新建調整層（Adjustment Layer）
2. 效果 → 雜訊與顆粒 → 新增顆粒
3. 強度：0.15-0.25，大小：1.5，柔和度：0.5
4. 動畫隨機化：開啟「使用顏色雜訊」= 關閉，「動畫設定」= 隨機種子動畫

### Midjourney Prompt 模板（S-D）
```
portrait photography, [角色描述：例如 30s Asian woman, warm smile, relieved expression],
warm golden hour light 5500K, window light from left,
relief and satisfaction expression, soft bokeh background,
documentary style, subtle film grain, 9:16 vertical,
ultra realistic, natural skin, cinematic warmth
--ar 9:16 --v 7
```

### Negative Prompt（S-D）
```
--no cold light, blue tones, sad expression, dark background,
cartoon, anime, watermark, text, logo, studio flash
```

---

## 9:16 豎屏構圖鐵則

### 主體位置規則
```
┌─────────────────┐
│   空氣感上方    │ 上方 15%：可有少量元素
│                 │
│  ┌───────────┐  │
│  │           │  │ 上方 1/3 = 主體臉部位置
│  │  主　　體  │  │ （雙眼約在整體高度 25-35%）
│  │           │  │
│  └───────────┘  │
│                 │
│  字幕安全區     │ 下方 25%：保持乾淨
│  ─────────────  │ 下方 20%：字幕置放區
└─────────────────┘
```

### 構圖鐵律
1. **主體在畫面上方 1/3**：主角雙眼位於整體高度 25-35% 處
2. **下方 25% 保持乾淨**：字幕安全區，主體不可延伸至此
3. **字幕在下方 20% 區域**：字型大小建議 42-48pt，行距 1.3
4. **不可有任何 logo / watermark**：所有圖像生成後必須確認無浮水印
5. **畫面邊緣留白 5%**：避免主體被裁切
6. **左右對稱感**：主體置中（±5% 偏移可接受）

### 禁止的構圖錯誤
- ❌ 主體臉部在畫面中央或下半部
- ❌ 字幕壓在主體臉部或重要元素上
- ❌ 背景線條（地平線、牆線）穿過主體頭部
- ❌ 主體被畫面邊緣截斷手臂或身體

---

## Return Last Frame 技術說明

### 目的
維持跨鏡頭視覺連貫性。Kling AI 每次生成的影片起始畫面會有細微差異，Return Last Frame 技術確保同一場景連續鏡頭之間角色外觀、背景一致，避免「跳躍感」。

### 操作步驟
1. 生成第一個鏡頭影片（例：S03-01）
2. 在影片播放器中找到最後一幀（最後 1/24 秒）
3. 截圖儲存為 PNG（命名：`S03-01_last_frame.png`）
4. 上傳 `S03-01_last_frame.png` 至 Kling AI 2.0 → Image to Video
5. 此圖作為 S03-02 的起始幀（First Frame）
6. 設定 Motion Intensity 3-4（比原始略低，確保主體形態延續）

### 適用情境
- ✅ 同一場景中同一角色的連續鏡頭
- ✅ 對話場景中攝影機切換角度
- ✅ 動作連續性需求（例：手部動作連貫）

### 不適用情境
- ❌ 場景切換（S-A 到 S-B 之間不需要）
- ❌ 時間跳躍（同場景但時間不同）

### 檔案命名規範
```
[鏡號]_last_frame.png
例：S03-01_last_frame.png
    S03-02_last_frame.png
```

---

## 場景設計 QC 清單

發布前確認每個場景符合以下標準：

### 視覺一致性
- [ ] 同場景跨鏡頭色溫偏差 < 200K
- [ ] 同一角色跨鏡頭服裝、髮型一致
- [ ] 無水印（Midjourney / Kling 浮水印）
- [ ] 無明顯 AI 形變（手指、五官扭曲）
- [ ] 主體輪廓偏移 < 10px（跨鏡頭比對）

### 構圖
- [ ] 主體位於上方 1/3 區域
- [ ] 下方 25% 無重要視覺元素
- [ ] 字幕不壓主體
- [ ] 無 logo / watermark

### 技術規格
- [ ] 解析度 1080×1920 px
- [ ] 幀率 24fps
- [ ] S-D 場景有 Film Grain（σ=8~12）
- [ ] 色溫符合場景類型規格
