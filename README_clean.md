# 面試分析系統（Whisper + Gemini + HEXACO）

本專案是一套整合 OpenAI Whisper 語音辨識模型與 Gemini API 的人格分析系統，能將面試影音檔自動轉為逐字稿、格式化問答內容，並透過 Gemini 產生 HEXACO 六大人格特質分析，最終輸出為 PDF 報告並於網頁顯示。

---

## 系統功能流程

1. 上傳面試影音（支援 .mov / .mp4 / .m4a）
2. 使用 Whisper 將語音轉為逐字稿
3. 使用 Gemini 將逐字稿格式化為 問題/回答 格式
4. 使用 Prompt Engineering 進行 HEXACO 分析（六大人格特質）
5. 匯出格式化 Q&A + 分析結果為 PDF（支援中文）
6. 即時顯示於 Gradio 前端網頁

---

## 系統流程圖

請於 GitHub 上傳 SVG 檔後，使用下列語法顯示流程圖：

```
<img src="https://github.com/你的帳號/你的倉庫/blob/main/flowchart.svg" alt="系統流程圖" width="600"/>
```

---

## 安裝依賴套件

請先建立虛擬環境（建議 Python 3.8~3.11），再執行：

```bash
pip install -r requirements.txt
```

若你沒有 `requirements.txt`，可手動安裝：

```bash
pip install git+https://github.com/openai/whisper.git
pip install gradio fpdf pandas python-dotenv google-generativeai
```

---

## Whisper 相依的 ffmpeg 安裝（Windows）

Whisper 需要 `ffmpeg` 來轉換音訊格式，本專案僅支援 Windows 使用方法一：

### 方法一：透過 Chocolatey 安裝

1. 確保你有安裝 Chocolatey：https://chocolatey.org/install
2. 開啟 PowerShell（以系統管理員身份執行）
3. 執行以下指令：

```powershell
choco install ffmpeg -y
```

4. 安裝完成後，重啟 terminal，輸入：

```bash
ffmpeg -version
```

若成功顯示版本號，即代表安裝完成。

---

## 設定 API 金鑰

請在專案根目錄建立 `.env` 檔案，格式如下：

```env
GEMINI_API_KEY=你的_Gemini_API_Key
```

你可以到 https://aistudio.google.com/app/apikey 取得你的 Gemini 金鑰。

---

## 執行程式

```bash
python ds-final.py
```

Gradio 啟動後將顯示本機網址（如 http://127.0.0.1:7860），在瀏覽器開啟即可使用。

---

## PDF 中文字型處理

本系統預設使用 `kaiu.ttf` 作為中文 PDF 字型，避免亂碼。
若你系統無此字型，請修改 `get_chinese_font_file()` 指向其他可用的 `.ttf` 字型（不可使用 .ttc）。

---

## 輸出內容說明

產出報告包含：

- 格式化面試逐字稿（問答）
- HEXACO 分析（含：評分、涵義、行為觀察、風險、證據）
- 中文支援、段落標示清楚、可列印或提交使用
