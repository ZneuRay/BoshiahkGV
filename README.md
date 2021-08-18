# BoshiahkGV - 嘸蝦殼 GDI+ Version。
免安裝的嘸蝦米輸入工具，以 AutoHotkey 搭配 GDI+ 寫成。  
本程式會攔截鍵盤事件，所以會被某些掃毒軟體誤判，附上掃毒結果給大家參考：  
[32位元執行檔](https://www.virustotal.com/gui/file/fb751ead2299d46ae6f6afd98fc13bb8cfed3ae28986769ba33216f955f870e6/detection)
[64位元執行檔](https://www.virustotal.com/gui/file/de549b13e2297abfc6b30a71bf84656464ddc7766e8ea9b37c46890f04ec5a3c/detection)

身為嘸蝦米輸入法的使用者，我非常能夠體會沒有嘸蝦米輸入法可用時的窘境。  

我也曾經用過能夠使用嘸蝦米輸入的框架，如 RIME、PIME，以及可以免安裝的小小輸入法，這些輸入法框架雖然都能夠套用嘸蝦米的表格，但是使用上總是不那麼順手，我在接觸了 AutoHotkey 一段時間之後，突然想到可以試著用 AutoHotkey 設計一個專屬嘸蝦米輸入法的工具。  

本程式選擇以 GDI+ 來繪製介面，可以依據輸入的字根與可選字調整介面的寬度，即態動顯示。

經過幾次的改良，加上自己也喜歡簡潔的介面，輸入工具的介面最後修改成現在的版本，將來也會維持目前的簡潔的介面。

只要 Autohotkey 能在 Windows 上執行，這個工具都會持續維護，也感謝 PTT 的蝦友們提出程式使用上的問題，協助我修正，讓程式更加完善。

### 更新 2021-08-18
- 變更: 系統圖示原本要用 ICO 格式，本次更新改成讀取 PNG 圖檔，未來自行更換圖示較方便。

### 更新 2021-08-17
- 新增: 當 show_tray_icon 設定成 1，即顯示系統列圖示時，介面會最簡化，只有在輸入時顯示字根與可選字。  
系統列圖示在切換全形/半形、中/英、剪貼簿時分別會再多出圖示做為提醒。  
對圖示按下右鍵可結束程式。  
系統列圖示會自動隱藏，要設定讓他一直顯示在系統列上，如下圖:  
![image](https://github.com/yurenli0217/Temp/blob/main/TrayIconSetting.png?raw=true)  


### 更新 2021-08-14
- 新增: INI 設定 show_tray_icon，可切換顯示右下角系統列圖示，圖示檔有兩個，在 tbl 資料夾中的 tray1.ico 與 tray2.ico，分別為開啟輸入法與關閉輸入法的顯示圖示。  
這次釋出新增系統列功能是測試長時間使用時，圖示的穩定性。  
未來計畫提供更精簡的模式，在顯示系統圖示的狀態下，隱藏所有輸入狀態提示，僅在輸入時顯示字根與候選字，因此使用者要記得輸入狀態，這算是給進階使用者的功能吧。  
系統列圖示要記得在「工作列設定 > 選取要顯示在工作的圖示」中開啟，這樣才不會自動隱藏。

### 更新 2021-08-10
- 變更: tbl\Clipboard.txt 格式有變更，加入設定值可以指定自動剪貼模式下用 Ctrl + V 或 Shift + Insert，有的程式只支援其中一個，此時就可以指定用何種熱鍵貼上。
原本 INI 內的 paste_hotkey_type 一樣有用，在強制貼剪簿模式下(,,b) 且視窗不在 Clipboard.txt 清單內的會套用此設定值。
- 測試: 內部加入一個特別碼「...m」，可以切換到另一種送字模式，不透過 AHK，而是直接呼叫底層 API 送字，大家可以玩玩看。

### 更新 2021-08-07
- 修正: 「＿＋＇”」符號無法輸出的問題。
- 更新 AutoHotkey 核心，重新編譯並瘦身，這次32位元和64位元經測試，Windows 內建的防毒軟體沒有誤判的情況。

# 輸入畫面範例
![image](https://github.com/yurenli0217/Temp/blob/main/Example3.gif?raw=true)  

# 下載方式如下圖  
![image](https://github.com/yurenli0217/Temp/blob/main/Download.png?raw=true)

# 程式執行前置作業
- AutoHotkey 本身有鍵盤攔截功能，所以有時會被防毒軟體誤判，因此提供四個版本的執行檔，請在解壓縮後，先選擇一個不會被系統誤判的執行檔案。
- `tbl`資料夾內放的是表格檔，`font`資料夾放的是 ttf 或 ttc 的字型檔，UniteTTC.exe 是拆 TTC 字型的工具，遇到不支援的 TTC 可以使用這個工具。  
- 程式執行時，會載入 `tbl\pos.ini` 儲存的座標位置，輸入介面有變更位置時會更新此檔案。刪除此檔案，執行時輸入介面會以預設值顯示在螢幕左下角。

## 輸入介面開啟時，熱鍵與對應的功能
- 對輸入介面按右鍵可結束程式，按中鍵重新載入
- Ctrl-Alt-X 離開程式
- Ctrl-Alt-R 重新載入程式設定
- Ctrl-Alt-L 切換送字時是否顯示該字的拆碼
- Ctrl-Alt-C 可以直接對已選取的單個中文字複製查碼
- Ctrl-Alt-Shift-C 查看焦點視窗的 Class Name 並複製到剪貼簿中。
- Ctrl-Space 輸入法開啟/關閉
- Shift-Space 半形/全形 輸入
- Shift+,. 在多頁選字時，切換上下頁
- Pgup/Pgdn 在多頁選字時，切換上下頁

## 修改 Boshiahk.ini 簡易說明
- 設定檔中已有針對各項設定值簡述用法
- 設定檔分成 `[Main]`、`[Style]`、`[Table]`、`[Cmd]` 四個區段，請留意不要刪除。
- 修改輸入介面的字型檔案可以用 TTC 或 TTF 格式，其中 TTC 會因檔案格式會有可能不支援，解決方式就是使用 Font 資料夾內的 UniteTTC.exe 將 TTC 拆成 TTF，然後再保留要使用的 TTF。
- 使用程式前可先詳細參閱 INI 檔內說明。
### ※注意※ 如果 boshiahk.ini 文字編碼格式不是 UTF-16LE，程式將無法正常讀取設定，用記事本開啟另存成 UTF16-LE 即可。這是 windows 本身的限制。

## Tbl\Clipboard.txt
- 檔案內容為視窗的 Class Name 清單，或是視窗標題，程式執行時會讀取該檔。
- 開啟輸入介面時，若是焦點視窗有符合 Class Name 或視窗標題，就會自動以剪貼簿送字。
- 熱鍵: Ctrl-Alt-Shift-C 查詢焦點視窗的 Class Name。
- 熱鍵: Ctrl-Alt-Shift-T 查詢焦點視窗的視窗標題。

如果想要符合的是 Class Name，每一行用*開頭，後面接 Class Name，如  
`*Notepad`  
只要 Class Name 為 Notepad 的都會自動用剪貼簿貼上。  

如果想要符合的是視窗標題，每一行直接輸入視窗標題包含的字串，如  
`批踢踢實業坊`  
視窗標題只要包含此字串，就會自動以剪貼簿送字。  
視窗標題也可以支援正規表示法比對字串，這是比較進階的用法，有興趣的可以試試。  
視窗標題比對時的英文大小寫視為一樣。

## Tbl\fixed.txt
- 檔案內容為視窗的 Class Name 清單，或是視窗標題，程式執行時會讀取該檔。  
- 開啟輸入介面時，若是焦點視窗有符合 Class Name 或視窗標題，會強制停用游標跟隨功能。  
- 熱鍵: Ctrl-Alt-Shift-C 查詢焦點視窗的 Class Name。
- 熱鍵: Ctrl-Alt-Shift-T 查詢焦點視窗的視窗標題。   
- 檔案格式同上方 Clipboard.txt

### 游標跟隨在雙螢幕會有些問題，目前已測試的情況:  
1.Chrome 在延伸螢幕會無法取得輸入游標位置。  
2.Office、Line 沒有問題。  
3.原生 GUI 沒有問題。  
4.部分程式如 Notepad++ 會因為雙螢幕的縮放比例不同，造成程式抓游標位置不正確，修正方式就是把兩台螢幕的 DPI 設定調成一樣。  

# 查詢功能
1.查詢同音字: 先輸入前導碼 `'[`，再輸入字根，選完字即可查詢同音字。  
2.查詢注音: 先輸入前導碼 `''[`再輸入字根，選完字即可查詢注音。  
3.用注音查字: 先輸入前導碼 `';`，會出現「注:」，可輸入注音，輸入完後按下空白鍵便會出現同音字。  
4.萬用字元查碼: 先輸入前導碼 `[`，再輸入字根，不知道的字根用`.`來表示，輸入完按下空白鍵便會出現符合的候選字。  

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
### 2021-08-04
- 修正: 注音模式下「ㄦ、ㄥ」無法輸入的問題。

關於防毒軟體誤判的問題，連我自己也無法倖免。  
目前我自己的工作環境都是用Windows 10 內建的防毒，我確定的是32位元版本的執行檔一定會被誤判，而 64 位元的目前都能正常運作。  
我自己會偏好 64m 的版本，這版執行檔不太會有 VC Runtimes 的相依性，我用在工作場所的電腦都沒問題。

### 2021-08-03
- 新增: 現在 Clipboard.txt 和 Fixed.txt 都可以使用視窗標題和視窗的 Class Name 了。
- 新增: INI 設定值 keep_clip，若是不會影嚮效能，可以試著開啟，在剪貼簿模式下可以保留之前複製的文字。

### 2021-08-02
- 新增: 加入判斷螢幕總解析度的程式碼，在雙螢幕的環境使用跟隨游標會用到。

### 2021-07-31
- 修正: 選字區的數字編號無法自動調整輪廓寬度的問題。

### 2021-07-29
- 修正: 自動剪貼功能內部效能改善。  
原本在每次送字前比對焦點視窗是否符合，經蝦友建議，改成在切換焦點視窗時，預先比對一次焦點視窗是否符合自動剪簿送字。

### 2021-07-28
- 新增: 剪貼簿的自動切換可以使用 Class Name 或是視窗標題。請參閱下方的說明。
- 變更: 因為支援比對視窗標題切換剪貼簿送字，所以將 Class.txt 改為 Clipboard.txt。


### 2021-07-19
- 修正: CapsLock 狀態會受影嚮的問題。修正後，輸入介面開啟時，用 CapsLock 切換中英文輸入模式，CapcLock 狀態不會改變。
- 修正: 不小心把鍵盤 Hook 關閉，造成程式支援度不佳，現已修正。
- 新增: UniteTTC.exe 在 Font 資料夾內，用來處理不支援的 TTC 字型檔案。

### 2021-07-18
- 修正: 跟隨游標功能錯誤修正。

### 2021-07-11
- 新增: tbl\fixed.txt。檔案內存ClassName清單，有在此清單內的視窗，開啟跟隨游標的功能時，會強制關閉跟隨游標功能，檔案內以Notepad為範例給大家試試。
- 這一次上傳四種執行檔，大家可以測試看看自己電腦的哪一個版本不會誤判為病毒，我之前試過 64 位元和 32 位元，不同的執行檔會被不同防軟體誤判，所以只能請大家找一個合適的執行檔了。

### 2021-06-25
- 新增: tbl\class.txt。檔案內容為視窗的 Class Name 清單，程式會讀取該檔，在輸入時，若是焦點視窗 ClassName 有符合的，會自動以剪貼簿送字。檔案內我放了一個 Chrome 的 ClassName 當範例，可以試試看喔。
- 新增: 可以用 Ctrl+Alt+Shift+c 組合鍵查看焦點視窗的 Class Name，並複製到剪貼簿中。
- 修正: 查同音字和查注音的前導碼會跟正常字根碼衝突，先改為 `'[` 查同音字，`''[` 查注音念法。
- 修正: 內部錯誤。

### 2021-06-20
- 新增: Shift + `,.[]'` 符號可以設定送下排，用 shift_altered 值設定。
- 修正: 修正游標跟隨內部計算錯誤，並於 INI 加上兩個設定值 `floating_offset_x` 與 `floating_offset_y`，可以調整跟隨模式的偏移量。

### 2021-06-19
- 修正: 跟隨游標模式下，正常狀況下可以隨游標高度調整位置，也會有例外，如果不行一樣關閉此功能即可。  
之後的做法會朝向可讀取一份清單，是能夠將不支援游標跟隨的程式自動停止使用，不過這個要花比較長的時間來評估與測試可行性了....  
目前在Windows GUI元件、Chrome、Office Word 中可以正常跟隨游標，而 Line 雖然有小問題，但仍然能跟隨游標。

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
