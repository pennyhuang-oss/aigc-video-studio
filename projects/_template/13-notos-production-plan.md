# [品牌代碼]-[集數] — Notos 平台製作計劃

**Owner：** 視覺創作 / 製片總控
**狀態：** 草稿
**最後更新：** YYYY-MM-DD

---

## 一、為什麼使用 Notos

Notos 整合了 BytePlus 的 Seedream（圖像生成）與 Seedance（影片生成），提供一站式 AIGC 製作流程。相較於傳統 Midjourney + Kling 組合，Notos 的主要優勢如下：

| 對比維度 | Midjourney + Kling | Notos（Seedream + Seedance）|
|---------|-------------------|---------------------------|
| 流程整合度 | 需在兩個平台間切換 | 一站式圖像→影片 |
| 角色一致性 | 需依賴 Seed 值管理 | 原生角色一致性支持 |
| 成本 | 需訂閱兩個平台 | 單一平台計費 |
| 中文 Prompt 支持 | Midjourney 建議英文 | 原生中英文雙語 |
| 首末幀控制 | Kling 支持，操作獨立 | Seedance 原生首末幀插值 |
| 攝影機控制 | Sea Dance 2 外掛 | Seedance 內建 |

**適用場景：**
- 預算有限，需減少工具訂閱成本
- 團隊 Midjourney 不熟練，需降低學習曲線
- 需要密集生產（高頻率發片，多集並行）

**不適用場景：**
- 需要高度精確 Midjourney 風格控制的品牌
- 已有完整 MJ + Kling 流程且品質穩定
- 需要特定 Midjourney --style 參數的視覺風格

---

## 二、四種工作流在 Notos 平台的對應

| 原工作流 | 原工具 | Notos 對應功能 | 說明 |
|---------|-------|--------------|------|
| Workflow A | Sea Dance 2 | Seedance 攝影機控制 | 同等的首末幀插值，攝影機路徑設定 |
| Workflow B | Wan 2.7 | Seedance UI 動態模式 | 介面操作展示，游標動態 |
| Workflow C | MJ v7 + Kling 2.0 | Seedream（圖像）+ Seedance（影片）| 主要工作流，一站式圖生影 |
| Workflow D | After Effects | 搭配 Notos 後期輸出 | AE 保持為主，Notos 提供素材 |

---

## 三、Notos Seedream 圖像生成規格

### Prompt 格式差異（vs Midjourney）

| 項目 | Midjourney | Seedream |
|------|-----------|---------|
| 語言 | 強烈建議英文 | 中英文均可 |
| 比例參數 | `--ar 9:16` | 在介面選擇 9:16，或 Prompt 末尾加 `9:16比例` |
| 版本參數 | `--v 7` | 選擇模型版本（無需 Prompt 參數）|
| Negative Prompt | `--no [內容]` | 在 Negative Prompt 欄位單獨填寫 |
| Seed | `--seed [數值]` | 在進階設定輸入 Seed 值 |
| 風格強度 | `--stylize [0-1000]` | Style Strength 滑桿 |

### Seedream Prompt 模板（對應各場景類型）

**S-A 採訪場景（Seedream）：**
```
紀錄片風格人物攝影，[角色描述：例如 30歲亞裔女性，自信表情]，
辦公室背景虛化散景，5000K暖白光，左側45度主燈，
右側柔和補光，專業但親切，超寫實，9:16豎屏

Negative: 卡通，動漫，插畫，水印，文字，logo，過曝，欠曝
```

**英文版（備用）：**
```
documentary portrait photography, [character description], office bokeh background,
5000K warm white light, left 45 degree key light, soft fill right,
professional and approachable, ultra realistic, 9:16 vertical

Negative: cartoon, anime, illustration, watermark, text, logo, overexposed
```

**S-B 痛點場景（Seedream）：**
```
極近景手持手機顯示帳單，深夜氛圍，冷藍色光3800K，
壓力與焦慮情緒，黑暗房間背景，螢幕光源，超寫實，9:16豎屏

Negative: 明亮顏色，開心表情，暖光，陽光，卡通，水印
```

**S-D 成果場景（Seedream）：**
```
人物攝影，[角色描述]，暖金色黃昏光5500K，
如釋重負的滿意表情，柔和散景背景，紀錄片風格，
輕微底片顆粒，超寫實，9:16豎屏

Negative: 冷色調，藍色，悲傷表情，黑暗背景，卡通，水印
```

### 解析度設定
- **輸出解析度**：1080×1920（Seedream 豎屏最高解析度）
- **圖像品質**：選擇 High Quality 模式
- **生成數量**：每次生成 4 張，選最佳後再 Upscale

### 風格參數建議
| 場景類型 | Style Strength | Realism | Detail Level |
|---------|---------------|---------|-------------|
| S-A 採訪 | 30-40 | 85-90 | High |
| S-B 痛點 | 20-30 | 90-95 | Medium |
| S-D 成果 | 35-45 | 80-85 | High |

---

## 四、Notos Seedance 影片生成規格

### Duration 設定
| 場景用途 | 建議時長 | 說明 |
|---------|---------|------|
| 標準敘事鏡頭 | 5 秒 | 大多數場景 |
| 長採訪鏡頭 | 8-10 秒 | S-A 主採訪段 |
| 快切痛點鏡頭 | 3-5 秒 | S-B 快速建立情緒 |
| UI 操作展示 | 5-8 秒 | S-C 需要足夠時間展示操作 |

### Motion 強度設定
| 情境 | Motion 強度 | 說明 |
|------|-----------|------|
| 採訪場景（自然呼吸感）| Low（1-2）| 過強會導致形變 |
| 一般敘事鏡頭 | Medium（3-4）| 標準值 |
| 動態展示鏡頭 | Medium-High（4-5）| S-D 高潮段落 |
| UI 場景 | Low（1-2）| 保持 UI 可讀性 |

### First/Last Frame 設定方法
**設定 First Frame（起始幀）：**
1. 上傳靜態圖至 Seedance → Image to Video
2. 系統自動以上傳圖作為起始幀
3. 在「起始幀設定」確認圖片已載入

**設定 Last Frame（結束幀 / Return Last Frame）：**
1. 播放前一鏡頭影片至最後一幀
2. 截圖儲存（命名：`[鏡號]_last_frame.png`）
3. 在 Seedance 的「結束幀」上傳此截圖
4. 勾選「首末幀插值」模式
5. 系統將自動在起始幀與結束幀之間生成流暢動態

**攝影機控制設定：**
```
鏡頭推進（Zoom In）：選擇 "Push In" 攝影機模式，強度 Medium
鏡頭搖移（Pan）：選擇 "Pan Left/Right"，速度 Slow
靜態（Static）：選擇 "Static" 或 "Minimal Motion"
上仰（Tilt Up）：選擇 "Tilt Up"，強度 Low
```

---

## 五、從 Midjourney + Kling 遷移到 Notos 的注意事項

### Prompt 翻譯原則

**核心原則：描述性內容可翻譯，風格關鍵字需驗證**

| Midjourney 元素 | Notos 對應翻譯 | 注意事項 |
|----------------|--------------|---------|
| `ultra realistic` | `超寫實` 或 `ultra realistic` | 兩者均可，英文更穩定 |
| `documentary style` | `紀錄片風格` | 直譯有效 |
| `bokeh` | `散景虛化` | 中文翻譯效果相同 |
| `--ar 9:16` | 在介面選擇比例 | 不在 Prompt 中寫 |
| `--v 7` | 選擇對應模型版本 | 不在 Prompt 中寫 |
| `--seed 2847` | 在進階設定輸入 Seed | 獨立欄位 |
| `--stylize 250` | Style Strength 滑桿 | 換算約 250/1000 = 25% |

### 品質對比測試建議

**在正式切換前，建議執行以下對比測試：**

1. **選取 3 個代表性鏡頭**（S-A 採訪 / S-B 痛點 / S-D 成果各一個）
2. **用相同 Prompt 在兩個平台各生成 4 張圖**
3. **評分維度**：
   - 真實感（1-10）
   - 色溫準確度（1-10）
   - 主體清晰度（1-10）
   - 整體符合腳本程度（1-10）
4. **影片生成測試**：對最佳靜態圖各生成 5 秒影片，評分形變程度
5. **決策門檻**：Notos 平均分 ≥ MJ+Kling 分數的 85% 即可切換

### 切換決策標準

| 情境 | 建議決策 |
|------|---------|
| 新品牌，無歷史素材 | 優先嘗試 Notos（成本低，從零開始）|
| 既有品牌，有已建立的 MJ 視覺風格 | 謹慎遷移，先做對比測試 |
| 預算緊縮，需削減工具費 | 切換至 Notos |
| 品質要求極高的精品品牌 | 保留 MJ + Kling，Notos 作為備援 |
| 製作時程緊迫（7 天內完成）| 使用熟悉的工具，避免遷移風險 |

### 遷移風險清單
- ⚠️ Notos Prompt 風格與 MJ 可能有差異，需要重新調試
- ⚠️ Seed 值不跨平台共用（需重新鎖定角色基準圖）
- ⚠️ 既有 LUT / 色調工作流需重新校準
- ⚠️ 第一次使用 Notos 請預留額外 1-2 天調試時間

---

## 六、Notos 製作時程調整（相較標準 7 天模板）

| 日期 | 標準工作流（MJ+Kling）| Notos 工作流 | 差異說明 |
|------|---------------------|------------|---------|
| Day 1 | S-A MJ 生成 + Seed 鎖定 | Seedream S-A + Seed 鎖定 | 平台介面不同，約需多 0.5 天熟悉 |
| Day 2 | S-B MJ + Kling 動態 | Seedream S-B + Seedance | 一站式，時間相當 |
| Day 3 | S-D MJ + Kling 動態 | Seedream S-D + Seedance | 一站式，略快 |
| Day 4 | S-C Wan 2.7 / AE | Seedance UI 模式 / AE | Seedance UI 模式需測試 |
| Day 5 | S-A 採訪 Kling 動態 | Seedance 首末幀插值 | 操作類似 |
| Day 6 | 音頻製作（平台無關）| 音頻製作（同）| 無差異 |
| Day 7 | AE 合成初剪 | AE 合成初剪 | 無差異 |

**額外建議：若是首次使用 Notos，在 Day 0（前一天）先做 30 分鐘平台熟悉操作。**
