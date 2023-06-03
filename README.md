# daochoc zmk frimware for tbkmini
daochoc, zmk config, nrfMicro1.4
![image](https://github.com/ouser555/daochoc/blob/main/pic/ZwHFFmVuw4.png)


## 操作方式
* 左右手燒好各自的燒錄檔後(就是出廠設定)可以兩邊同時按Reset鍵，讓兩邊鍵盤自動配對。

  正常情況下左右邊配對好就會一直保持著，除非刻意去改。
  
* 不使用TRRS線的設計，即使是USB有線模式，左右手鍵盤通訊還是使用無線。  

* 左邊鍵盤為主鍵盤，只有插左邊USB電腦端才會辨識為鍵盤。

* 左邊鍵盤插著USB即為USB模式，USB斷開即為藍牙模式。

* 可先使用USB模式測試左右鍵盤是否有配對成功。

* 藍牙模式與一般藍牙鍵盤配對使用方式無異。

#### 藍牙配對後如果左手有接USB充電，那會變成走USB模式，此時藍牙雖連線著但是不會進行藍牙傳輸，

#### 所以藍牙配對的電腦都沒有辦法輸入，此時把USB充電移除就藍牙可以傳輸了。

#### 充電時必須將鍵盤的開關打開才可充電，TBKMini沒有開關，所以它就是一直保持電源開啟的狀態。

## 藍牙配對切換設定簡易說明
![image](https://github.com/ouser555/daochoc/blob/main/pic/layerdefault.png)
![image](https://github.com/ouser555/daochoc/blob/main/pic/layerlower.png)
![image](https://github.com/ouser555/daochoc/blob/main/pic/layerraise.png)
![image](https://github.com/ouser555/daochoc/blob/main/pic/layeradjust.png)
  * 此鍵盤預設有四層，default/lower/raise/adjust
  * 右手鍵盤靠拇指的下方三個鍵，為方便說明先稱作，左/中/右。想成是筆電的FN鍵就很好理解。
  * 正常情形下都在DEFAULT層。
  * 按住左鍵可以進入LOWER層。放開就回DEFAULT層。單擊一下則是ESC鍵。
  * 按住右鍵可以進入RAISE層。放開就回DEFAULT層。單擊一下則是DEL鍵。
  * 先按住左鍵即進入LOWER層，不放開，接著按右鍵，此時就是LOWER層的右鍵，這個鍵也是設為切層鍵會切到ADJUST鍵。
  * 
  * 左手鍵盤ADJUST層，由上面數來第二排都是設定成BLUE TOOTH的功能鍵。預設可以設定五組配對。
    * 由左往右
    1. Reset
    2. 清除當下這組的配對設定
    3. 切到第0組
    4. 切到第1組
    5. 切到第2組
    6. 切到第3組
    7. 切到第4組
    8. 右手
    9. 切到第4組
    10. 切到第3組
    11. 切到第2組
    12. 切到第1組
    13. 切到第0組
    14. 清除當下這組的配對設定
    15. Reset
  * 所以有時候當下的組別與電腦端無法配對時，就可以利用功能鍵清除配對設定，然後就可以重新配對了。
  * 鍵位詳情看keymap檔就可以知道了。

## 更改按鍵映射功能
  * 目前沒有更改keycode的user interface，只能靠更改程式碼來改變鍵碼。
  
  * 可以用文字編輯器打開 /daochoc/daochoc.keymap 修改需要的鍵碼，然後進行編譯燒錄。
  
  * [https://github.com/ouser555/daochoc/blob/main/daochoc/daochoc.keymap](https://github.com/ouser555/dao-zmk-config/blob/main/config/boards/arm/dao/dao.keymap)
    
    當然是到使用者自己的repo去修改。

## 編譯方式
 
* 1. 在github上建一個帳號，fork這個repo
   
* 2. 進入剛fork到自己github帳號的repo 
     github網頁靠上方橫的標籤頁，選Action
     如果沒看到它自動編譯，選左邊欄位的Build，
     右邊有個run workflow的下拉選單，
     點開選run workflow就會開始編譯。
     稍微等它跑完
     編譯成功後點開往下拉，
     會有firmware.zip可以下載。
     裡面有三個檔案
     左手鍵盤燒錄檔、右手鍵盤燒錄檔、reset燒錄檔，
     如果藍牙配對資料錯亂了就可以燒錄這個reset燒錄檔，
     然後再重燒一次鍵盤燒錄檔即可。
  
  * 之後可以在自己的repo內修改keymap，
    Action選單裡面都會自動編譯，
    稍微等一下就會編譯完成。
  
  * 最近ZMK的改版，要安裝linux開發環境變得繁瑣很多，
    失敗率也很高，所以這邊使用github Action的方式編譯會比較簡單。
    如果要使用本地編譯，請自行參考ZMK官方說明文檔。


## 燒錄方式

* Action頁面下載的firmware.zip資料夾內有left、right左右手的燒錄檔。
  
* 鍵盤連接電腦USB後，連按兩下鍵盤側面的Reset鍵(電源開關旁邊)進入bootloader mode，
  TBKMini沒有拉出Reset鍵的機構，必須要打開鍵盤，連續短接reset和gnd兩次達成同樣操作。

  成功會持續閃綠燈，電腦會把鍵盤辨識為一個隨身碟，
  
  從我的電腦打開這個隨身碟，把zmk.uf2複製進去，
  
  複製完即是燒錄完成，隨身碟會自動退出。
  
* 如果上述燒錄步驟正確的話，鍵盤為新的狀態，但之前已配對的資料還是會保留。

## 常見問題
* Q1:連按兩下Reset鍵進入bootloader模式，綠燈有閃爍，但是沒有辨識成隨身碟。

  A:應該是電腦驅動程式跑掉了。
  * 解決方式:
    1. 換USB孔試試看。
    2. 裝置管理員找到該裝置，重新安裝驅動。
    3. 重新開機。


* Q2:無法和主機成功配對

  A:應該是配對資料錯亂了，或是目前頻道已有其他配對資料。
  * 解決方式1:
  
    * 找到keymap裡面有沒有按鍵被設為 &bt BT_CLR
    * 按這個鍵可以清除目前鍵盤頻道的配對資料，然後就可以重新配對。
    
  * 解決方式2:
    * Action編譯好的firmware.zip內，settings_reset-nice_nano_v2-zmk.uf2燒錄檔。
    
      進入bootloader模式，把這個檔案燒進去，重置配對資訊。
      
      
    * 然後再重燒一次左右手的daochoc燒錄檔。
    
    
    * 兩邊燒完後同時按Reset鍵，左右手鍵盤連接後，再與電腦配對應該就可以成功配對。

* Q3:左右邊沒有辦法成功配對

  A:應該是配對資料錯亂了，或是目前頻道已有其他配對資料。

  * 解決方式:
    * Action編譯好的firmware.zip內，settings_reset-nice_nano_v2-zmk.uf2燒錄檔。
    
      進入bootloader模式，把這個檔案燒進去，重置配對資訊。
      
      
    * 然後再重燒一次左右手的ergodash燒錄檔。
    
    
    * 兩邊燒完後同時按Reset鍵，應該就可以重新配對。  
  

