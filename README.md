# 影音製作企劃室 — Video Production Studio

> 以 AIGC 為核心，為品牌製作高轉換率宣傳影片的標準化作業框架。
> 架構源自 AI Token King 見證影片系列（EP.01~EP.06）的實戰沉澱。

---

## 理念

**先鎖定，再生產。** 每支影片開工前，必須鎖定「規格 / 產品真相 / 品牌資產 / 製作方式」四件事。  
**用真實，不用想像。** UI 截圖、品牌色、吉祥物、網域——去取用，不去發明。  
**顆粒度對齊產能。** 規劃只做「最後真的會有人照著做」的部分。

---

## Repo 結構

```
video-production-studio/
├── README.md                   # 本文件
├── docs/
│   ├── production-framework.md     # 製作框架總覽（5 Phases + 4 Gates）
│   ├── aigc-tool-chain.md          # AIGC 工具鏈規格（Midjourney/Kling/Sea Dance/Wan/Suno）
│   ├── witness-video-skill.md      # 見證影片製作通用 Skill（開工前四鎖）
│   ├── visual-direction-guide.md   # 視覺導演規格（豎屏三鐵則）
│   └── qc-checklist.md             # 品質驗收清單
├── templates/
│   ├── 00-project-overview.md      # 專案總覽範本
│   ├── 01-scripts.md               # 腳本範本（三段式敘事結構）
│   ├── 02-aigc-specs.md            # AIGC 規格書範本
│   ├── 03-asset-tracker.md         # 素材追蹤清單範本
│   ├── 04-qc-report.md             # QC 報告範本
│   ├── 05-publish-tracker.md       # 發布追蹤範本
│   ├── 08-production-log.md        # 製作日誌範本
│   ├── 09-character-bible.md       # 角色聖經範本
│   └── production-brief.md         # G0 製作 Brief（一頁）
├── skills/
│   └── witness-video-production-skill.md   # Claude Skill 格式（可直接安裝）
├── projects/
│   └── _template/               # 新專案複製此目錄
│       ├── 00-project-overview.md
│       ├── 01-scripts.md
│       ├── 02-aigc-specs.md
│       ├── 03-asset-tracker.md
│       ├── 04-qc-report.md
│       ├── 05-publish-tracker.md
│       ├── 08-production-log.md
│       └── production-brief.md
└── assets/
    └── brand-kits/              # 品牌素材目錄（各品牌一個子資料夾）
```

---

## 快速開始一個新專案

1. 複製 `projects/_template/` 到 `projects/[品牌代碼]-[專案代碼]/`
2. 開 G0 會議，逐項完成 `production-brief.md` 的四鎖確認
3. 依 `docs/production-framework.md` 的 5 Phases 推進
4. 每個 Gate 前完成對應的 QC 清單

---

## 適用影片類型

- **見證影片**（User Testimonial）：B2B / B2C 使用者真實故事
- **品牌宣傳片**（Brand Film）：品牌定位與核心價值傳達
- **產品展示影片**（Product Demo）：功能展示 + 使用場景
- **案例研究影片**（Case Study）：數字驅動的成效呈現

---

## 核心工具鏈

| 用途 | 工具 |
|------|------|
| 靜態場景圖 | Midjourney v7 |
| 動態 B-roll | Kling AI 2.0 |
| 攝影機運動 | Sea Dance 2 |
| UI 操作動態 | Wan 2.7 |
| 後製合成 | After Effects |
| AI 音樂 | Suno AI |
| TTS 旁白 | ElevenLabs（繁中）|
| 口型同步 | HeyGen |

---

## 版本記錄

| 版本 | 日期 | 說明 |
|------|------|------|
| v1.0 | 2026-06-25 | 初版建立，源自 AITokenKing testimonial-videos 實戰架構 |
