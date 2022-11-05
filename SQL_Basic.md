---
title: SQL
tags: DataBase
lang: zh-tw
---

[![hackmd-github-sync-badge](https://hackmd.io/DQme0ZPtQvONrz-11rBhxA/badge)](https://hackmd.io/DQme0ZPtQvONrz-11rBhxA)

{%hackmd theme-dark %}

# SQL 簡介
- 英文全名：Structured Query Language
- 中：結構化查詢語言
- 類別：關聯式資料庫(Relational database)

### 關聯式資料庫管理系統
#### 簡介
- 英文簡稱：RDBMS
- 英文全名：Relational DataBase Management System

# 關聯名詞比較表
| 關聯式資料模型    |     SQL Server或Access      |
| ----------------- |:---------------------------:|
| 關聯(Relation)    |         表格(Table)         |
| 值組(Tuple)       |         值組(Tuple)         |
| 屬性(Attribute)   |  直欄(Column)或欄位(Filed)  |
| 基數(Cardinality) | 記錄個數(number of Record)  |
| 主鍵(Primary Key) | 唯一識別(unique identifier) |
| 定義域(Domain)    | 合法值群(pool legal values) |

![](https://i.imgur.com/EamJPgi.png)

# 重要專有名詞
### 資料表 (Table)
- 是真正儲存資料的地方。
- 是由`資料行`與`資料列`的二維表格組合而成。

### 資料行 (Column)
- 指資料表中的某些`欄位`，以`垂直`方式來呈現。

### 資料列 (Row)
- 指資料表中某些`記錄`，以`水平`方式來呈現。

# 鍵值屬性
## 屬性(Attribute)
### 定義
- 用來描述實體的性質(Property)。

### 分類
#### 簡單屬性 (Simple Attribute)
- 已經`無法`再繼續切割成其他`有意義`的單位。
- Ex：學號

#### 複合屬性(Composite Attribute)
- 由`兩個`或`兩個以上`的其他屬性的值所組成。
- Ex：`地址`屬性是由區域號碼、縣市、鄉鎮、路、巷、弄、號等各個屬性所組成。
- 適用時機：戶政事務查詢，房屋仲介網站…
- 一般使用者在設定客戶資料表或學生資料表時，`地址`屬性是視為`簡單屬性`

#### 衍生屬性(Derived Attribute)
- 指可以經由某種方式的`計算`或`推論`而獲得的。
- Ex：年齡 (目前的系統時間 - 生日)、性別 (使用身分證字號推論得出)

## 超鍵(Super Key)
### 定義
- 選出兩個或兩個以上的欄位組合起來，以作為唯一識別資料的欄位。
- 在一個關聯 (表格) 中至少有一個`超鍵`，就是所有屬性的集合。

## 主鍵 (Primary Key)
### 定義
- 縮寫：P.K.
- 主鍵中的每一筆資料都是表格中的唯一值。
- 用來確認一個表格中的每一行資料。
- 可以是原本資料內的一個欄位，或是一個人造欄位 (與原本資料沒有關係的欄位)。
- 在一個關聯中，只有`一個主鍵`，若候選鍵未被選為主鍵時，則稱為`交替鍵(Alternate Key)`。
- 主鍵之鍵值不可為虛值 (Null Value) 。

### Ex
![](https://i.imgur.com/Ik1qDlq.png)

## 複合鍵(Composite Key)
### 定義
- 指資料表中的主鍵，是由兩個或兩個欄位以上所組成。

### 使用時機
- 當表格中某一欄位的值無法區分資料記錄時。

### Ex
![](https://i.imgur.com/DARpTRL.png)

## 候選鍵(Candidate Key)
### 定義
- 就是主鍵的候選人，並且也是關聯表的屬性子集所組成。
- 不含有多餘屬性的超鍵稱為候選鍵。
- 一個資料表中可以含有多個。
- 常被稱為最小的超鍵。

### 條件
- 必須同時要符合下列兩項條件：
    1. 具有唯一性
    2. 具有最小性
        - 最小性定義：在該`屬性子集`中移除任一個屬性之後，不再符合唯一性。

### Ex
![](https://i.imgur.com/Gurflrh.png)

## 外來鍵(Foreign Key)
### 定義
- 縮寫：F.K.
- 是一個 (或數個) 指向另外一個表格主鍵的欄位。
- 目的是確定資料的參考完整性 (Referential Integrity)。
- `主鍵`值的所在資料表稱為`父關聯`
- `外來鍵`值的所在資料表稱為`子關聯`
- 外來鍵和`父關聯`的主鍵欄位必須要具有相同的`資料型態`和`欄位長度`，但名稱則可以不相同。
- 欄位值可以是`重覆值`或`空值 (NULL)` 。

# 關聯的種類
## 一對一的關聯 (1：1)
- 甲資料表中的一筆記錄，只能對應到乙資料表中的一筆記錄。
- 並且乙資料表中的一筆記錄，只能對應到甲資料表中的一筆記錄。

## 一對多的關聯(1：M)
- 甲資料表中的一筆記錄，可以對應到乙資料表中的多筆記錄。
- 但乙資料表中的一筆記錄，卻只能對應到甲資料表中的一筆記錄。

## 多對多的關聯(M：N)
- 甲資料表中的一筆記錄，能夠對應到乙資料表中的多筆記錄。
- 且乙資料表中的一筆記錄，也能夠對應到甲資料表中的多筆記錄。

# 資料庫之完整性規則
## 簡介
- `完整性規則 (Integrity Rules)`是用來確保資料的`一致性`與`完整性`，以避免資料在經過`新增`、`修改`及`刪除`等運算之後，而產生的異常現象。

## 完整性規則
- 實體完整性規則(Entity Integrity Rule)
- 參考完整性規則(Referential Integrity Rule)
- 值域完整性規則(Domain Integrity Rule)

![](https://i.imgur.com/viEiEcK.png)

# 實體關係模式 (Entity-Relation Model)
## 概念
### 定義
- 用來描述`實體`與`實體`之間關係的工具。

## ER 圖的符號表
![](https://i.imgur.com/XwD6J4G.png)

### Ex
![](https://i.imgur.com/rKgw9Uf.png)

## 實體 (Entity)
### 定義
- 用來描述實際存在的事物(如：學生)。
- 也可以是邏輯抽象的概念(如：課程)。
- 必須可以被識別，亦即能夠清楚分辨出兩個不同的實體。
- 實體都是以「名詞」的型式來命名，不可以是「形容詞」或「動詞」。
- 分類：
    - 強實體 (strong entity)
    - 弱實體 (weak entity)
### 強實體 (strong entity)
- 指不需要依附其他實體而存在的實體。
- 也就是真實世界中`獨立存在`的一切事物。
- 可以是實際存在的物品，也可以是概念性的事物。
- Ex：學生、課程。
- 表示圖形：長方形
    
![](https://i.imgur.com/QcbLj2s.png)


### 弱實體 (weak entity)
- 是指需要依賴其他實體而存在的實體。
- Ex：教職員的眷屬、課程的上課教室。
- 表示圖形：雙同心長方形

![](https://i.imgur.com/eddJgKs.png)

## 屬性 (Attribute)
### 定義
- 用來描述實體的性質(Property)。
- 分類：
    - 簡單屬性 (simple attribute)
    - 複合屬性 (composite attribute)
    - 鍵屬性 (Key attribute)
    - 單值屬性(single-valued attribute)
    - 多值屬性(Multi-valued attribute)
    - 衍生屬性(Derived attribute)

### 簡單屬性(simple attribute)
- 指已經不能再細分為更小單位的屬性。
- Ex：`學號`屬性便是`簡單屬性`。
- 表示圖形：橢圓形

![](https://i.imgur.com/VVoT4Ra.png)

### 複合屬性(composite attribute)
- 屬性是由`兩個`或`兩個以上`的其他屬性的值所組成，並且代表未來該屬性可以進一步作切割。
- Ex：`地址`屬性是由區域號碼、縣市、鄉鎮、路、巷、弄、號等各個屬性所組成。
- 表示圖形：

![](https://i.imgur.com/UaRCs2O.png)

### 鍵屬性(Key attribute)
- 指該屬性的值在某個環境下具有唯一性。
- Ex：學號屬性稱為`鍵(Key)`。
- 表示圖形：`橢圓形`內的屬性名稱加底線方式。
![](https://i.imgur.com/5e2RDUN.png)

### 單值屬性(single-valued attribute)
- 是指屬性中只會存在一個單一值。
- Ex：學號
- 表示圖形：橢圓形

![](https://i.imgur.com/VVoT4Ra.png)

### 多值屬性(Multi-valued attribute)
- 指屬性中會存在多個數值。
- Ex：學生的`電話`
- 表示圖形：雙邊線的橢圓形

![](https://i.imgur.com/cjKCwUr.png)

### 衍生屬性(Derived attribute)
- 指可由其他`屬性`或`欄位`計算而得的屬性。
- Ex：年齡
- 表示圖形：虛線橢圓形

![](https://i.imgur.com/Uxh39Gv.png)

## 關係 (Relationship)
### 定義
- 是指用來表達兩個實體之間所隱含的關聯性。

### 命名規則
- 使用足以說明關聯性質的`動詞`或`動詞片語`命名。

### Ex
- `學生`與`系所`兩個實體型態間存在著一種關係─`就讀於`。

### 表示圖形
- 菱形

![](https://i.imgur.com/cBnKmmA.png)

### 關係的基數性 (cardinality)
- 代表實體所能參與關係的案例數。
- 表示方式可分為三大類：
    1. 比率關係
    2. 雞爪圖基數性
    3. 基數限制條件

#### 利用「比率關係」來表示
- 一對一的關係(1：1)
    - 說明：一個A實體會對應到一個B實體。
    ![](https://i.imgur.com/3M3Ebce.png)
    - 對應關係圖：
    ![](https://i.imgur.com/YWICJCV.png)
    
- 一對多的關係(1：M)
    - 說明：一個A實體會對應到多個B實體。
    ![](https://i.imgur.com/ApUa5jN.png)
    - 對應關係圖：
    ![](https://i.imgur.com/sxLfO6E.png)

- 多對一的關係(M：1)
    - 說明：一個B實體會對應到多個A實體。
    ![](https://i.imgur.com/VWYzj2T.png)
    - 對應關係圖：
    ![](https://i.imgur.com/hMML4yM.png)

- 多對多的關係(M：N)
    - 說明：多個A實體會對應到多個B實體。
    ![](https://i.imgur.com/9aSemS5.png)
    - 對應關係圖
    ![](https://i.imgur.com/oWVXe52.png)

#### 利用「雞爪圖基數性」來表示
- 強制單基數
    - 說明：指一個實體參與其關係的案例數`最少一個`，`最多也一個`。
    ![](https://i.imgur.com/duQKwIn.png)
    
- 強制多基數
    - 說明：指一個實體參與其關係的案例數`最少一個`，`最多有多個`。
    ![](https://i.imgur.com/VHiRvNr.png)

- 選擇單基數
    - 說明：指一個實體參與其關係的案例數`最少0個`，`最多有一個`。
    ![](https://i.imgur.com/aJ1Jiso.png)

- 選擇多基數
    - 說明：指一個實體參與其關係的案例數`最少0個`，`最多有多個`。
    ![](https://i.imgur.com/vurCMwr.png)

#### 利用「基數限制條件」來表示
- (1,1)
    - 說明：指一個實體參與其關係的案例數`最少一個`，`最多也一個`。
    ![](https://i.imgur.com/FBfoINT.png)

- (1,N)
    - 說明：指一個實體參與其關係的案例數`最少一個`，`最多有多個`。
    ![](https://i.imgur.com/RXXk97w.png)

- (0,1)
    - 說明：指一個實體參與其關係的案例數`最少0個`，`最多有一個`。
    ![](https://i.imgur.com/mLcy2vh.png)

- (0,N)
    - 說明：指一個實體參與其關係的案例數`最少0個`，`最多有多個`。
    ![](https://i.imgur.com/6NgH5Cm.png)

### 關係的分支度(Degree)
- 指參與關係的實體的個數，稱之為`分支度 (Degree)`。
- 分為三種：
    1. 一元關係
    2. 二元關係
    3. 三元關係

#### 一元關係
- 指參與關係的實體的個數只有一個。
- 示意圖：
![](https://i.imgur.com/Q2oR1CR.png)

#### 二元關係
- 指參與關係的實體的個數有二個。
- 示意圖：
![](https://i.imgur.com/DNK2p8g.png)

#### 三元關係
- 指參與關係的實體的個數有三個。
- 示意圖：
![](https://i.imgur.com/1y7g7Qa.png)

### 關係的屬性
- 適用時機：指兩個實體真正交易的時間點時，才會產生的屬性。
![](https://i.imgur.com/LQDftzu.png)

### 關係的參與限制
- 指「實體的實例」是全部或部分參與關係。
- 可分為兩種：
    1. 全部參與限制條件（Total Participation Constraints）
    2. 部分參與限制條件（Partial Participation Constraints）

#### 全部參與限制條件
- 是指實體全部集合中的實例都參與關聯性。
- 標示方法：雙線
![](https://i.imgur.com/3L5U1uB.png)

#### 部分參與限制條件
- 指在實體全部集合中只有部分實例參與關聯性。
- 標示方法：單線
![](https://i.imgur.com/Naivtsc.png)

### 綱要（Schema）
- 是資料庫中全體資料的邏輯結構和特徵的描述。
- 它僅僅涉及到型態的描述，不涉及到具體的值。
- Ex：學生資料表(學號,姓名,系別)

### 實例（Instance）
- 綱要的一個具體值稱為綱要的一個實例。

## 建立資料表間的關聯
- 資料表之間的關聯性有三種情況：
    1. 1對1(1:1)關係
    2. 1對多(1:M)關係
    3. 多對多(M:N)關係

### 1對1(1:1)關係
- ER 圖：
![](https://i.imgur.com/aqbGEk7.png)

- 作法：
    1. 將 Entity2 資料表的主鍵 B 嵌入到 Entity1 資料表中，當作 Entity1 資料表的外來鍵 (F.K.)。
    ![](https://i.imgur.com/DMcSJMN.png)
    2. 將 Entity1 資料表的主鍵 A 嵌入到 Entity2 資料表中，當作 Entity2 資料表的外來鍵 (F.K.)。
    ![](https://i.imgur.com/Sk7a4yC.png)

### 1對多(1:M)關係
- ER 圖：
![](https://i.imgur.com/xwcvPSL.png)

- 作法：將 Entity1 資料表 (少的那方) 的主鍵 A 嵌入到 Entity2 資料表 (多的那方) 中，當作 Entity2 資料表的外來鍵 (F.K.)。
![](https://i.imgur.com/AK2qyLw.png)


### 多對多(M:N)關係
- ER 圖：
![](https://i.imgur.com/0hJ59P7.png)

- 作法：增加一個R資料表，而R資料表的主鍵欄位是由Entity1資料表的主鍵A與Entity2資料表的主鍵B所組成。
![](https://i.imgur.com/d4uYzDr.png)

# 正規化
- 英文全名：Normalization

## 概念
- 是結構化分析與設計中，建構`資料模式`所運用的一個技術。
- 目的是為了降低資料的`重覆性`與避免`更新異常`的情況發生。

## 定義
- 指將原先關聯(表格)的所有資訊，在`分解`之後，仍能由數個新關聯(表格)中經過`合併`得到相同的資訊。
    - 無損失分解：
        - 當關聯表 R 被`分解`成數個關聯表 R1，R2，…， Rn 時，則可以再透過`合併` R1，R2，…，Rn 得到相同的資訊 R。
    ![](https://i.imgur.com/W9LPd04.png)

## 目的
- 降低資料重複性(Data Redundancy)。
- 避免資料更新異常(Anomalies)。

### 避免資料更新異常(Anomalies)
#### 實例：
![](https://i.imgur.com/PS5YYhn.png)

#### 新增異常(Insert Anomalies)
- 新增某些資料時必須同時新增其他的資料，否則會產生新增異常現象。
![](https://i.imgur.com/xxE7d3U.png)

#### 修改異常(Update Anomalies)
- 修改某些資料時必須一併修改其他的資料，否則會產生修改異常現象。
![](https://i.imgur.com/N9qKYng.png)

#### 刪除異常(Delete Anomalies)
- 刪除某些資料時必須同時刪除其他的資料，否則會產生刪除異常現象。
![](https://i.imgur.com/jRi3ycD.png)

#### 解決方法
![](https://i.imgur.com/mmIKYbK.png)

## 功能相依 (Functional Dependence)
- 簡稱：FD

### 定義
- 指資料表中各欄位之間的相依性。
- 亦即某欄位不能單獨存在，必須要和其他欄位一起存在時才有意義。

### Ex
- 學生資料表
    ![](https://i.imgur.com/U67EdWF.png)
    - 說明：`姓名`欄位的值必須搭配`學號`欄位才有意義, 則我們說`姓名欄位相依於學號欄位`。

### 表示方式
- 假設有一個資料表 R，並且有三個欄位，分別為 X,Y,Z，因此，我們就可以利用一條數學式來表示：`R = {X,Y,Z}`。
- 假設在 `R={X,Y,Z}` 數學式中，X 和 Y 之間存在`功能相依`時，並且存在 Y 功能相依於 X，則我們可以利用以下的表示式：
    1. Y ∝ X   (Y 功能相依於 X)
    2. X ➜ Y  (X 決定 Y)
    
    > [color=#d19a25] ps.
    > 若 `X ➜ Y` 時：
    > 在FD的左邊X稱為決定因素(Determinant)
    > 在FD的右邊Y稱為相依因素(Dependent)
- 示意圖：
    ![](https://i.imgur.com/Dt4MQ84.png)

### 完全功能相依 (Full Functional Dependency)
- 假設在關聯表 R( X, Y, Z ) 中，包含一組`功能相依 ( X, Y ) ➜ Z`，如果我們從關聯表 R 中`移除`任一屬性 X 或 Y 時，則使得這個功能相依 ( X, Y ) ➜ Z `不存在`，此時我們稱 Z 為`完全功能相依`於 ( X, Y )。

### 部份功能相依 (Partial Functional Dependency)
- 假設在關聯表 R( X, Y, Z ) 中，包含一組`功能相依 ( X, Y ) ➜ Z`，如果我們從關聯表 R 中`移除`任一屬性 X 或 Y 時，則使得這個功能相依 ( X, Y ) ➜ Z `存在`，此時我們稱 Z 為`部分功能相依`於 ( X, Y )。

### 遞移相依 (Transitive Dependency)
- 指在二個欄位間並非直接相依，而是借助第三個欄位來達成資料相依的關係。
- Ex：
    - Y 相依於 X ( X ➜ Y)；而 Z 又相依於 Y ( Y ➜ Z)，如此 X 與 Z 之間就是遞移相依的關係。
    ![](https://i.imgur.com/qDLYwRM.png)

## 規則
- 第一 ~ 第五正規化：
    1. 1NF
    2. 2NF
    3. 3NF
    4. 4NF
    5. 5NF
- 正規化最多可以進行到第五正規化形式
- BCNF 被視為大部分應用程式所需的最高階正規形式。

![](https://i.imgur.com/oydVBOX.png)

## 步驟
![](https://i.imgur.com/GQFuLXZ.png)

### 第一正規化 (First Normal Form)
- 簡稱：1NF。

#### 規則
- 每一個欄位只能有一個`基元值 (Atomic)`即單一值。
    - Ex：課程名稱欄位中不能存入兩科或兩科以上的課程名稱。
- 沒有任何`兩筆以上`的資料是完全重覆。
- 資料表中有主鍵，而其他所有的欄位都相依於`主鍵`。
    - Ex：姓名與性別欄位都相依於「學號」欄位。

#### 作法
- 將重複的資料項分別儲存到`不同`的記錄中, 並加上適當的主鍵。

### 第二正規化 (Second Normal Form)
- 簡稱：2NF。

#### 規則
- 符合 1NF。
- 每一非鍵屬性 (如：姓名、性別…) 必須`完全相依`於主鍵 (學號)；即不可`部分功能相依`於主鍵。

#### 作法
- 分割資料表；亦即將`部分功能相依`的欄位`分割`出去，再另外組成`新的資料表`。

### 第三正規化 (Third Normal Form)
- 簡稱：3NF。

#### 規則
- 符合 2NF。
- 各欄位與`主鍵`之間沒有`遞移相依`的關係。

#### 作法
- 分割資料表；亦即將`遞移相依`或`間接相依`的欄位`分割`出去，再另外組成`新的資料表`。

### Boyce-Codd 正規化型式 (Boyce-Codd Normal Form)
- 簡稱：BCNF。
- 其條件比 3NF 更加嚴苛。因此每一個符合 BCNF 的關聯一定也是 3NF。

#### 適用時機
- 如果資料表的`主鍵`是由`多個欄位`組成的, 則必須再執行 BCNF。

#### 規則
- 如果資料表的`主鍵`只由`單一欄位`組合而成，則符合 3NF 的資料表，亦符合 BCNF。
- 如果資料表的`主鍵`由`多個欄位`組成 (又稱為複合主鍵)，則資料表就必須要符合以下條件：
    1. 符合 3NF 的格式。
    2. `主鍵`中的各欄位不可以相依於其他非主鍵的欄位。

### 第四正規化 (Fourth Normal Form)
- 簡稱：4NF。
- 符合 BCNF，再除去所有的`多值相依`。

### 第五正規化 (Fifth Normal Form)
- 簡稱：5NF。
- 符合 4NF，且沒有`合併相依`。

# MySQL