# [品牌代碼]-[集數] — 音頻設計規格

**Owner：** 聲音創作 / 製片總控
**狀態：** 草稿
**最後更新：** YYYY-MM-DD

---

## 一、品牌聲音語言定義（Brand Sound Identity）

### 情感調性
| 維度 | 描述 | 對應音樂語言 |
|------|------|------------|
| 主調性 | 溫暖、專業、可信賴 | 鋼琴主旋律 + 弦樂墊底 |
| 次調性 | 積極、前進感 | 輕快打擊節奏（70-85 BPM）|
| 質感 | 乾淨、不過分商業 | 原聲樂器為主，電子為輔 |

### 禁止使用的音效類型
- ❌ 廉價廣告感音效（例：叮咚提示音、卡通音效）
- ❌ 過於電子化 EDM / 電子舞曲
- ❌ 搖滾吉他失真音色
- ❌ 帶有其他品牌聯想的旋律
- ❌ 人聲樣本（rap / 哼唱）—— 旁白除外

### 核心音頻元素清單
1. **品牌尾板（Brand Stinger）**：1.5-2 秒，出現在每集片尾
2. **開場氛圍墊（Ambient Intro）**：0-5 秒，低音量建立情境
3. **主題音樂（Theme Music）**：貫穿全片，隨情緒起伏調整音量
4. **場景過渡音效（Transition SFX）**：簡短（0.3-0.5s），銜接鏡頭切換
5. **旁白（VO）**：ElevenLabs TTS，見第四節規格

---

## 二、各版本音樂弧線規劃

### 版本 A — 情感驅動型（2 分鐘示範）

```
時間軸：
00:00-00:05  開場墊 ── 低音量，建立情境（BPM: 65-70，情緒溫度: 20）
00:05-00:20  問題鋪陳 ── 略帶緊張感（BPM: 70，情緒溫度: 30）
00:20-00:50  轉折點 ── 旋律開始上揚（BPM: 75，情緒溫度: 50）
00:50-01:30  解決方案展示 ── 明亮上揚（BPM: 80，情緒溫度: 70）
01:30-01:50  成果高潮 ── 最大動態，弦樂全開（BPM: 80，情緒溫度: 90）
01:50-02:00  品牌尾板 ── 淡出 + Stinger（BPM: N/A，情緒溫度: 75）
```

**音量包絡線設計（版本 A）：**
- 開場：-24 LUFS（幾乎感覺不到音樂）
- 問題段：-20 LUFS
- 轉折：-18 LUFS（音樂開始被意識到）
- 高潮：-16 LUFS
- VO 說話時：音樂 ducking 至 -24 LUFS，VO 結束後 0.5s 回升
- 尾板：-12 LUFS（Stinger 清晰可聽）

### 版本 B — 節奏驅動型（快剪）

```
時間軸：
00:00-00:03  直接開場 ── 節奏先行（BPM: 85，情緒溫度: 55）
00:03-00:20  問題快切 ── 持續高能（BPM: 85，情緒溫度: 60）
00:20-00:45  方案展示 ── 節奏加速感（BPM: 90，情緒溫度: 75）
00:45-00:55  成果 ── 最強節拍（BPM: 90，情緒溫度: 90）
00:55-01:00  品牌尾板（BPM: N/A，情緒溫度: 80）
```

### 版本 C — 靜謐信任型（B2B / LinkedIn）

```
時間軸：
00:00-00:10  靜默開場 ── 幾乎無音樂（BPM: 60，情緒溫度: 15）
00:10-00:40  緩慢鋪陳 ── 鋼琴為主（BPM: 60-65，情緒溫度: 35）
00:40-01:10  解決方案 ── 弦樂進入（BPM: 65，情緒溫度: 60）
01:10-01:30  結論 ── 溫暖收尾（BPM: 65，情緒溫度: 70）
01:30-01:40  品牌尾板（情緒溫度: 65）
```

---

## 三、Suno AI Prompt 格式

### Prompt 結構
```
[風格關鍵字], [BPM], [樂器組合], [情緒描述], [禁止元素]
```

### 版本 A Prompt（情感驅動型）
```
instrumental, cinematic documentary, 75 BPM, piano + strings + subtle percussion,
warm and trustworthy, emotional arc from tension to resolution,
no vocals, no electronic beats, no distortion, no choir
```

### 版本 B Prompt（節奏驅動型）
```
instrumental, upbeat corporate, 85 BPM, acoustic guitar + light piano + driving percussion,
energetic and optimistic, forward momentum, clean and professional,
no vocals, no heavy bass drops, no EDM elements, no jazz improvisation
```

### 版本 C Prompt（靜謐信任型）
```
instrumental, minimal piano, 62 BPM, solo piano + soft string pad,
quiet confidence, trust and credibility, gentle emotional warmth,
no percussion, no vocals, no brass, no dramatic swells, under 90 seconds
```

### Suno 生成後處理步驟
1. 生成 3-5 個版本，選取情緒最符合腳本弧線的版本
2. 使用 GarageBand 或 Audacity 調整：
   - 裁剪至所需長度（精確到 0.1 秒）
   - 頭尾加 0.5 秒 fade in / fade out
3. 導出格式：WAV 48kHz / 24bit（剪輯主檔），MP3 320kbps（備份）

---

## 四、品牌尾板（Brand Stinger）設計規格

### 基礎規格
| 項目 | 規格 |
|------|------|
| 時長 | 1.5-2 秒 |
| 音符結構 | Do-Re-Mi-Sol（上行四音）|
| 主音色 | Marimba（木琴）|
| 補充音色 | 輕柔鋼琴泛音 |
| 結尾殘響 | 0.5 秒 reverb tail |

### 頻率設計
- **掃頻層**：2kHz → 4kHz 上行掃頻（配合音符上行）
- **落地低音**：150-250Hz，最後一音（Sol）落地時進入
- **高頻亮度**：8kHz shelf boost +2dB，增加清晰度

### 音量規格
| 指標 | 數值 |
|------|------|
| 目標響度 | -12 LUFS |
| 峰值限制 | -1 dBTP |
| 動態範圍 | 8-12 LU |

### 使用情境
- 出現時機：每集最後一個畫面（品牌 logo 出現時）
- 疊加方式：與背景音樂疊加，背景音樂同步 fade out 至 -30 LUFS
- 不可出現時機：廣告投放版（30 秒以下），改用靜默或 2 秒音樂淡出

---

## 五、ElevenLabs TTS 旁白規格

### 基礎設定
| 項目 | 推薦值 | 說明 |
|------|--------|------|
| 語速（Speed）| 0.85-0.95x | 0.9 為標準值，情感段落可降至 0.85 |
| Stability | 0.55-0.65 | 過高會失去自然感 |
| Clarity | 0.75-0.85 | 清晰度優先 |
| Style Exaggeration | 0.15-0.25 | 輕微情感表現，避免過度 |

### 情緒標籤設定（SSML）
```xml
<!-- 問題段：略帶緊張 -->
<prosody rate="slow" pitch="-2st">這個問題困擾了我三年。</prosody>

<!-- 轉折點：語氣上揚 -->
<prosody rate="medium" pitch="+1st">直到我發現了這個方法。</prosody>

<!-- CTA：清晰有力 -->
<prosody rate="medium" volume="+3dB">現在就試試看。</prosody>
```

### 各平台旁白音量標準
| 平台 | 目標響度 | 峰值限制 |
|------|---------|---------|
| TikTok | -14 LUFS | -1 dBTP |
| Instagram Reels | -14 LUFS | -1 dBTP |
| YouTube | -14 LUFS | -1 dBTP |
| LinkedIn | -16 LUFS | -1 dBTP |

### SOT vs VO Ducking 規格
| 情境 | 音樂音量 | 旁白音量 |
|------|---------|---------|
| 純音樂段 | 主響度 | — |
| VO 說話時 | -18 LUFS（ducking）| -14 LUFS |
| VO 結束後 | 0.5 秒內回升至主響度 | — |
| SOT（同期聲）段 | -20 LUFS | — |

**Ducking 技術設定（Final Cut Pro）：**
1. 在音樂軌道加入「音量」關鍵幀
2. VO 開始前 0.2 秒開始降低
3. 降低時間：0.2 秒
4. 回升時間：0.5 秒

---

## 六、平台發布音頻適配清單

### 技術規格對照表
| 平台 | 目標響度 | 峰值 | 格式 | 位元率 | 採樣率 |
|------|---------|------|------|--------|--------|
| TikTok | -14 LUFS | -1 dBTP | AAC | 128 kbps | 44.1 kHz |
| Instagram Reels | -14 LUFS | -1 dBTP | AAC | 128 kbps | 44.1 kHz |
| YouTube | -14 LUFS | -1 dBTP | AAC | 192 kbps | 48 kHz |
| LinkedIn | -16 LUFS | -1 dBTP | AAC | 128 kbps | 44.1 kHz |

### 響度標準化操作步驟

**Final Cut Pro：**
1. 選取影片 → 修改 → 音量與聲像
2. 開啟「響度」面板
3. 設定：目標 -14 LUFS，最大真峰值 -1 dBTP
4. 點擊「分析並修正」
5. 匯出前：共享 → 使用預設條件確認設定

**Adobe Premiere Pro：**
1. 視窗 → 響度（Loudness）面板
2. 序列 → 序列設定 → 音頻 → 響度標準：ITU-R BS.1770-3
3. 匯出設定：音頻 → 勾選「標準化音頻」→ -14 LUFS
4. 或使用 Loudness Radar 插件手動確認

**DaVinci Resolve：**
1. Fairlight 頁面 → 響度計
2. 目標設定：-14 LUFS，LRA ≤ 15
3. 使用「Bus Compressor」配合 Loudness Normalizer
4. 匯出：Deliver 頁面 → 音頻格式選 AAC，位元率對應平台規格

### 發布前音頻 QC 清單
- [ ] 旁白無爆音（峰值 < -1 dBTP）
- [ ] 旁白無底噪（底噪 < -60 dBFS）
- [ ] 音樂 ducking 流暢，無明顯突兀感
- [ ] 品牌尾板出現時間正確（最後 1.5-2 秒）
- [ ] 整體響度符合目標平台規格
- [ ] 不同場景間無明顯音量跳躍
- [ ] 用耳機 + 喇叭兩種設備各試聽一次
