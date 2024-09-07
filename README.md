# Script Spider

## 說明
Script Spider 是一個以 Selenium 為基礎的網路爬蟲程. 主要特點是可以透過 Script 來控制 Spider 行為, 不需要每換一個網站就要改一次程式.

## Script 語法
Script 為 UTF-8 格式的純文字檔, 每行都是一個獨立的指令. 開頭為 --- 表示為註解, 可以使用空格及 Tab 來內縮以方便閱讀. 也可以用空白行來分隔不同區塊以增加 Script 的可讀性.

以下為一段 Script 範例及對應說明:

```
-- define parameters
Define testUrl https://www.momoshop.com.tw/main/Main.jsp
Navigate $(testUrl)
Click #keyword
Input 測試  試紙
Click #topSchFrm button
```

| Script                                                       | 說明   |
|--------------------------------------------------------------|-------------|
| -- define parameters                                         | 註解 |
| Define testUrl https://www.momoshop.com.tw/main/Main.jsp     | 定義變數 |
| Navigate $(testUrl)                                          | 瀏覽網頁 |
| Click #keyword                                               | 使用 CSS Selector 搜尋元件並點擊 |
| Input 測試 試紙                                              | 輸入文字: "測試 試紙" |
| 瀏覽網頁 https://www.momoshop.com.tw/main/Main.jsp           | 瀏覽網頁 (使用中文指令) |
| 點擊元件 #topSchFrm button                                   | 使用 CSS Selector 搜尋元件並點擊 (使用中文指令) |

## 指令說明
如上面的範例所示, 指令可以使用中文或英文. 以下列出目前所有支援的指令:

### 定義變數
- 指令名稱:
  - 英文: Define
  - 中文: 定義變數
- 參數:
  1. 變數名稱: 用來記錄這個變數的名稱, 不能含有空格. 定義成功後, 可以使用 $(var) 來使用.
  1. 變數內容: 要記錄的內容, 可以直接輸入, 也可以用變數指定.

### 瀏覽網頁
- 指令名稱:
  - 英文: Navigate
  - 中文: 瀏覽網頁
- 參數:
  1. 網址: 要瀏覽的網址, 可直接輸入, 或使用變數來指定.



跳出迴圈	Break
點擊元件	Click
關閉頁籤	CloseTab
定義變數	Define
下載檔案	Download
結束判斷	End
搜尋元件	Find
取得元件	Get
條件判斷	If
輸入文字	Input
進入迴圈	Loop
瀏覽網頁	Navigate
回到開頭	Next
剖析字串	ParseText
中場休息	Sleep
切換頁籤	SwitchTab
