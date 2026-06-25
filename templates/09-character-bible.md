# [專案代碼] — 角色聖經

**Owner：** 影像創作 + Vincent（AIGC 技術指導）  
**用途：** 定義每集 AIGC 主角角色的外觀、Fixed Seed、IP-Adapter 設定

---

## 角色模板

### CHAR-[編號]：[角色代碼]

**外觀規格：**

| 項目 | 描述 |
|------|------|
| 年齡 | |
| 性別 | |
| 族裔外觀 | |
| 體型 | |
| 臉型 | |
| 眼鏡 | 有/無，類型 |
| 髮型 | |
| 特徵 | |
| 服裝 | |
| 職業感 | |

**Midjourney Base Prompt：**

```
[貼入 Midjourney Prompt]
--ar 9:16 --style raw --v 7
```

**Fixed Seed 鎖定（三輪流程）：**

第一輪（探索性，20~30 張）→ 第二輪（收斂精修）→ 第三輪（六基準圖）

| 欄位 | 數值 |
|------|------|
| Primary Seed | |
| Backup Seed 1 | |
| Backup Seed 2 | |
| 鎖定日期 | |
| 基準圖存放路徑 | assets/characters/CHAR-[編號]/ |

**六基準圖規格：**

| 基準圖 | 情緒溫度 | 用途 | 生成狀態 |
|--------|---------|------|---------|
| 正面 MCU 55 | 55 | 主採訪參考 | |
| 正面 MCU 85 | 85 | 情感高點參考 | |
| 正面 MCU 90 | 90 | 最高光鏡頭 | |
| 正面 CU 75 | 75 | 靜幀參考 | |
| 半身 MS 50 | 50 | B-roll 參考 | |
| 正面 MCU 78 | 78 | CTA 銜接段 | |

**IP-Adapter 強度設定：**

| 鏡頭類型 | 強度 |
|---------|------|
| 主採訪特寫（MCU / CU）| 0.88 |
| 半身 B-roll | 0.82 |
| 背影 / 手部特寫 | 不需要 |

**一致性驗收三要素：**
- 下巴輪廓線：臉型不漂移
- 眼鏡框形狀：規格一致
- 鼻樑結構：寬度一致

**Negative Prompt：**
```
smooth airbrushed skin, stock photo posing, fake smile,
obvious staged interaction, low quality, blurry, watermark,
text overlay, cartoon, anime, western facial features,
overly dramatic expressions, CGI render, oversaturated colors
```
