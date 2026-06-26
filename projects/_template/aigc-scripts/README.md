# aigc-scripts — Python 自動化腳本目錄

此目錄包含用於自動化 AIGC 影片製作流程的 Python 腳本，減少重複性的 Prompt 管理工作，支援批次生成與版本追蹤。

---

## 目錄結構

```
aigc-scripts/
├── README.md              # 本文件
├── api_client.py          # API 連接客戶端（Midjourney / Kling / ElevenLabs）
├── config.py              # 環境設定與全域參數
├── ep_prompts.py          # 本集所有鏡頭的 Prompt 定義
└── generate_ep.py         # 主執行腳本，批次生成素材
```

---

## 各腳本功能說明

### `api_client.py`
封裝對各 AIGC 平台 API 的呼叫，提供統一介面：

- `MidjourneyClient.generate(prompt, seed)` → 送出 Prompt → 等待生成 → 下載圖片，回傳圖片路徑
- `KlingClient.image_to_video(image_path, duration, motion)` → 圖片上傳 → 設定參數 → 等待影片生成 → 下載，回傳影片路徑
- `ElevenLabsClient.text_to_speech(text, voice_id, speed)` → 文字轉語音，回傳 WAV 檔案路徑

**支援的 API：**
- Midjourney（透過 Midjourney API 第三方接口）
- Kling AI 2.0（官方 API）
- ElevenLabs（官方 API）
- Suno AI（透過非官方接口，可選）

### `config.py`
全域設定與環境變數管理：

```python
# 從 .env 載入
MIDJOURNEY_API_KEY = os.getenv("MIDJOURNEY_API_KEY")
KLING_API_KEY = os.getenv("KLING_API_KEY")
ELEVENLABS_API_KEY = os.getenv("ELEVENLABS_API_KEY")

# 品牌設定（每集修改）
BRAND_CODE = "BRAND_XX"   # 替換為實際品牌代碼
EPISODE_NUM = "EP01"

# 輸出目錄
OUTPUT_DIR = f"../_assets/{BRAND_CODE}/{EPISODE_NUM}/"
RAW_VIDEO_DIR = f"{OUTPUT_DIR}video/raw/"
RAW_IMAGE_DIR = f"{OUTPUT_DIR}images/"
AUDIO_DIR = f"{OUTPUT_DIR}audio/"

# AIGC 預設參數
DEFAULT_MJ_VERSION = "--v 7"
DEFAULT_MJ_AR = "--ar 9:16"
DEFAULT_KLING_DURATION = 5    # 秒
DEFAULT_KLING_MOTION = 3      # 1-5
DEFAULT_EL_SPEED = 0.9
DEFAULT_EL_STABILITY = 0.6
```

### `ep_prompts.py`
本集所有鏡頭的 Prompt 清單，使用結構化格式定義每個鏡頭的生成參數：

```python
SHOTS = [
    {
        "shot_id": "S01",
        "scene_type": "S-B",          # S-A / S-B / S-C / S-D
        "workflow": "C",              # A / B / C / D
        "tool": "MJ→Kling",
        "duration": 5,                # 影片秒數
        "motion_intensity": 3,        # 1-5
        "camera_movement": "static",  # static / zoom_in / pan_left / pan_right / tilt_up
        "mj_prompt": "close up of hands holding phone showing bill, late night, cold blue 3800K, stress mood, documentary, 9:16 --ar 9:16 --v 7",
        "mj_negative": "bright colors, happy expression, warm light, cartoon, watermark",
        "mj_seed": None,              # 填入鎖定的 Seed 值（S-A 採訪場景必填）
        "kling_prompt": "subtle hand trembling, authentic stress",
        "description": "深夜帳單 ECU"
    },
    {
        "shot_id": "S03",
        "scene_type": "S-A",
        "workflow": "C",
        "tool": "MJ→Kling",
        "duration": 8,
        "motion_intensity": 2,
        "camera_movement": "static",
        "mj_prompt": "portrait photography, 30s Asian woman confident, office bokeh, 5000K warm, left 45 key light, documentary, 9:16 --ar 9:16 --v 7",
        "mj_negative": "cartoon, anime, watermark, text, logo",
        "mj_seed": None,              # Day 1 完成後填入
        "kling_prompt": "natural breathing, slight blink, authentic interview feel",
        "description": "主角採訪主場景 MCU"
    },
    # ... 繼續填入其他鏡頭
]

VOICEOVER_LINES = [
    {
        "line_id": "VO-01",
        "text": "[旁白文字]",
        "emotion": "neutral",       # neutral / warm / urgent
        "speed": 0.9,
        "shot_ref": "S02"           # 對應鏡頭
    },
    # ...
]
```

### `generate_ep.py`
主執行腳本，讀取 `ep_prompts.py` 並批次執行生成流程：

```bash
# 只生成 MJ 靜態圖（快速驗證 Prompt 方向）
python3 generate_ep.py --mode images

# 只執行 Kling 動態化（需先有靜態圖）
python3 generate_ep.py --mode videos

# 只生成 ElevenLabs 旁白
python3 generate_ep.py --mode audio

# 全部執行
python3 generate_ep.py --mode all

# 只執行指定鏡頭
python3 generate_ep.py --shot S03
```

**功能：**
1. 讀取 `ep_prompts.py` 中的 SHOTS 清單
2. 跳過已生成的鏡頭（防止重複消耗 API 額度）
3. 自動命名輸出檔案（`EP01_S01_mj_base.png`、`EP01_S01_v1.mp4`）
4. 生成後自動更新 `12-aigc-workflow-EPxx.md` 中的狀態欄位
5. 錯誤時記錄到 `generate_ep.log`，不中斷整體流程

---

## 使用方式

### 步驟一：環境設定

```bash
# 建立虛擬環境
python3 -m venv venv
source venv/bin/activate    # macOS / Linux
# .\venv\Scripts\activate   # Windows

# 安裝依賴庫
pip install -r requirements.txt

# 設定環境變數
cp .env.example .env
# 編輯 .env，填入各平台 API Key
```

**`.env.example` 內容：**
```
MIDJOURNEY_API_KEY=your_key_here
KLING_API_KEY=your_key_here
ELEVENLABS_API_KEY=your_key_here
```

### 步驟二：填寫本集 Prompt

1. 複製 `ep_prompts.py`，重新命名為 `ep[XX]_prompts.py`
2. 根據 `12-aigc-workflow-EPxx.md` 的鏡頭列表，填寫每個鏡頭的 Prompt
3. 參考 `10-scene-design.md` 中各場景類型的 Prompt 模板確保格式正確

### 步驟三：執行生成

```bash
# 先只生成靜態圖，快速驗證 Prompt 方向是否正確
python3 generate_ep.py --mode images

# 確認靜態圖品質後，執行動態化
python3 generate_ep.py --mode videos

# 生成旁白音頻
python3 generate_ep.py --mode audio
```

### 步驟四：確認輸出

生成完畢後確認 `_assets/[品牌代碼]/[集數]/` 目錄：

```
_assets/BRAND_XX/EP01/
├── images/
│   ├── EP01_S01_mj_base.png
│   ├── EP01_S03_mj_base.png
│   └── ...
├── video/
│   └── raw/
│       ├── EP01_S01_v1.mp4
│       ├── EP01_S03_v1.mp4
│       └── ...
└── audio/
    ├── EP01_VO-01.wav
    ├── EP01_VO-02.wav
    └── music/
        └── EP01_theme_v1.mp3
```

---

## 依賴庫

```
# requirements.txt
requests>=2.31.0
openai>=1.0.0
python-dotenv>=1.0.0
Pillow>=10.0.0       # 圖片處理（Last Frame 截取）
tqdm>=4.65.0         # 批次生成進度條
```

安裝命令：
```bash
pip install requests openai python-dotenv Pillow tqdm
```

---

## 常見問題

**Q：API 呼叫失敗怎麼辦？**
查看 `generate_ep.log`，確認 API Key 正確，檢查各平台 API 配額是否用盡。

**Q：生成的圖片品質不好，想重試特定鏡頭？**
使用 `--shot [鏡號]` 參數只重跑特定鏡頭，腳本會自動將舊檔案移至 `_archive/` 目錄。

**Q：如何批次更新 Prompt？**
直接修改 `ep_prompts.py` 中對應鏡頭的 `mj_prompt` 欄位，重新執行即可。

**Q：Seed 值何時填入？**
Day 1 完成 S-A 採訪場景靜態圖確認後，從 Midjourney 取得 Seed 值，填入 `ep_prompts.py` 中 `S03` 的 `mj_seed` 欄位，後續同角色鏡頭即可使用相同 Seed。
