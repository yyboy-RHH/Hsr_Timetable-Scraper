一個基於 Python 的自動化工具，繞過傳統網頁視覺介面，直接透過 HTTP POST 請求與台灣高鐵後台 API 對接，精準萃取並解析 JSON 格式的時刻表資料。

## 核心特色 (Core Features)

- **直接對接核心 (Direct API Request)**：放棄不穩定的網頁 DOM 元素解析，直接封裝查詢條件並發送至高鐵 `TimeTable/Search` 端點。
- **純粹結構化資料 (JSON Parsing)**：接收並處理伺服器回傳的純 JSON 數據，將繁雜的原始資料轉化為清晰的 Python 字典結構。
- **精準提取 (Precision Extraction)**：透過定義明確的資料節點路徑 (`result['data']['DepartureTable']['TrainItem']`)，自動過濾並輸出關鍵乘車資訊（車次、出發時間、抵達時間）。

## 環境要求 (Prerequisites)

執行此 Jupyter Notebook (`Hsr_Timetable-Scraper.ipynb`) 前，請確保已安裝以下 Python 模組：

bash
pip install requests


> **工程師筆記**：腳本中雖有引入 `BeautifulSoup`，但因本專案採用直接解析 JSON API 的作法，實際上無需進行 HTML 解析。未來重構時建議將其移除，以維持程式碼整潔與執行效率。

## 參數設定指南 (Payload Configuration)

要自訂查詢條件，請直接修改腳本中的 `payload` 字典檔。以下為關鍵參數說明：

- `StartStation`: 起點站的英文拼音（例：`BanQiao` 板橋, `NanGang` 南港）
- `EndStation`: 終點站的英文拼音（例：`ZhangHua` 彰化, `ZuoYing` 左營）
- `OutWardSearchDate`: 查詢日期，格式為 `YYYY/MM/DD`（例：`2025/10/02`）
- `OutWardSearchTime`: 查詢時間，格式為 `HH:MM`（例：`12:30`）
- `SearchType`: 預設為 `S` (單程)
- `Lang`: 預設為 `TW` (繁體中文)

## 輸出範例 (Output Example)

程式執行後，將透過迴圈自動印出符合條件的班次列表：

text
Train number: 0803, Departure time: 06:15, Destination time: 08:40
Train number: 0603, Departure time: 06:40, Destination time: 08:50
Train number: 0805, Departure time: 07:00, Destination time: 09:25
...
