# BoshiahkGV - 嘸蝦殼 GDI+ Version。
免安裝的嘸蝦米輸入工具，以 AutoHotkey 搭配 GDI+ 寫成。  
本程式會攔截鍵盤事件，所以會被某些掃毒軟體誤判，附上掃毒結果給大家參考：[連結](https://www.virustotal.com/gui/file/422deefb3964342c442799d0f60b97d8a6c3b90c7b0e8d9416257cba83ea509d/detection)

身為嘸蝦米輸入法的使用者，我非常能夠體會沒有嘸蝦米輸入法可用時的窘境。  

我也曾經用過能夠使用嘸蝦米輸入的框架，如 RIME、PIME，以及可以免安裝的小小輸入法，這些輸入法框架雖然都能夠套用嘸蝦米的表格，但是使用上總是不那麼順手，我在接觸了 AutoHotkey 一段時間之後，突然想到可以試著用 AutoHotkey 設計一個專屬嘸蝦米輸入法的工具。  

本程式選擇以 GDI+ 來繪製介面，可以依據輸入的字根與可選字調整介面的寬度，即態動顯示。

經過幾次的改良，加上自己也喜歡簡潔的介面，輸入工具的介面最後修改成現在的版本，將來也會維持目前的簡潔的介面。

只要 Autohotkey 能在 Windows 上執行，這個工具都會持續維護，也感謝 PTT 的蝦友們提出程式使用上的問題，協助我修正，讓程式更加完善。

### 更新 2021-06-20
- 新增: Shift + `,.[]'` 符號可以設定送下排，用 shift_altered 值設定。
- 修正: 修正游標跟隨內部計算錯誤，並於 INI 加上兩個設定值 `floating_offset_x` 與 `floating_offset_y`，可以調整跟隨模式的偏移量。

### 更新 2021-06-19
- 修正: 跟隨游標模式下，正常狀況下可以隨游標高度調整位置，也會有例外，如果不行一樣關閉此功能即可。  
之後的做法會朝向可讀取一份清單，是能夠將不支援游標跟隨的程式自動停止使用，不過這個要花比較長的時間來評估與測試可行性了....  
目前在Windows GUI元件、Chrome、Office Word 中可以正常跟隨游標，而 Line 雖然有小問題，但仍然能跟隨游標。

# 輸入畫面範例  
![image](https://github.com/yurenli0217/Temp/blob/main/Example2.gif?raw=true)
![image](https://github.com/yurenli0217/Temp/blob/main/Example.gif?raw=true)  

# 下載方式如下圖  
![image](https://github.com/yurenli0217/Temp/blob/main/Download.png?raw=true)

# 使用說明
- 解壓縮後執行 Boshiashk.exe 即可使用，程式預設會在螢幕左下角顯示「嘸」的字樣。  
- `tbl`資料夾內放的是表格檔，`font`資料夾放的是 ttf 或 ttc 的字型檔。  
- 程式執行時，會載入 `tbl\pos.ini` 儲存的座標位置，輸入介面有變更位置時會更新此檔案。刪除此檔執行時預設會在螢幕左下角。

## 程式基本內建功能
- 對介面按右鍵可結束程式，按中鍵重新載入
- Ctrl-Alt-X 離開程式
- Ctrl-Alt-R 重新載入程式設定
- Ctrl-Alt-L 切換送字時是否顯示該字的拆碼
- Ctrl-Alt-C 可以直接對已選取的單個中文字複製查碼
- Ctrl-Space 輸入法開啟/關閉
- Shift-Space 半形/全形 輸入
- 可以修改套用不同的表格檔
- 修改介面字體大小與樣式
- 可用 Shift 或 CapsLock 切換 中/英 模式 (INI需設定)
- 內建功能碼與其餘可選功能，參閱 INI 檔內說明。

## 程式的設定可參閱 `Boshiahk.ini`，檔案內的各項設定項目都有說明。
### 如果 boshiahk.ini 文字編碼格式不是 UTF-16LE，程式無法正常讀檔執行，用記事本開啟另存成 UTF16-LE 即可。這是 windows 本身的限制。

# 查詢功能
1.查詢同音字: 先輸入單引號(`'`)，再輸入字根，選完字即可查詢同音字。  
2.查詢注音: 先輸兩個單引號(`''`)再輸入字根，選完字即可查詢注音。
![image](https://github.com/yurenli0217/Temp/blob/main/Example_phon.gif?raw=true)   

3.用注音查字
先輸入切換到注音模式的功能碼，會出現「注:」，可輸入注音，輸入完後按下空白鍵便會出現同音字。
![image](https://github.com/yurenli0217/Temp/blob/main/Example_Query2.gif?raw=true)  

4.萬用字元查碼
先輸入`[`，再輸入字根，不知道的字根用`.`來表示，輸入完按下空白鍵便會出現符合的候選字。  
![image](https://github.com/yurenli0217/Temp/blob/main/Example_query.gif?raw=true)  

# 系統輸入法和語系設定
嘸蝦殼輸入介面的運作屬外掛方式輸入中文，若要正常運作，系統內建的輸入法要先進行設定。  
系統的語言設定和輸入法設定可以參照以下兩種方式:  
1. 語系設定成英文語系  
![image](https://github.com/yurenli0217/Temp/blob/main/LangSetting2.png?raw=true)  
此模式下使用外掛式中文輸入最穩定，但若是遇到某些應用程式需要系統輸入法在中文語系下才能輸入中文時，就必須要使用第二種方法。

2. 輸入法設定成倉頡英數模式(非必要時不建議)  
![image](https://github.com/yurenli0217/Temp/blob/main/LangSetting1.png?raw=true)  
設定成倉頡輸入法，可以配合 INI 設定項 `sys_ime_patch`，程式會自動監控將系統輸入法狀態維持在英數模式。

# TblConv.exe 指令參數
來源檔案，像是 CIN、小小輸入法、IBUS 的表格檔，檔內會有一些專屬的格式設定內容，要先刪除，只留下字碼對應表，如

a 對  
b 八  
c 七  
ix 我 曳  
miwi 衛  
miwi 衍  

再進行轉換才不會有問題。

#### 指令格式: TblConv [ftype=ibus] [passExt=1] src=source_table out=output_file
#### 參數說明:
- `ftype=ibus` 使用的來源檔案是 ibus 格式
- `passExt=1` 略過從擴展區B開始的少用字
- `src` 指定來源檔名
- `out` 指定輸出檔名

# 歷史更新
### 2021-06-18
- 修正: 到螢幕右側超出螢幕邊緣寬度不夠時位置錯誤
- 新增: 簡易的游標跟隨功能，INI設定`[MAIN]`中加入`floating_mode`，`[cmd]`中加入`cmd_floating`。
如果有遇到不支援會亂跑的，可先用功能碼關閉。

### 2021-06-15
- 輸入介面文字顯示位置設定微調
- 一樣有 32 位元與 64 位元可以選擇使用。
32位元和64位元版本會被不同的防毒軟體擋下，真的很奇妙。

### 2021-06-13
- 介面稍做調整以及更新 INI 檔，補充一些說明。
- 新增: 可用 `<` 和 `>` 切換上一頁和下一頁。
- 變更: Hook 模式感覺支援度較好，此版本的熱鍵設定直接改用 Hook 模式。
- 新增: TblConv.exe，外部表格轉檔工具，請參閱[用法](#tblconvexe-指令參數)

### 2021-06-11
- 修正: 符號對應，我已經將我知道的調整為和官蝦7.0相同了
- 變更: 同音字和注音查詢方式將單引號調整到前面了，即原本的`cox'`改為`'cox`，`cox''`改為`''cox`。
- 新增: INI內，`[style]`區新增 list_gap，設定查注音和拆碼時，各個注音和拆碼的間距。
- 這一次有兩個版本的執行檔，一為原始的熱鍵設定，另一個為熱鍵全部用 Hook 模式，主要是請大家測試原本遇到 Ctrl-Space 無法切換的程式，
是否可以正常切換。測試前可以先將輸入法狀態開啟，然後執行程式，遇到切換熱鍵失效時，可以對`嘸`按中鍵重新載入，再試著切換看看。
我自己所使用到的程式都可以在原始設定下正常切換，所以無法確認 Hook 模式是否能改善。

### 2021-06-08
- 修正: CapsLock 開啟時，Shift 搭配英數鍵的功能會反轉。

### 2020-06-04
- 修正在英文輸入模式下，鍵盤開啟大寫模式時無法輸出大寫英文字母的問題。
- 如果要使用我提供參考官方製作的表格檔，可以開啟內部 vrsf 選字修補功能，可以開啟功能玩看看，開啟方式:

default=Liu_CJK,嘸,1

### 2021-06-03
- 新增: 三個參考官方的表格檔。Liu_CJK.txt 為預設表格檔，Liu_T2S.txt 為打繁出簡表格檔，Liu_JAP.txt 為日文表格檔。
這三個表格檔的字集範圍較少，很多擴展區的字沒有加入，但日常生活輸入已足夠。有需要的可以自替換。

### 2021-06-02
- 修正: 程式內部效能改善
- 新增: `[INI]` rshift_switch，可選擇是否開啟右邊 shift 切換中英模式
- 新增: `[INI]` enter_send_key，可選擇是否開啟 enter 鍵直接送出字根區內容。
Enter 鍵直接送字根的功能不確定是否穩定，如果不穩定請先關閉此功能。
- 變更: Boshiahk.exe 為 64 位元執行檔，舊電腦可以用 32 位元版本的 Boshiahk86.exe

### 先前更新略
