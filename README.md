# Script Spider

## 說明
Script Spider 是一個以 Selenium 為基礎的網路爬蟲程式. 主要特點是可以透過 Script 來控制 Spider 行為, 不需要每換一個網站就要改一次程式.

## Script 語法
Script 為 UTF-8 格式的純文字檔, 每行都是一個獨立的指令. 開頭為 --- 表示為註解, 可以使用空格及 Tab 來內縮以方便閱讀. 也可以用空白行來分隔不同區塊以增加 Script 的可讀性. 所有的指令都有中英文版本, 可參考下面範例.

以下為一段簡短 Script 範例及對應說明:

```
-- define parameters
Define testUrl https://www.momoshop.com.tw/main/Main.jsp

-- MOMO
Navigate $(testUrl)
Click #keyword
Input 測試  試紙
Click #topSchFrm button

-- Google
瀏覽網頁 https://www.google.com.tw/
點擊元件 textarea[name="q"]
輸入文字 Test
```

說明
| Script                                                       | 說明                                         |
|--------------------------------------------------------------|----------------------------------------------|
| --- define parameters                                        | 註解                                         |
| Define testUrl https://www.momoshop.com.tw/main/Main.jsp     | 定義變數                                      |
|                                                              | 空白行                                       |
| --- MOMO                                                     | 註解                                         |
| Navigate $(testUrl)                                          | 瀏覽網頁                                      |
| Click #keyword                                               | 使用 CSS Selector 搜尋元件並點擊               |
| Input 測試 試紙                                               | 輸入文字: "測試 試紙"                          |
|                                                              | 空白行                                        |
| --- Google                                                   | 註解                                         |
| 瀏覽網頁 https://www.google.com.tw/                           | 瀏覽網頁 (使用中文指令)                        |
| 點擊元件 textarea[name="q"]                                   | 使用 CSS Selector 搜尋元件並點擊 (使用中文指令) |
| 輸入文字 Test                                                 | 輸入 Test 文字 (使用中文指令)                  |
```
PS. 詳細 Script 範例可以參考 8Comic_eng.script / 8Comic_cht.script
```


## 指令說明
以下列出目前所有支援的指令:

### 補助指令

-  註解
  - 指令格式:
    - ---
  - 指令說明:
    - 所有以 --- 開頭的都是註解
    - --- 之前可以有空白, 但不支援在指令後增註解, 如下例:
      - Navigate https://url --- Error, Cannot add remark after command

- 定義變數
  - 指令格式:
    - Define {key} {value}
    - 定義變數 {key} {value}
  - 指令說明:
    - 定義變數供之後使用
    - {key} 變數名稱, 不可使用空白字元, 也不可使用其他變數.
    - {value} 變數內容, 前後不需要使用雙引號, 如果有加雙引號的話, 會視為變數內容. 可以直接輸入內容, 也可以用其他已經定義過的變數.
    - 變數定義成功後, 可以用 $(key) 來使用
  - 特別說明:
    - 除了自定變數, 目前還有下列的預設變數可以使用:
      - ${loop}: 在 Loop 迴圈中取得目前 Loop Index, 如果不在迴圈中, 會直接忽略.
      - ${prevText}: 取得前一個指令擷取的內容. 如果之前沒有執行過任何一個會擷取字串的指令, 則內容為空字串.

- 用 Regular Express 剖析字串並擷取內容
  - 指令格式:
    - ParseText {text} {pattern}
    - 剖析字串 {text} {pattern}
  - 指令說明:
    - 使用 Regular Express 剖析字串
    - {text} 要被剖析的字串, 如果字串包含空白, 要用雙引號包住.
    - {pattern} 用來剖析字串的 Pattern. , 如果包含空白, 要用雙引號包住. 可以使用 (?<target>) 來指明要擷取的內容.
    - 如果 {pattern} 沒有指定 <target>, 則會擷取第一個符合 Pattern 的 group (?:) 內容.
    - 以下為範例及說明:
      - ParseText "Page: 3/10" "(?<target>\d+)/"
        - 從 "Page: 3/10" 中擷取 "3"
      - ParseText "Page: 3/10" /(\d+)
        - 從 "Page: 3/10" 中擷取 "10"

- 暫停指令執行
  - 指令格式:
    - Sleep {duration}
    - 中場休息 {duration}
  - 指令說明:
    - 休息一段時間後, 再繼續執行下一個指令.
    - {duration} 要暫停的秒數. 如果秒數為負數, 則會隨機暫停一段以其數值為上限的秒數.

### 瀏覽器相關指令

- 瀏覽網頁
  - 指令格式:
    - Navigate {url}
    - 瀏覽網頁 {url}
  - 指令說明:
    - 直接輸入網址瀏覽特定網頁
    - {url} 為網址, 可使用變數, 不可有空挌.

- 切換頁籤
  - 指令格式:
    - SwitchTab {tab-index}
    - 切換頁籤 {tab-index}
  - 指令說明:
    - 切換到某個頁籤
    - {tab-index} 為頁籤編號, 從 0 開始.

- 關閉頁籤
  - 指令格式:
    - CloseTab {tab-index}
    - 關閉頁籤 {tab-index}
  - 指令說明:
    - 關閉到某個頁籤
    - {tab-index} 為頁籤編號, 從 0 開始. 如果關閉的頁籤編號為 0, 會關閉整個瀏覽器.

### 網頁元件操作指令

搜尋元件	Find
取得元件	Get
點擊元件	Click
輸入文字	Input
下載檔案	Download

### 流程控制指令

條件判斷	If
結束判斷	End
進入迴圈	Loop
回到開頭	Next
跳出迴圈	Break

