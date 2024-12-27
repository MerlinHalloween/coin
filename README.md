# coin
# FPGA-Dodge 閃避遊戲

## 作者: 112321041

---

## 簡介
此專案是一個基於 FPGA 的閃避遊戲，透過 8x8 LED 矩陣、七段顯示器以及開關進行操作。遊戲特色包含玩家控制角色、掉落障礙物及金幣收集。此版本包含多項改進，例如蜂鳴器、新增暫停、重新開始、難度調整及增強的視覺聽覺互動特效效果。

### 遊戲展示
[點擊觀看遊戲示範影片](https://youtu.be/b9Tf317bIJk)

![我的遊戲不錯吧？！](https://raw.githubusercontent.com/MerlinHalloween/coin/refs/heads/main/image.png)

---

## 輸入/輸出元件
1. **8x8 LED 矩陣:** 顯示角色、掉落物、金幣及遊戲狀態（例如通關或遊戲結束）。
2. **七段顯示器:** 顯示累計金幣數量。
3. **4 位元開關:** 控制角色移動、重新開始及暫停功能。
4. **8 顆 LED 燈:** 表示倒數計時。
5. **蜂鳴器:** 提供遊戲事件的音效反饋。

---

## 基本功能
1. **角色移動:** 紅色 LED 代表角色，透過開關控制左右移動。
2. **掉落物:** 綠色 LED 代表障礙物，玩家需要閃避。
3. **金幣收集:** 藍色 LED 代表金幣，玩家可以收集，總數顯示在七段顯示器上。
4. **倒數計時:** 使用 8 顆 LED 表示遊戲時間。
5. **遊戲結束:** 當角色碰到障礙物時，遊戲結束，8x8 LED 矩陣顯示 "X" 並發出長音。
6. **通關條件:** 成功閃避所有障礙物時，8x8 LED 矩陣顯示 "V"。

---

## 新增功能
1. **暫停:** 可透過指定開關暫停遊戲。
2. **重新開始:** 可隨時透過指定開關重新開始遊戲。
3. **蜂鳴器:** 新增遊戲事件的音效反饋（例如遊戲結束）。
4. **難度調整:** 玩家可選擇不同難度（0.5x、1x、2x、4x 及 16x 的速度）。
5. **增強的遊戲結束狀態:** 遊戲結束時，8x8 LED 矩陣依序顯示 "LO" 和 "SE"。
6. **優化倒數系統:** 倒數計時現採用 8 位元 LED 系統，一個循環代表完整遊戲時間。
7. **顏色自訂:** 可透過調整 `drop_19` 參數更改遊戲結束時 "X" 的顏色。

---

## 實作細節
### 輸出
- **R, G, B:** 連接至 8x8 LED 矩陣，用於控制顏色。
- **Second:** 連接至 8 顆 LED 燈，作為倒數計時器。
- **COMM:** 控制 LED 矩陣的列及啟用訊號。
- **SevenSeg:** 驅動七段顯示器。

### 輸入
- **CLK:** FPGA 時鐘輸入（50 MHz）。
- **Left, Right:** 透過 4 位元開關控制角色移動。

---

## PIN 分配
### 圖示
![PIN 分配](https://raw.githubusercontent.com/MerlinHalloween/coin/refs/heads/main/16528.jpg)

---

## 矩陣編碼
矩陣編碼依據規則：`73516240`。參考以下筆記圖片進行參數設定：
![矩陣編碼筆記](https://raw.githubusercontent.com/MerlinHalloween/coin/refs/heads/main/16995.jpg)

---

## 倒數系統說明
原本的倒數系統使用 16 位元 LED，但因硬體限制，現改為使用 8 位元 LED：
- 8 位元 LED 倒數時，逐漸熄滅所有燈光。
- 當倒數結束，切換到下一階段，LED 重新亮起。
- 一個循環代表完整的遊戲時間。

![倒數系統](https://raw.githubusercontent.com/MerlinHalloween/coin/refs/heads/main/16998.jpg)

---

## 自訂功能
- 若需更改遊戲結束時 "X" 的顏色，可調整 `drop_19` 參數，將其指定為 `B`，並設置 `R` 和 `G` 為 `8'b11111111`。
- 難度調整可透過修改程式中的速度參數進行設置。

---

## 未來展望
1. 隨機生成掉落物與金幣。
2. 掉落物與金幣的速度不同步。
3. 延長遊戲時間。

---

## 參考
[原始專案 Joe0411](https://github.com/joe0411/final-1)




[https://youtu.be/atA9PljkhF8](https://youtu.be/b9Tf317bIJk)

this video shows the gaming demonstration
the four bit button got (left)(right)(restart)(pause),four different state

when pass,show V on 8x8 matrix led;
else if, show X on matrix,and the beeper will generate a long beep sound

you can restart the game by pressing restart

new function added:
beeper
pause
restart
different dificulty choice for 0.5X,1X,2X,4X(even 16X:in the code//)



PS: i add extra lose state expression which is 
LO
SE
in the drop_19 parameter
the matrix coding should base on the rule:73516240
when you write on the parameter,refer to my note pic:16995


Base on the origin project, the count down system is base on 16 bit led,but i got only 8 pin to assign .
Due to that case,i change the count down system as the 8 bit led light will -1 to snub out all 8 bit,then the phase will change to 1,and the 8 bit led will +1 light up again .Hence,one loop represent the gaming time.

if you wanna change the X color,change drop_19, assign it to B,and let R G<=8'b11111111.

more explanation about the basic function of normal coin game should have,refer to the link below.





reference:
https://github.com/joe0411/final-1



PIN number assign
![Alt Text](https://raw.githubusercontent.com/MerlinHalloween/coin/refs/heads/main/16528.jpg)

