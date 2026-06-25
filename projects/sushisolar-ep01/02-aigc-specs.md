# 鮨佐樂 omakase — AIGC 技術規格書

**版本：** v1.0  
**Owner：** AIGC 技術指導  
**建立日期：** 2026-06-25  
**對應腳本：** 01-scripts.md

---

## 工具鏈選定

| 素材類型 | 選定工具 | 版本 | 用途 |
|---------|---------|------|------|
| 靜態場景生成 | Midjourney | v7 | 漁港、城市、吧台、食材特寫 |
| 圖生影（動態 B-roll）| Kling AI | 2.0 | 現有 IG 照片轉動態 |
| 攝影機運動補間 | Sea Dance 2 | — | push-in、城市推進、視差移動 |
| GFX + 字幕合成 | After Effects | 2024+ | 所有文字動態、Logo 動畫、CTA |
| AI 音樂 | Suno AI | v4 | 3 支影片背景音樂 |
| TTS 旁白（B版）| ElevenLabs | — | 普通話女聲，B-HKM 版 |

---

## 豎屏構圖規格

**Midjourney 必加參數：**
```
--ar 9:16 --style raw --v 7
```

**構圖區域分配（1080×1920px）：**

| 區域 | 像素範圍 | 用途 |
|------|---------|------|
| 上方 60% | y: 0–1152px | 主體視覺（食材、師傅手、場景）|
| 中間 15% | y: 1152–1440px | 視覺緩衝，避免主體太低 |
| 下方 25% | y: 1440–1920px | 字幕安全區（完全保留，不放主體）|

**必加構圖控制語（每個 Prompt 都要加）：**
```
subject positioned in upper portion of frame, generous empty lower third 
for text overlay, vertical composition optimized for mobile viewing, 
9:16 aspect ratio
```

---

## 逐鏡 Midjourney Prompt

> 格式：`[畫質基底] + [場景描述] + [構圖控制] + [燈光方案] + [情緒色調] + 豎屏參數`

### 版本 A-SUM / A-EVR 共用場景

**S01：玻璃杯碎冰 + 海膽**
```
cinematic macro photography, transparent glass filled with crushed ice, 
bright orange sea urchin nestled between ice cubes, summer afternoon 
side light refracting into scattered white specks, cold blue-white color 
temperature 3800K, no human hands, minimal composition, 
subject in upper third of frame, empty lower third for subtitles, 
photorealistic, film grain --ar 9:16 --style raw --v 7
```

**S02：日式木質吧台俯拍**
```
overhead shot japanese hinoki wood counter, single warm spotlight circle 
on wood grain texture, empty white ceramic plate centered, extreme bokeh 
background f1.4, warm rim lighting, minimalist zen composition, 
subject in upper center of frame, lower third clear, 
photorealistic restaurant interior --ar 9:16 --style raw --v 7
```

**S03：師傅手部捏握壽司**
```
close up japanese sushi chef hands forming nigiri, no face visible, 
traditional white chef uniform sleeves, fish placed perfectly, 
dramatic side lighting, shallow depth of field, 
hands in upper half of frame, lower third empty, 
cinematic food photography --ar 9:16 --style raw --v 7
```

**S04-A（夏季版）：海膽竹葉特寫**
```
macro food photography, fresh sea urchin on bamboo leaf, 
steam rising softly around edges, warm backlight contrasting 
with cold orange roe, high detail, 
subject in upper two thirds, lower third empty for text, 
cinematic food still --ar 9:16 --style raw --v 7
```

**S04-B：鮪魚大腹特寫**
```
macro photography, bluefin tuna otoro cross-section, 
visible fat marbling lines, sharp Japanese knife blade visible on right 
not yet cutting, suspended moment, left-side dramatic lighting, 
food positioned upper third, lower area empty, 
photorealistic --ar 9:16 --style raw --v 7
```

**S04-C（夏季版）：日本漁港清晨（溯源場景）**
```
cinematic wide shot, japanese fishing harbor at dawn, 
wooden fishing boats docked, morning mist, fishermen unloading catch, 
blue-grey color palette, golden horizon glow, no text, 
scene fills upper 70% of frame, lower third empty sky or water reflection,
35mm film look --ar 9:16 --style raw --v 7
```

**S05：台北夏夜城市感**
```
cinematic night street photography, Taipei Da'an district, 
neon reflections on wet cobblestones after rain, distant 101 tower silhouette, 
warm amber streetlights, slightly cool color grading 5000K, 
bokeh foreground, city fills upper frame, 
lower third: wet ground reflection only --ar 9:16 --style raw --v 7
```

**S05（吧台用餐背影）：**
```
cinematic restaurant scene, two diners seen from behind sitting at 
japanese omakase counter, chef preparing dish behind counter, 
warm bokeh background lights, intimate atmosphere, 
no faces visible, figures in upper center frame, 
lower third floor/counter only --ar 9:16 --style raw --v 7
```

### 版本 A-EVR 額外場景

**S03 職人背影：**
```
japanese sushi chef standing motionless behind hinoki counter, 
back facing camera, white uniform, hands folded, 
soft overhead light, waiting posture, zen stillness, 
figure in upper center, lower third clean counter surface, 
photorealistic --ar 9:16 --style raw --v 7
```

**S04-A（通用版）：松露特寫**
```
macro food photography, fresh truffle slice on white ceramic plate, 
morning mist background, neutral color temperature 5000K, 
no seasonal cues, fine texture detail visible, 
food in upper center frame, lower third empty --ar 9:16 --style raw --v 7
```

### 版本 B-HKM 額外場景

**S01：台北夜街城市感**
```
cinematic night street, Taipei modern city, wet streets reflecting neon,  
Japanese restaurant facade with glowing signage in foreground, 
distant Taipei 101 skyline, cold blue-purple ambient, 
city scene fills upper 75%, lower quarter wet ground reflection only,
35mm film cinematic --ar 9:16 --style raw --v 7
```

**S02-A：日本漁港清晨**
```
（同 S04-C 夏季版 Prompt，直接複用）
```

**S02-B：築地風格市場**
```
cinematic fish market scene, fishmonger holding large tuna belly otoro 
examining quality, white cold fluorescent overhead light, 
fish market stalls background blurred, documentary style, 
subject in upper half of frame, lower third empty floor --ar 9:16 --style raw --v 7
```

**S05-B：從店外看進吧台**
```
night exterior looking through restaurant window into warm interior, 
japanese omakase counter visible inside, warm amber light glowing, 
blurred silhouettes of diners, cold exterior contrasting warm interior, 
window fills upper frame, lower third: exterior ground --ar 9:16 --style raw --v 7
```

---

## Kling AI 圖生影規格

**標準設定：**
- 解析度：1080×1920（豎屏）
- 時長：5 秒 / 段（剪輯時可截取）
- 運動幅度：低（Low motion）
- 種子固定：生成滿意後記錄 Seed 備用

**各鏡頭設定：**

| 鏡號 | 來源圖片 | 運動指令 | 備注 |
|------|---------|---------|------|
| S03 師傅手部 | IG 師傅手部圖 or MJ 生成 | `hands slowly shaping nigiri, gentle natural movement, slow motion` | 生成 3 段選最自然 |
| S04-D 師傅端菜 | MJ 生成白盤圖 | `plate slowly moving toward camera, gentle push in` | 速度極慢 |
| S03-A 店外 | IG 店外圖 | `subtle camera zoom in toward entrance, lights flickering gently` | 低動態 |
| S03-C 切魚 | IG 師傅手部圖 or MJ | `knife descending slowly, slow motion, light reflecting off blade` | 慢動作感 |
| S04-A 師傅遞壽司 | MJ 生成 | `hands extending plate toward viewer, slow push forward` | 低動態 |

---

## Sea Dance 2 攝影機運動規格

**使用場景：需要電影感推進、視差移動的靜態圖片**

| 鏡號 | 動作類型 | 速度 | 幀數 |
|------|---------|------|------|
| S01 碎冰 | 極微 zoom-in | 極慢 | 60f |
| S04-C 漁港 | horizontal parallax push-in | 慢 | 90f |
| S05 台北城市 | vertical push-in from above | 慢 | 120f |
| B S01 台北夜街 | slow push-in toward restaurant | 慢 | 90f |
| B S05-A 台北 101 | subtle pull-back | 慢 | 90f |
| B S07 城市收尾 | slow pull-back | 中 | 90f |

**Sea Dance 2 Prompt 補充語（必加）：**
```
vertical 9:16 composition, slow vertical push-in, subject in upper frame,
lower area kept clean for text, mobile-first framing, cinematic movement
```

---

## 色溫方案

| 段落 | 色溫 | After Effects 調色方向 |
|------|------|----------------------|
| 開場（S01–S02）| 3800K | 降低色溫，藍色偏移，高對比 |
| 食材段（S03–S04）| 4500K | 中性偏暖，食材色彩還原 |
| 用餐氛圍（S05）| 5500K | 暖白，Lift 微升，Shadows 深褐 |
| CTA（S06）| 品牌色 | 背景 #1A0E06，文字 #F5E6C8 |

---

## Negative Prompt（所有 MJ 圖必加）

```
smooth airbrushed skin, stock photo posing, fake smile, watermark, logo, 
text overlay, CGI render, cartoon, anime, blurry, low quality, 
subject centered too low, face obscured by bottom frame, 
horizontal composition, widescreen format, oversaturated colors,
western facial features
```

---

## 算力成本追蹤

| 工具 | 生成數量 | 版本 | 費用記錄 |
|------|---------|------|---------|
| Midjourney | 張 | v7 | — |
| Kling AI | 段 | 2.0 | — |
| Sea Dance 2 | 段 | — | — |
| Suno AI | 首 | v4 | — |
| ElevenLabs | 分鐘 | — | — |
| **合計** | | | — |

> 生成後請於此表記錄實際用量，以便未來案例的成本估算。
