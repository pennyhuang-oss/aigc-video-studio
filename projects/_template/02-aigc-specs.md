# [專案代碼] — AIGC 技術規格書

**Owner：** AIGC 技術指導  
**版本：** v1.0  
**建立日期：** [填入]

---

## 工具鏈選定

| 素材類型 | 選定工具 | 備選 | 授權狀態 |
|---------|---------|------|---------|
| 靜態場景圖 | Midjourney v7 | DALL-E 3 | |
| 圖生動態 B-roll | Kling AI 2.0 | Wan 2.1 | |
| 攝影機運動補間 | Sea Dance 2 | Kling AI | |
| UI 操作動態 | Wan 2.7 | ScreenFlow | |
| GFX + 字幕 | After Effects | — | |
| AI 音樂 | Suno AI | Udio | |
| TTS | ElevenLabs | Azure TTS | |
| 口型同步 | HeyGen | — | |

---

## 豎屏構圖規格

**Midjourney 必加參數：**
```
--ar 9:16 --style raw --v 7
```

**構圖區域分配：**

| 區域 | 畫面比例 | 用途 |
|------|---------|------|
| 上方 60% | 0~1152px | 主體視覺區 |
| 中間 15% | 1152~1440px | 視覺緩衝 |
| 下方 25% | 1440~1920px | 字幕安全區 |

**必加構圖控制語：**
```
subject positioned in upper portion of frame, generous empty lower third
for text overlay, vertical composition optimized for mobile viewing
```

---

## Midjourney 場景 Prompt 策略

**基礎模板：**
```
[畫質基底] + [場景描述] + [構圖控制] + [燈光方案] + [情緒色調] + 豎屏參數
```

**通用 Negative Prompt：**
```
smooth skin, perfect skin, flawless, airbrushed, watermark, logo, text overlay,
CGI, 3D render, cartoon, anime, blurry, low quality, subject centered too low,
face obscured by bottom frame, horizontal composition, widescreen format
```

---

## 各集 Prompt 庫

### EP.01 — [集數名稱]

**痛點場景 A：**
```
[填入 Prompt]
```

**轉折場景：**
```
[填入 Prompt]
```

**使用產品場景：**
```
[填入 Prompt]
```

**結果展示場景：**
```
[填入 Prompt]
```

---

## 音樂分段（Suno AI）

| 段落 | 時間點 | Suno Prompt 方向 |
|------|--------|----------------|
| 痛點建立 | 0~30s | subtle tension, minimalist electronic, low tempo |
| 轉折發現 | 30~50s | building curiosity, gentle uplifting |
| 使用產品 | 50~90s | confident modern corporate, steady rhythm |
| 結果收尾 | 90~120s | warm resolution, optimistic, light and clean |

---

## 算力成本估算

| 素材 | 數量（每集）| 單價 | 單集成本 |
|------|-----------|------|---------|
| Midjourney 靜態圖 | | NT$/張 | |
| Kling AI B-roll | | NT$/段 | |
| Sea Dance 2 補間 | | NT$/段 | |
| Wan 2.7 UI 動態 | | NT$/段 | |
| Suno AI 音樂 | | NT$/段 | |
| ElevenLabs TTS | | NT$/集 | |
| **單集合計** | | | |
| **_集總計** | | | |

---

## 版本記錄

| 版本 | 日期 | 更新內容 |
|------|------|---------|
| v1.0 | | 初版建立 |
