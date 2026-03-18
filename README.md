

# EchoTransc 🚀

**EchoTransc** 是一款輕量化、免顯卡（GPU-free）的即時語音翻譯工作台。它結合了 **Vosk 離線辨識** 技術與 **Gemma 3 (Ollama)** 的高級 AI 精修能力，並具備 Google 翻譯無縫備援機制，旨在為演講聽寫、課程紀錄提供最穩定且高品質的雙語對照體驗。

---

## 🌟 核心特色

- **雙引擎翻譯架構**：
  - **即時快譯 (Google)**：利用 Google 翻譯提供毫秒級的視覺反饋，確保字幕流暢不卡頓。
  - **AI 高品質精修 (Gemma 3)**：在語音停頓（0.3s）時觸發 Gemma 3 進行深度語境理解與優雅修辭，產出專業課程紀錄。
- **無縫備援機制 (Fallback)**：若 AI 伺服器斷線或回應超時，系統將自動切換回 Google 翻譯存檔，確保紀錄不中斷、不遺失。
- **免顯卡負擔**：語音辨識部分（Vosk）完全在 CPU 運行，普通筆電也能流暢執行，將 GPU 資源保留給其他開發需求或 AI 運算。
- **多語模型切換**：支援動態載入多組 Vosk 模型資料夾（如：英文快速、日文品質佳），透過介面一鍵切換。
- **右側歷史紀錄**：自動彙整中英對照紀錄，支援一鍵匯出為 `.txt` 檔案。

---

## ⚙️ AI 配置與運行建議

本專案目前的設計重點在於「資源分配」與「靈活性」：

1. **AI 服務建議**：
   - 推薦使用 **自己搭建的伺服器** 或 **本機 Ollama 服務**。
   - 由於語音辨識（Vosk）主要消耗 **CPU** 運算力，若將 AI 翻譯也放在本機且同樣使用 CPU 運算，可能會造成短暫的卡頓。
   - **理想配置**：如果您的 **GPU** 顯存足夠（例如 8G VRAM 以上），建議讓 Ollama 運行在 GPU 上，這樣 CPU 專心負責聽寫，GPU 負責翻譯，兩者並行可達到最佳效能。

2. **API 位置設定**：
   - **注意**：目前版本尚未提供在 UI 介面上更改 API 位置的功能。
   - 請在執行或打包前，直接於 `app.py` 程式碼頂部修改以下參數：
     ```python
     # 設定您的 AI 伺服器網址 (OpenAI 相容格式)
     API_URL = "http://你的伺服器/v1/chat/completions"
     MODEL_NAME = "gemma3:12b" # 可更換你喜歡的模型
     ```

---

## 🛠️ 環境準備

1. **安裝依賴套件**：
   ```bash
   pip install vosk pyaudio deep-translator pyperclip pyttsx3 numpy requests
   ```

2. **下載語音模型**：
   請至 [Vosk Models](https://alphacephei.com/vosk/models) 下載所需模型。

3. **資料夾結構**：
   為了讓程式能自動偵測模型，請保持以下結構（資料夾名稱建議使用英文，避免亂碼）：
   ```text
   EchoTransc/
   ├── app.py
   └── model/
       ├── en_fast/       (英文快速模型)
       ├── en_quality/    (英文高品質模型)
       └── ja_quality/    (日文高品質模型)
   ```

---

## 📦 打包為 EXE

若要將本程式打包給其他人使用，請使用 PyInstaller 並確保包含 `vosk` 的所有相依檔案：

```bash
pyinstaller --onefile --windowed --collect-all vosk app.py
```

打包後，請將產出的 `app.exe` 與 `model` 資料夾放在同一個目錄下即可運行。

---

## 📝 免責聲明

本專案主要用於個人學習與學術演講紀錄。請確保在法律允許的範圍內錄製音訊，並尊重講者的智慧財產權。AI 翻譯結果僅供參考。

---

### 👨‍💻 開發者
**[ddmmbb]** 歡迎提供建議與 Pull Request，讓我們一起完善 **EchoTransc**！
