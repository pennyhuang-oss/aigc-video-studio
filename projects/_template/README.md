# [品牌] — [專案名稱]

**建立方式：** 複製 `projects/_template/` 目錄，重新命名為 `projects/[品牌代碼]-[專案代碼]/`  
**開工前：** 先完成 `production-brief.md` 的四鎖確認

## 檔案清單

| 檔案 | 說明 | 狀態 |
|------|------|------|
| `production-brief.md` | G0 製作 Brief（四鎖 + 預算 + 時程）| 🔴 開工前必須完成 |
| `00-project-overview.md` | 專案總覽、RACI、時程 | 🟡 G0 完成後建立 |
| `01-scripts.md` | 腳本 | 🟡 Phase 1 |
| `02-aigc-specs.md` | AIGC 規格書 + Prompt 庫 | 🟡 Phase 2 |
| `03-asset-tracker.md` | 素材授權清單 | 🟡 Phase 2 |
| `04-qc-report.md` | QC 報告 | 🟡 各 Gate |
| `05-publish-tracker.md` | 發布追蹤與效果數據（各平台 KPI、UTM、30 天報告）| 🟡 發布後 |
| `07-audio-design.md` | 音頻設計規格（品牌聲音語言、Suno Prompt、ElevenLabs 規格）| 🟡 Phase 2 開始時 |
| `08-production-log.md` | 每日製作日誌 | 🟡 Phase 2 開始 |
| `10-scene-design.md` | 場景設計規格（S-A/B/C/D 四種場景類型、MJ Prompt 模板）| 🟡 G1 通過後 |
| `12-aigc-workflow-EPxx.md` | AIGC 製作工作流（鏡頭對照表、逐日時程、品質標準）| 🟡 G1 通過後 |
| `13-notos-production-plan.md` | Notos 平台備援製作計劃（Seedream + Seedance）| 🟡 選用 |

## 子目錄

| 目錄 | 說明 | 使用時機 |
|------|------|---------|
| `aigc-scripts/` | Python 自動化腳本（批次 Prompt 生成）| Phase 2，需生成多集素材時 |
| `coherence/` | 場景連貫性驗證（D1-D7 七維度品質評分）| G2 素材審核前必須執行 |

## 製作流程快速參考

```
G0 企劃確認
  └── production-brief.md（四鎖）
  └── 00-project-overview.md（RACI + 時程）

G1 腳本確認
  └── 01-scripts.md（雙層檢查表）
  └── 10-scene-design.md（場景設計）
  └── 12-aigc-workflow-EPxx.md（工作流 + 鏡頭表）

G2 素材確認
  └── 02-aigc-specs.md（Prompt 庫）
  └── aigc-scripts/（自動化生成）
  └── coherence/（品質驗證，必須通過）

G3 初剪確認
  └── 08-production-log.md（日誌）
  └── 07-audio-design.md（音頻規格）

G4 終剪確認
  └── 04-qc-report.md

G5 發布準備
  └── 05-publish-tracker.md（發布文案 + UTM + KPI）
```

## 工具選用決策

| 情境 | 建議工具 |
|------|---------|
| 主要圖生影工作流 | Midjourney v7 + Kling AI 2.0（Workflow C）|
| UI / 介面操作展示 | Wan 2.7（Workflow B）|
| 攝影機路徑控制 | Sea Dance 2（Workflow A）|
| 後製合成 / 字幕 / GFX | After Effects（Workflow D）|
| 備援 / 低成本替代 | Notos（Seedream + Seedance，見 13-notos-production-plan.md）|
| 背景音樂 | Suno AI（規格見 07-audio-design.md）|
| 旁白 TTS | ElevenLabs（規格見 07-audio-design.md）|
