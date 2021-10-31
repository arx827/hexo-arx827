---
title: '[筆記]_CSS重構'
date: 2021-09-18 23:53:56
tags: [筆記, CSS]
---

- <small>[本書相關範例](http://www.cssrefactoringbook.com/)</small>

## 第一章 - *重構與架構*
  - ### 重構 (Refactoring)
    是為了讓程式更簡單且更容易複用，在不改變其行為的情況下重寫程式的過程。
  - ### 軟體架構 (software architecture)
    描述軟體專案中這些零件如何組織在一起的用語，最好的架構通常會在進行編程之前就被規劃妥當。
    1. #### 好架構可預期
      可預期，意指可以對軟體的運作方式與其組成作為精確的假設。
    2. #### 好架構有助於樣式碼複用
      樣式碼複用，指樣式碼不需複製就可以在許多地方使用的性質。
    3. #### 好架構易擴充
      擴充性，具有這種特質的系統，可以很容易地在其上加進新的功能。
    4. #### 好架構易維護
      維護性，維護性高，調整起現有功能來就比較容易。
  
  #### 為什麼重構？
    重構能改善軟體架構，一種可將程式碼重新組織成結構性更好的技術，
    目的是讓程式更容易預期、複用、擴充與維護。

<!-- more -->
  - ### 進行重構的原因
    1. #### 需求改變
      軟體系統會因為需求改變而演變。
    2. #### 設計不良的架構
      現實環境的限制下，通常無法有足夠的時間作完整的規劃。
    3. #### 低估難度
      在專案時程被低估時，開發者寫碼時就不會深思熟慮。
    4. #### 忽視最佳實務
      需要再重新檢視樣式碼並進行某種程度的重構。

  - ### 何時該重構樣式碼？
    通常在修正錯誤或使用現有樣式碼建置新功能時，就是重構的最佳時機。
    固定進行的重構會讓程式品質不斷提升。
  - ### 何時「不該」重構樣式碼？
    應該只在能改善架構或為了符合一慣的編程準則時，才進行重構。
  - ### 重構範例
  > <small>單元測試，是一段執行另一段程式的碼，用來檢查該程式是否如預期地運作。
  > 為了將可能浮現之任何問題的根本肇因範圍縮小，
  > 單元測試應該只用來檢測單一功能的樣式碼。</small>
    - #### JS重構後，通常會出現下列現象：
      - 函式數量比之前更多。
      - 單元測試比之前更多。
      - 每個函式都只做一件特定的工作。
      - 每個函式都有一個相對應的單元測試。
      - 函式可互相搭配以進行更複雜的計算。
    - #### CSS重構後，會出現下列現象：
      - 抽離行內CSS有助於提高複用性 (reusability)。
      - 功能區隔 (樣式與結構)，讓樣式碼的可讀性提高。
      - 回歸測試 (regression testing) 可透過網頁瀏覽器手動的方式，或透過比較截圖與重構後介面的方式來進行。

-----------

## 第二章 - *暸解串接*
  - ### 串接 (cascade)
    是瀏覽器用來決定樣式如何套用到元素上的方法。
  - ### 選取器特定度 (specificity)
    是所使用的CSS選取器能多精準地將元素識別出來的一種估測。
    (a, b, c, d, e)
    - a: !important
    - b: inline style
    - c: ID選取器
    - d: class選取器、屬性選取器、偽類
    - e: 類型選取器、偽元素
  - ### 規則集順序
    CSS規則集在樣式表中的位置。
    較晚出現的宣告區塊具有較高的優先權。

-----------

## 第三章 - *編寫較佳的CSS*
  - ### 善用註解
    應該加上註解部份包括：

    1. 檔案內容。
    2. 選取器的相依性與用法等。
    3. 為何要如此宣告 (處理瀏覽器特有渲染方式時特別有用)。
    4. 重構過但已停用的樣式 (deprecated styles) 與不該再使用的樣式。

    CSS只有區塊型註釋 (多行註釋)，以 `/*` 開頭，以 `*/` 結尾。
      ```css
      /*
      * 主要導覽連結的樣式
      */
      ```
  - ### 一致的結構規則集
    以一致的方式來編寫規則集可讓CSS更容易預期，也更容易被理解。
    1.寫成一行的CSS規則集
    ```css
      selector {property1: value; property2: value; property3: value}
    ```
    2.寫成多行的CSS規則及
    ```css
      selector {
        property1: value;
        property2: value;
        property3: value;
      }
    ```
    3.大括號另成一行的CSS規則集
    ```css
      selector
      {
        property1: value;
        property2: value;
        property3: value;
      }
    ```
    - #### 以供應商前綴整理性質
      供應商前綴 (vendor prefix) 是瀏覽器開發商在新的實驗性CSS屬性尚未標準化前，在屬性名稱前加上的標示用字串。
      - 使用 Blink 或 Webkit 渲染引擎的瀏覽器，(如 Chrome 與 Safari) 會使用 `-webkit-` 前綴。
      - 使用 Gecko 渲染引擎的瀏覽器，(如 Firefox) 會使用 `-moz` 前綴。
      - 使用 Trident 渲染引擎的瀏覽器，(如 Internet Explorer / Edge)，會使用 `-ms` 前綴。

      ```css
      .border-radius{
        -ms-border-radius: 5px;
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
        border-radius: 5px;
      }
      ```

      當該屬性標準化後，就不會再加上前綴。
      這些屬性的排列順序很重要，瀏覽器會以宣告區塊中由上而下的順序來套用這些屬性，
      沒有辦法辨識的，它就會略過。
      因為要讓特定瀏覽器的使用者升級其瀏覽器需要一些時間，
      有前綴與沒有前綴屬性應該都要保留，直到你的網站不支援該瀏覽器為止。
  - ### 維持選取器的單純
    有時使用限定選取器是比較洽當的。
    - #### 高效選取器
      簡單選取器的效能會比複雜選取器的效能要好。
      - ##### 由右向左比對選取器
        瀏覽器會從右自左比對選取器，所以它能排除前頭不符合的元素，不會浪費時間在檢查可能符合的元素。
      - ##### 關鍵選取器
        選取器最右邊的部份稱為關鍵選取器。
        只用全域選取器 (`*`) 不與組合器與其他選取器併用 (`body *`)。
  - ### 切斷CSS與JavaScript的耦合
      JavaScript中用來選取元素的類別與ID不應該用來為元素指定樣式，
      當元素的樣式需要透過JavaScript來調整時，應該透過增刪類別的方式來做。
      - #### 為JavaScript中的類別與ID名稱之前加上前綴
        於要用在JavaScript中的類別與ID名稱之前加上`js-`。
      - #### 以類別修改元素樣式
        與其透過JavaScript將樣式加到元素style屬性的方式來調整HTML元素的樣式，應該透過增刪元素類別的方式來進行調整。
  - ### 使用類別
    元素使用唯一ID所能獲得的好處其實可以用唯一的類別名稱來替代，可以有相同的效果。
      > <small>ID是JavaScript中選取元素最快的方法，
      > 與在類別名稱前加上 `js-` 一樣，
      > 不用它指定元素的樣式是另一種將CSS與JavaScript分離的好方法。</small>
  - ### 為類別取有意義的名稱
    能清楚表達意義很重要，但也要注意千萬別做過頭了。
    ex: `.female-black-and-white-kitten `
    - #### 避免類別過度模組化
      有意義的類別名稱所表示的是要套用樣式的元素，而不是要被套用到元素上的樣式。 
      ```html
      <h1 class="font-bold uppercase blue-text margin-bottom-large no-padding">
        Too Many CSS Classes
      </h1>
      ```
      應該避免使用過度模組化的類別，因為它們比行內樣式好不到哪兒去。
    - #### 建造較佳的盒框
      盒框模型 (box model) 是瀏覽器決定如何渲染 (render) 一個方型區域的方法，HTML的所有元素基本上都可視為是一個盒框。
      - ##### box-sizing: `content-box`
        盒框元素 height 與 width，不包含 padding 與 border
      - ##### box-sizing: `border-box`
        盒框元素 height 與 width，包含 padding 與 border
      為了一致性，通常只會選一種來使用，可以透過全域選取器來為它設定一個適當的值。

## 第四章 - *為不同類型的樣式分類*
  為不同樣式作分類才能善用串接的特性
  - ### 樣式分類的重要性
    具語意的 HTML標籤 來描述要呈現的內容。
    有助於創建出更好的架構，因為將樣式組織成不同的分類能讓樣式碼更容易複用。
  - ### 樣式正規化
    不同的瀏覽器，樣式表集的屬性與值可能略有不同。
    樣式正規化 (normalizing styles) 用來提供不同元素的屬性預設值。
    為不同瀏覽器族系所製作的開源正規化樣式 ex: ` normalize.css `
  - ### 基底樣式
    基底樣式 (base styles) 用來作為其他特定度更高之樣式的建構基點。
    編寫基底樣式時要注意的原則是，後來添加的樣式應該不需要覆寫太多基底樣式就可以做得出來。
    - #### 定義基底樣式
      設計樣式時，應考慮元素最常見的使用方式，適合於最常見之使用情境的值。
      經常用到的屬性包括：
        - `color`
        - `font-family`
        - `font-size`
        - `font-weight`
        - `letter-spacing`
        - `line-height`
        - `margin`
        - `padding`
    - #### 文件詮釋資料
      文件詮釋資料 (metadata) 標籤包括`<head>`、`<title>`、`<base>`、`<link>`與`<meta>`等。
      因為使用者看不到它們，所以無法指定這些標籤的樣式。
    - #### 分段元素
      分段元素 (sectioning elements)包括`<address>`、`<article>`、`<aside>`、`<body>`、`<footer>`、`<header>`、`<nav>`與`<section>`等。
      通常會包含其他元素，構成HTML文件中不同的段落。
    - #### 標頭與文本元素
      標頭元素 (heading elements) 包括 `<h1>` ~ `<h6>` 元素，
      是用來在HTML文件中定義每一不同段落主題的元素。
      文本元素 (text elements) 包括 `figure`、`<figcaption>`、`<p>`與`<pre>`元素，用來顯示文本區塊。
    - #### 錨點標籤
      錨點標籤 (anchor tags) 提供可連到其他HTML文件或同一份HTML文件中段落的連結，
      能搭配常用來顯示狀態的 `:link`、`:visited`、`:focus`、`:hover`與`:active` 虛擬類別。
      - `:link`
        套用在具有href屬性的元素上。
      - `:visited`
        套用在具有href屬性的連結上，且該連結的位置已列在瀏覽器的瀏覽歷史紀錄中。
      - `:focus`
        當元素被點選、觸碰或透過跳位鍵(Tab key)選到該元素時，此樣式會被套用。
      - `:hover`
        套用在滑鼠指標下的連結。在觸控裝置上，因為不具有hover狀態，通常會被套用在被觸碰的元素上。
      - `:active`
        套用在連結『被啟用(activated)』的元素上。
        在滑鼠的情況下，點選連結但滑鼠鍵還未放開時就是處於這種狀態。
        在觸控裝置上，點選元素但手指尚未移開螢幕時，元素會處於這種狀態。
    - #### 文本語意
      文本語意 (text semantics)，用來賦予文本更多意義或結構的元素。通常是行內型，包括：
      `<abbr>`、`<b>`、`<cite>`、`<code>`、`<data>`、`<dfn>`、`<em>`、`<i>`、`<kbd>`、`<s>`、`<strong>`、`<sub>`、`<sup>`、`<time>`與`<u>`等標籤。
    - #### 列表
      包括
        - `<ol>` (有序列表，ordered list)
        - `<ul>` (無序列表，unordered list)
        - `<dl>` (定義列表，definition list)
      
      有序與無序列表只能內含`<li>`(列表項目，list item)元素，
      定義列表只能包含`<dt>`(定義項，definition term)與`<dd>`(定義說明，definition description)元素。

      `list-style-type`、`list-style-image`與`list-style-position`屬性，
      若列表元素比較少用，直接設定成 `none` 可能會比較好，避免需要不斷地去覆寫這些屬性。
      `<ol>` 或 `<ul>` 的 `padding-left` 屬性應該設為0。
      子`<li>`元素會繼承其父元素`<ol>`或`<ul>`的`font-family`、`font-size`與`line-height`屬性，但不會繼承`margin`、`padding`屬性。
    - #### 群組元素
      包括`<div>`、`<main>`與`<span>`。
      `<span>`標籤，主要用來群組文本或行內元素。
    - #### 表格
      包括 `<table>`、`<caption>`、`<colgroup>`、
      `<col>` (列，column)、
      `<tbody>` (表格主體，table body)、
      `<thead>` (表格標題，table header)、
      `<tfoot>` (表格頁尾，table footer)、
      `<tr>` (表格列，table row)、
      `<td>` (表格方格，table cell)、
      `<th>` (表格標題方格，table header cell)等元素。
    - #### 表單
      包括 `<form>`、`<label>`、`<input>`、`<button>`、`<select>`、`<datalist>`、`<optgroup>`、`<option>`、`<textarea>`、`<output>`、`<progress>`、`<meter>`、`<fieldset>`與`<legend>`等元素。
      某些表單元素的樣式可能不容易設定，因為瀏覽器會直接忽略其上所套用的屬性。
      ex: 瀏覽器會忽略套用在複選框(checkboxes)與選項鈕(radio button)上的`border-color`、`border-width`、`background-color`或其他屬性。
    - #### 影像
      圖片可透過`<img>`與`<picture>`標籤來呈現。
      因為`<img>`元素可在行內的格式情境中使用，`baseline`是`vertical-align`屬性的預設值。
      避免影像超出其容器的範圍，可將其`max-width`設定成等於其父容器的100%。
      `img`標籤基底樣式可設定成：
      ```css
      img {
        border: none;
        max-width: 100%;
        vertical-align: middle;
      }
      ```
    - #### 組件樣式
      可複用組件 (reusable components)，
      在製作可複用組件時，可先思考可複用組件的流程：
        1. 在製作組件前，先定義所需的行為。
        2. 保持組件樣式粒度並設定合理的預設值。
        3. 在其周圍置放具不同類別之容器元素的方式，視需要覆寫群組組件的視覺樣式。
        4. 讓結構容器為其指定大小。
      
      ex：
      - ##### 定義需要建置的行為
        - 組件應該可以只有2個或更多的頁籤。
        - 當頁籤被點選時，底框會變成藍色而背景則為白色。
        - 當頁籤未被點選時，背景色為灰色。

        ``` html
        <nav>
          <ul>
            <li><a href="#">Tab One</a></li>
            <li><a href="#">Tab Two</a></li>
            <li><a href="#">Tab Three</a></li>
          </ul>
        </nav>
        ```
      - ##### 保持組件樣式粒度
        每一種組件樣式應該只用來為一個元素指定樣式。

        ``` css
        /**
        * 分別為每個頁籤指定樣式會產生不少重複的碼
        */
        .tab-1,
        .tab-2,
        .tab-3 { ... }

        .tab-1:hover,
        .tab-2:hover,
        .tab-3:hover { ... }

        .tab-1:active,
        .tab-2:active,
        .tab-3:active { ... }

        .tab-1 > a,
        .tab-2 > a,
        .tab-3 > a { ... }

        .tab-group { ... }
        ```
        將樣式抽離到一個可重複使用的類別。
        ``` css
        /**
        * 頁籤組件樣式
        */
        .tab {
          background-color: #F2F2F2;
          border-bottom: 1px solid #EEEEEE;
          border-top: 1px solid #EEEEEE;
          bottom: -1px;
          display: inline-block;
          margin-left: 0;
          margin-right: 0;
          margin-top: 4px;
          position: relative;
        }
        .tab:first-child {
          border-left: 1px solid #EEEEEE;
          border-top-left-radius: 4px;
        }
        
        .tab:last-child {
          border-right: 1px solid #EEEEEE;
          border-top-right-radius: 4px;
        }
        .tab.active {
          background-color: #FFFFFF;
          border-bottom: 1px solid #2196F3;
          color: #000000;
        }
        .tab:hover {
          background-color: #F9F9F9;
        }
        .tab > a {
          color: inherit;
          display: block;
          height: 100%;
          padding: 12px;
          text-decoration: none;
          width: 100%
        }
        /**
        * 頁籤組件容器
        */
        .tab-group {
          border-bottom: 1px solid #EEEEEE;
          list-style: none;
          margin: 0;
          padding-left: 0;
        }
        ```
      - ##### 讓組件容器依需要覆寫視覺樣式
        將定義這些樣式的工作委派給父容器來處理。
        ``` css
        /**
        * 水平頁籤群組
        */
        .tab-group {
          border-bottom: 1px solid #EEEEEE;
        }
        .tab-group .tab {
          border-bottom: 1px solid #EEEEEE;
          border-top: 1px solid #EEEEEE;
          bottom: -1px;
          display: inline-block;
        }
        /**
        * 垂直頁籤群組
        */
        .tab-group-vertical {
          border-left: 1px solid #EEEEEE;
        }
        .tab-group-vertical .tab{
          border-left: 1px solid #EEEEEE;
          border-right: 1px solid #EEEEEE;
          left: -1px;
          display: block;
        }
        ```
      - ##### 將指定尺寸委派給結構容器
        指定尺寸的責任應該被委派給包含該組件或組件群組的結構。

    - #### 結構樣式
      結構樣式，包含組件及其容器。
    - #### 工具樣式
      工具樣式(utility styles)，在定義要套用到HTML元素上之類別時，套用到元素上的樣式，或是在滿足特定條件時，由JavaScript所指定之樣式。
      ```css
        .hidden {
          display:none !important;
        }
      ```
    - #### 瀏覽器特定樣式
      透過瀏覽器-特定的CSS改裝來對付有怪癖的舊版瀏覽器。
      可以將這些改裝另外放在專屬的樣式表中，
      並透過條件式註解將它們加到頁面裡，
      這些條件式註解只會為特定版本的瀏覽器載入這些樣式。
      ```html
        <!--[if IE7]>
          <link rel="stylesheet" href="ie7.css" type="text/css" />
        <![endif]-->
      ```


## 第五章 - *測試*
  測試CSS可能會很困難，因為有許多不同的平台、螢幕尺寸與裝置形體 (form factors) 需要進行檢測。
  - ### 測試為何困難？
    要徹底檢測CSS的變動，可能會耗費許多時間，也需要一些工具的輔助。
    需要思考的因素：
      1. 檢測網頁的瀏覽器是哪一種？
      2. 如何對不同作業系統上的幾種瀏覽器進行測試？
      3. 檢視網頁的視窗尺寸為何？
      4. 如何快速檢測為數眾多的網頁？
      5. 如何確認所見的結果是正確的？
      6. 如何在無法取得某些特定裝置的情況下，在這些裝置上檢測網站？
  - ### 哪些瀏覽器對測試而言是重要的？
    理想上，只需要支援有一定數量的使用者用來檢視網站的瀏覽器即可。
    透過分析工具，可以很容易地解析出使用者用來瀏覽網站的瀏覽器與裝置的各種版本。
  - ### 瀏覽器市佔率
    支援最近幾年釋出的主要瀏覽器是很重要的工作。
    Chrome、Firefox、Safari、Edge與其行動裝置的版本大部分都已符合標準的規範，瀏覽器行為不一致的情況也較之前少。
    若使用舊版瀏覽器的網站使用者並不多，也許就不需要特別為這些舊瀏覽器去維護樣式碼。
    - #### 從Google Analytics取得瀏覽器與螢幕解析度的統計資料
      [Google Analytics](https://analytics.google.com/) 是google所提供的免費服務，也是最常見的分析套件；
      能追蹤網站流量、使用者的操作行為以及提供其他網站瀏覽資訊等。
    - #### 瀏覽器資訊
      當「Browser」被選成主要考量時，瀏覽器資訊可在GA中的Audience -> Technology -> Browser & OS選單下找到。
      這些資訊可讓你瞭解有哪些瀏覽器會被用來瀏覽你的網站，
    - #### 螢幕解析度
      當「Screen Resolution」被選成主要考量時，螢幕解析度資訊也可在GA中的Audience -> Technology -> Browser & OS選單下找到，
      這些資訊呈現出用來瀏覽你的裝置螢幕尺寸為何。
  - ### 以幾種瀏覽器進行測試
    在不同瀏覽器上檢測CSS最常見的方法是以手動方式進行測試。
    目前主流的瀏覽器有:
    - Google Chrome
    - Firefox
    - Safari
    - Microsoft Edge

    就行動裝置的測試而言，也會需要從對應的市集(marketplace)中下載所需的瀏覽器。

    - #### iOS版的Safari
      iOS上的Safari可以透過iOS裝置上的原生應用程式或是使用Xcode裡面的iOS Simulator來測試
      要注意的是Xcode只能在Mac OS上執行，他沒辦法在Windows上安裝。
    - #### Android
      可以透過Android Studio中的擬真器(emulators)來進行在Android裝置上的測試
  - ### 以舊版瀏覽器進行測試
    - #### Internet Eplorer 與 Microsoft Edge
      可以從Microsoft的網站上面下載到Microsoft Edge和舊版的Internet Eplorer以供檢測使用。
    - #### Firefox
      可以從Firefox的網站上面下載到舊版的Firefox，只要找到你要測試的版本並下載在你的作業系統上能運行的版本即可。
    - #### Safari與iOS版的Safari
      因為Safari使用OS X上的WebKit框架來渲染網頁，要測試舊版的Safari會比較麻煩，需要找到舊版的Mac OS才行。
      不過，要進行舊版的Safari for iOS測試可以透過Xcode上的模擬器來進行。
    - #### Chrome
      然Google並沒有提供舊版的Chrome讓大家下載測試，不過每六週都會有新版的Chrome釋出，而且每一個新版本的採用率(adoption rate)都非常高。
  - ### 測試最新版本
    各瀏覽器最新的開發測試版：
    - [Chrome Canary](https://www.google.com/chrome/browser/canary.html)
    - [Firefox Aurora](https://nightly.mozilla.org)
    - [WebKit Nightly](https://nightly.webkit.org)

    Microsoft並沒有提供Edge的開發測試版，但經常會提供先期版本給[Windows Insider Program](https://insider.window)的會員進行測試。
  - ### 第三方測試服務
    採用第三方廠商所提供的服務，是另一種在多重作業系統上透過一些瀏覽器與模擬器來測試網站的方法。
  - ### 以開發者工具進行測試
    每一種主流瀏覽器都會附帶一組開發者工具，來協助開發者將網站做得更好。
    - [Chrome DevTools](https://developer.chrome.com/devtools)
    - [Safari for Developers](https://developer.apple.com/safari/tools/)
    - [Firefox Developer Tools](https://developer.mozilla.org/en-US/docs/Tools)
    - [Microsoft Edge Developer Tools](https://dev.modern.ie/platform/documentation/f12-devtools-guide/)
    - #### 模擬裝置尺寸
      要在不同的裝置形體 (如手機、平板等) 上進行測試，透過瀏覽器的開發者工具來模擬目標裝置的尺寸。
  - ### 視覺回歸測試 (visual regression testing)
    產生一張使用者介面的比較基準圖 (baseline image)，然後用它來與後續的使用者介面圖進行比較。
    - #### 視覺回歸測試的技巧
      - ##### 測試重要的東西
        測試越多，需要維護的就越多，與其要在大量的測試中打轉，不如只測試真正重要的。
        基底樣式 (base styles)，通常不太會再回歸；
        檢測更複雜且可能會更難處理的可複用元件，反而比較要緊。
      - ##### 保持測試粒度
        若有太多元件一起測試，很難找出造成一個回歸產生的確切原因，個別測試一個元件，才能維持測試的粒度。
      - ##### 使用不同的瀏覽器
        因為不同的瀏覽器間可能會有不一致的現象。
    - #### 以Gemini進行視覺回歸測試
      它能在任何主要瀏覽器上編寫自動為元素截圖的程序(Script)，然後讓這些截圖與基準圖作比較，並以不同的反白強調方式，將差異處標示出來。
      透過無介面瀏覽器 [PhantomJS](http://phantomjs.org) 來存取該操作介面。
      無介面瀏覽器 (headless browser) 是沒有使用者操作介面的網頁瀏覽器，
      能在不顯示網頁的情況下渲染網站並截取螢幕截圖。
      > [Gemini安裝](https://github.com/gemini-testing/gemini)、[PhantomJS安裝](https://phantomjs.org)
      <small>Gemini也可以測試其他使用 Selenium 或如 Sauce Labs 及 BrowserStack 等雲端服務的瀏覽器。</small>
      - ##### 組態
        安裝 Gemini 之後，需要在專案的根目錄下創建一個名為 `.gemini.js` 的檔案。
        [完整的組態選項列表](https://github.com/gemini-testing/gemini)
        範例：
        ```js
          module.exports = {
            rootUrl: 'http://127.0.0.1:8000',
            browsers: {
              phantomjs: {
                desiredCapabilities: {
                  browserName: 'phantomjs'
                }
              }
            }
          };
        ```
        根網址(root URL)設定成 http://127.0.0.1:8000 ，
        以 PhantomJS 來進行測試，而且用該瀏覽器截下來的圖，
        要以 `phantomjs` 為其檔名。(當使用多瀏覽器測試時，方便辨識)
      - ##### 測試
        編寫一個測試檔。
        Gemini 本身有一套功能，能開啟URL、選取特定元素、操作視窗並截取螢幕截圖等。
        ```js
          // Gemini 測試套組檔 (animal-tests.js)
          gemini.suite('animals', function(suite){
            suite.setUrl('/')
              .setCaptureElements('.animal')
              .capture('plain')
          });
        ```
        先宣告測試套組(test suite)，為其命名( `'animals'` )。
        網站的首頁( `/` )則透過 `setUrl` 指定成要開啟的URL。
        用 `.setCaptureElements` 選取要測試的元素，
        以 `.capture` 來截取螢幕截圖。
      - ##### 收集基準圖
        在進行任何測試前，要先收集基準圖，如此 Gemini 才能用它們來比較新的截圖。
        先在終端機 (terminal) 中執行 PhantomJS 與 Gemini，才能截取基準圖。
        - 開啟終端機視窗並輸入 `phontomjs -webdriver=4444` 指令。
          讓 PhantomJS 在 WebDriver 模式中的 4444 號埠上執行。
          是 Gemini 與瀏覽器互動的管道。
        - 另一個終端機跳到 `.gemini.js` 檔所在的目錄，
          執行 `gemini update test/gemini/animal-tests.js` 指令，以取得基準螢幕截圖。
          基準圖收集完成後，它們會被存放在 `gemini/screens/animals/plain` 這個新目錄底下。
      - ##### 測試回歸
        基準圖已經收集完成，可以測試回歸了。
        以 `gemini test -reporter html tests/gemini/animal-test.js` 指令來執行Gemini。
        這個指令要Gemini執行測試、比較螢幕截圖並將結果輸出到存放在gemini-report/index.html的HTML網頁中。
        - ###### Gemini的替代方案
          Wraith 與 PhantomCSS。
          都可以被用來開啟網站、透過PhantomJS (Webkit型的無介面瀏覽器) 或SlimerJS (Gecko型的無介面瀏覽器)來為元素截圖，並呈現元素目前版本與比較基準版本的不同。
          - [Wraith](http://bbc-news.github.io/wraith/index.html)
            由BBC開發而成。
            需要 CasperJS、PhantomJS 或 SlimerJS 以及 ImageMagick 與 Ruby 的支援。
          - [PhantomCSS](https://github.com/Huddle/PhantomCSS)
            由James Cryer 與 [Huddle](http://huddle.com)的開發團隊發展而成。
            需要 CasperJS 與 Resemble.JS 的支援，也可以搭配 PhantomJS 與 SlimerJS 使用。
  - ### 維護樣式碼
    樣式碼的品質可透過寫碼準則與樣式庫來維護。
    - #### 寫碼準則 (coding standards)
      團隊成員以同一方式來編寫樣式碼的指引方針。
      CSS寫碼準則通常會規定註解、格式、命名、選取器使用的慣用法。
      - ##### 寫碼準則範本
        1. 註解
          A. 每一個檔的開頭都應寫上註解，說明該檔案的內容：
            ```css
              /**
              * 這個檔案內含頁籤群組的樣式。
              * 頁籤群組只會用來含括帶有頁籤類別的元素。
              */
            ```
          
          B. 可能會產生混淆的屬性應該以註解說明：
            ```css
              .tab-group-flush {
                display: block;
                margin-left: -12px; /* 移除父容器的內距 */
                margin-right: -12px; /* 移除父容器的內距 */
              }
            ```
          
        2. 格式
          A. 規則集 (rulesets) 應該：
            - 若屬性不只一個，則應該要分行編寫。
            - 其中的宣告須縮排4格
            
          ```css
            /* 不正確的寫法 */
            .selector {
            property1: value;
            property2: value;
            }

            /* 不正確的寫法 */
            .selector {
                    property1: value;
                    property2: value;
            }

            /* 不正確的寫法 */
            .selector { property1: value; property2: value; }

            /* 正確的寫法 */
            .selector {
                property1: value;
                property2: value;
            }
          ```
          
          B. 宣告應該：
            - 在冒號後加上一個空格。
            - 結尾一定加上分號。

          ```css
            /* 不正確的寫法 */
            .selector {
                property1:value;
            }

            /* 不正確的寫法 */
            .selector {
                property1: value
            }

            /* 不正確的寫法 */
            .selector {
                property1 : value;
            }

            /* 正確的寫法 */
            .selector {
                property1: value;
            }
          ```
          
          C. 在幾個規則集有不同之 `background-position` 設定的情況下，規則集可以寫在一行。
          ```css
            /* 不正確的寫法 */
            .selector1 { property1: value; property2: value;}
            .selector2 { property1: value; property2: value;}
            .selector3 { property1: value; property2: value;}

            /* 正確的寫法 */
            .selector1 { background-position: 0 0; }
            .selector2 { background-position: 0 -10px; }
            .selector3 { background-position: 0 -10px; }
          ```
          
          D. 規則集與宣告後的空白必須移除。
        
        3. 選取器命名慣例：
          A. 只使用小寫字母。
            ```css
              /* 不正確的寫法 */
              .SeleCtor {}
              .SELECTOR {}

              /* 正確的寫法 */
              .selector {}
            ```
          
          B. 由多字組成的選取器必須以骨節式 (spinal-case) 表示。
            ```css
              /* 不正確的寫法 */
              .selectorWithMultipleWords {}
              .SELECTORWITHMULTIPLEWORDS {}
              .selector_with_multiple_words {}
              .selectorWith_multiple-words {}

              /* 正確的寫法 */
              .selector-with-multiple-words {}
            ```
          
          C. ID不能用來為元素訂樣式；請改用類別。
            ```css
              /* 不正確的寫法 */
              #element-to-style {}

              /* 正確的寫法 */
              .element-to-style {}
            ```
          
          D. 會用JavaScript調整的樣式 (不管框架為何)，必須以新增或刪除CSS類別的方式來進行。
            ```js
              /**
               *  不正確的寫法：元素樣式會被JavaScript中的樣式屬性改變
              */
             $('.js-menu-item').on('click', function (e) {
               $(this).css('background-color', '#FFFF00');
             });

             /**
               *  正確的寫法：元素樣式會透過JavaScript新增的類別來調整
              */
              $('.js-menu-item').on('click', function (e) {
                $(this).addClass('highlighted');
              });
            ```
          
          E. 作爲JavaScript選取器使用的類別與ID，必須加上 `js-` 字頭，而且不能寫在樣式表中。
            ```js
              /**
               *  不正確的寫法：帶有js-字頭的樣式不應該出現在樣式表中
              */
              #js-element-only-used-by-javascript {
                  background-color: #FFFF00;
              }

              /**
               *  不正確的寫法：透過指定元素樣式的類別在JavaScript中選取元素
              */
              $('.menu-item').on('click', function () {
                $(this).addClass('highlighted');
              });

             /**
               *  正確的寫法：在JavaScript中以用來在JavaScript中使用的選取器選取元素
              */
              $('.js-menu-item').on('click', function () {
                $(this).addClass('highlighted');
              });
            ```
          
          F. 必須使用有意義的類別名稱
            ```css
              /* 不正確的寫法：沒有意義的類別名稱 */
              .r {}

              /* 正確的寫法：有意義且具說明性的類別名稱 */
              .resident {}
            ```
          
          G. 類別名稱要描述被指定樣式的標的，而不是樣式本身
            ```css
              /* 不正確的寫法：描述要套用的樣式 */
              .float-left-bold {}

              /* 正確的寫法：描述要套用樣式的標的 */
              .sidebar-important {}
            ```
          
        4. 屬性
          A. 只能在 `border` 、 `margin` 與 `padding` 上使用屬性的速寫法
            ```css
              /* 不正確的寫法：在字型屬性上使用速寫法 */
              .selector {
                border: 1px solid #000000;
                font: 12px Arial, sans-serif;
              }

              /* 正確的寫法：只在border屬性上使用速寫法 */
              .selector {
                border: 1px solid #000000;
                font-family: Arial, sans-serif;
                font-size: 12px;
              }
            ```
          
          B. 屬性必須按照字母排序排列
            ```css
              /* 不正確的寫法 */
              .selector {
                padding: 12px;
                margin: 24px;
                border: 1px solid #000000;
              }

              /* 正確的寫法 */
              .selector {
                border: 1px solid #000000;
                margin: 24px;
                padding: 12px;
              }
            ```
          
          C. 值為0的屬性其單位必須省略
            ```css
              /* 不正確的寫法 */
              .selector {
                padding: 0px;
                margin: 20px;
                border: 1px solid #000000;
              }

              /* 正確的寫法 */
              .selector {
                border: 1px solid #000000;
                margin: 0;
                padding: 0;
              }
            ```
        
        可參照下列寫碼準則
          - [Google CSS 寫碼準則](http://bit.ly/2e68N3y)
          - [WordPress CSS](http://bit.ly/2fgLrp2)
          - [18F 前端指引](https://pages.18f.gov/frontend/#css)
    - #### 模版庫 (pattern library)
      是一組在網站上使用的操作介面模版，重要資訊包括：
        - 模版的使用時機
        - 簡單的模版使用說明
        - 為何要使用某特定模版的原因
      
      ex: [Yelp 模版庫](https://www.yelp.com/styleguide)、[MailChimp 模版庫](https://ux.mailchimp.com/patterns)
      - ##### 好處
        模版庫呈現了所有組成網站的元件，讓每位成員都能取得建造網站的基礎元件，也可確保成員們熟悉其運作方式。
        不需為每一個新專案重新製作這些基礎元件。
        讓所有元件都陳列在同一個地方，藉以建置出的使用者介面更一致。
      - ##### 建置模版庫
        包含 可運行的實作、使用時機的指引，以及呈現如何實作該模版的範例樣式碼。

      > <small>取得更多模版庫資源：http://styleguides.io</small>

## 第六章 - 樣式碼置放與重構策略
  - ### 從特定度低到特定度高之樣式的順序來組織CSS
    CSS樣式依據特定度與被引用的順序來套用，按照被套用的順序來組織CSS也是很合理的
    1. 正規化樣式 (normalizing styles)
    2. 基底樣式 (base styles)
    3. 組件及其容器使用的樣式
    4. 結構樣式 (structural styles)
    5. 工具樣式 (utility styles)
    6. 瀏覽器特定樣式 (如果一定需要的話)

    - #### 正規化樣式
      將各瀏覽器不一致的地方排除。
    - #### 基底樣式
      定義了網站中所有元件的起始樣式。
    - #### 組件與其容器的樣式
      以基底樣式為基礎，提供具視覺意涵的樣式，應該要能適用於全站的主要使用案例上，樣式上的任何調整，應該委派給父容器。
    - #### 結構化樣式
      包含組件與其容器，用來創建網頁的版面與適用於一般情況的尺寸。
    - #### 工具樣式
      特定度最高的樣式。像其他單一用途的樣式，由JavaScript所套用，會用到!important的類別，應該寫在這。
    - #### 瀏覽器特定樣式
      要支援傳統的瀏覽器，特別實作出的樣式。可能也會用到!important，也可能由網站依據條件而引用。
      不需要的時候，記得要將它們刪除。
    
    > <small><b>媒介查詢 (media queries)</b>
    > 用來在特定條件滿足時，為元素套用不同的樣式。
    > 媒體查詢應該儘可能地寫在靠近樣式宣告區塊的位置，而不是放在CSS的結尾處或另外存成一個檔案。</small>
  
  - ### 多檔還是單一大檔 ?
    - #### 供應CSS
      造訪網站時，瀏覽器會要求下載檔案然後進行解析並套用適當的樣式。
      因此，為了能迅速下載，這些檔案越小越好。
      - ##### 併接 (concatenation)
        減少需下載的檔案數來降低頁面下載時間的常用技術。
        - headings.css
        ```css
          /**
           * 本檔內含基本標頭元素的樣式
           */
          h1 {
            color: #333;
            font-size: 24px;
            margin-bottom: 6px;
            margin-left: 12px;
            margin-right: 6px;
            margin-top: 12px;
          }
        ```
        - lists.css
        ```css
          /**
           * 本檔內含列表元素的樣式
           */
          ul {
            list-style-type: none;
            padding-bottom: 12px;
            padding-left: 0;
            padding-top: 12px;
            padding-right: 0;
          }
        ```
        - 併接而成的CSS檔
        ```css
          /**
           * 本檔內含基本標頭元素的樣式
           */
          h1 {
            color: #333;
            font-size: 24px;
            margin-bottom: 6px;
            margin-left: 12px;
            margin-right: 6px;
            margin-top: 12px;
          }
          /**
           * 本檔內含列表元素的樣式
           */
          ul {
            list-style-type: none;
            padding-bottom: 12px;
            padding-left: 0;
            padding-top: 12px;
            padding-right: 0;
          }
        ```

      - ##### 縮整 (minification)
        是移除檔案不需要的空白、註解與新行碼 (newlines) 的操作。
        - 縮整後的CSS
        ```css
          h1{color:#333;font-size:24px;margin-bottom:6px;margin-left:12px;margin-right:6px;margin-top:12px;}ul{list-style-type:none;padding-bottom:12px;padding-left:0;padding-top:12px;padding-right:0;}
        ```
    - #### 單檔開發
      小型專案而言，將CSS放在一個檔中，依據CSS被引入的串接順序，適當地以註解將之分段組織好，
      ```css
        /**
         * 正規化樣式
         * -----------------------------------------------------
         */
        
        /**
         * 基底樣式
         * -----------------------------------------------------
         */

        /* 基底樣式：表單 */
        /* 基底樣式：標頭 */
        /* 基底樣式：影像 */
        /* 基底樣式：列表 */
        /* 基底樣式：表格 */
        /* 等等 */

        /**
         * 組件樣式
         * -----------------------------------------------------
         */

        /* 組件樣式：警告 */
        /* 組件樣式：按鈕 */
        /* 組件樣式：輪播 */
        /* 組件樣式：下拉式選單 */
        /* 組件樣式：模板 */
        /* 等等 */

        /**
         * 結構樣式
         * -----------------------------------------------------
         */

        /* 結構樣式：登出版面 */
        /* 結構樣式：側欄版面 */
        /* 結構樣式：主要版面 */
        /* 結構樣式：設定版面 */
        /* 等等 */

        /**
         * 工具樣式
         * -----------------------------------------------------
         */
      ```
      若到了某個臨界點，還是需要將CSS拆分成幾個檔案。

    - #### 多檔開發
      透過好幾個CSS檔來開發網站時，每個檔案的內容就可以聚焦。
      避免CSS被放在另一個比較不恰當的地方而影響到優化。
      ```markdown
        |-css/
        | |-normalizing-styles
        | |   |- normalize.css
        | |
        | |-base-styles
        | |   |- forms.css
        | |   |- headings.css
        | |   |- images.css
        | |   |- lists.css
        | |   |- tables.css
        | |   |- etc.
        | |
        | |-bcomponent-styles
        | |   |- alerts.css
        | |   |- buttons.css
        | |   |- carousel.css
        | |   |- dropdowns.css
        | |   |- modals.css
        | |   |- etc.
        | |
        | |-structural-styles
        | |   |- layout-checkout.css
        | |   |- layout-sidebar.css
        | |   |- layout-primary.css
        | |   |- layout-settings.css
        | |   |- etc.
        | |
        | |-utility-styles
        | |   |- utility.css
        | |
        | |-browser-specific-styles
        | |   |- ie8.css
      ```
      有這麼多的樣式檔，就不應該在HTML中把每一個都引進來。
      因為太多檔案要求會讓頁面的載入速度變慢。
  - ### 重構前檢核CSS
    高階的CSS評估準則：
    - 所用屬性列表
    - 使用特定屬性之宣告區塊列表
    - 所用之不同顏色的數量
    - 所用之最高與最低的特定度
    - 具最高與最低特定度的選擇器
    - 選擇器的長度

    推薦一個Google Chrome瀏覽器的外掛工具『CSS Dig』，
    只要到Chrome的擴充功能裡面搜尋 [CSS Dig](http://cssdig.com) 並下載，
    在網站內按下CSS Dig的圖示就可以使用，
    能夠分析網頁內可用的CSS，是一套能將樣式碼整理好的實用工具！

  - ### 重構策略
    應該儘可能只在常需被檢核與釋出的小且可控制的區段(chunks)上進行重構。
    若在一個小區段中進行樣式碼的重構，會變動且產生回歸的地方就比較少，測試起來也比較容易。
    建議每次只進行能很快佈署出去的小範圍變動。
    - #### 一致地架構規則集
      取決於要將宣告區塊寫成什麼格式，以及宣告的順序要如何安排。
    - #### 刪除廢碼
      廢碼(dead code)指的是有寫但沒有用到的碼。
      - ##### 未用宣告區塊 (unused declaration blocks)
        有寫但絕不會被用到的宣告區塊。
      - ##### 重複宣告區塊 (duplicate declaration blocks)
        因與其他現有宣告完全相同而變成不需要重複的宣告區塊。
        ```css
          h1 {
            font-size: 28px;
            font-weight: 900;
          }
          /* 重複宣告區塊 */
          h1 {
            font-size: 28px;
            font-weight: 900;
          }
        ```
      - ##### 重複宣告 (duplicate declarations)
        在同一規則集中，應避免出現重複的宣告，因為只有最後那一個宣告才會被套用。
        ```css
          h1 {
            font-size: 28px;
            font-weight: 900;
            font-weight: 900; /* 重複宣告 */
          }
        ```
    - #### 切斷CSS與JavaScript的耦合
      用來為元素指定樣式的類別與ID不應該在JavaScript中被用來選取元素，會產生相依性(dependency)，讓這些選取器不容易被修改。
      因為類別與ID一被修改，可能會造成JavaScript的錯誤。
      先在JavaScript中找到選取元素的地方，然後在選取器前加上 `js-` ，再將選取器加到定義元素的HTML裡頭即可。
    - #### 拆分基底樣式
      它們運用的是類型選取器(type selectors)。
      用『CSS Dig』 分析過網站後，Selectors 面板會列出不少選取器在何時與何處的使用資訊。
      將基底樣式用分組的方式列出來：
        - 標題 (`<h1>` - `<h6>`)
        - 文本 (`<p>`，`<fig>`，`<code>`)
        - 連結 (`<a>`)
        - 列表 (`<dl>`，`<ol>`，`<ul>`)
        - 表單 (`<form>`，`<legend>`，`<fieldset>`，`<input>`，`<button>`)
        - 表格 (`<table>`，`<thead>`，`<tbody>`，`<tfoot>`，`<tr>`，`<td>`)
        - 媒體 (`<audio>`，`<object>`，`<video>`)
      
      做完之後，使用『CSS Dig』再去找可以歸類在特定分類的選取器，找出最常用的屬性。
      依照下列步驟來處理：
        1. 在基底樣式中為要進行重構的類型選取器製作新的規則集。
        2. 將在所有類型選取器中找出的最常用屬性複製到新做好的規則集中。
        3. 移除其他規則集中可繼承自新基底樣式的重複樣式。

      範例：
        ```css
          /* 檔案：style.css */
          h1 {
            color: #000000;
            font-family: Helvetica, sans-serif;
            font-size: 32px;
            line-height: 1.2;
          }
          body > div > h1 {
            color: #000000;
            font-size: 32px;
            margin-bottom: 12px;
          }
          .section-condensed h1 {
            color: #000000;
            font-size: 16px;
          }
          .order-form h1 {
            font-family: Helvetica, sans-serif;
            color: #333333;
            text-decoration: underline;
          }
        ```
      - 第一步，製作一個新的規則集：
        ```css
          /* 檔案：headings.css */
          h1 { }
        ```
      - 接著，複製最常用的樣式到規則集裡頭：
        ```css
          /* 檔案：headings.css */
          h1 {
            color: #000000;
            font-family: Helvetica, sans-serif;
            font-size: 32px;
            line-height: 1.2;
          }
        ```
      - 最後，從規則集中移除重複的樣式，改由繼承基底樣式的樣式：
        ```css
          /* 檔案：style.css */
          body > div > h1 {
            margin-bottom: 12px;
          }
          .section-condensed h1 {
            font-size: 16px;
          }
          .order-form h1 {
            color: #333333;
            text-decoration: underline;
          }
        ```
      
      仔細檢查那些不包含在基本樣式中的樣式，看看這些樣式是否已經偏離了方向，
      若是，可將這些偏離方向的樣式移除。
    - #### 移除多餘的ID
      在一個選取器中多寫的那幾個ID都是多餘的。
      調降具更高特定度之選取器的特定度。
      範例：
      ```css
        #main-header > div > div > ul#main-menu {
          border-bottom: 1px solid #000000;
        }
      ```
      - 從選取器中移除多餘的ID
      ```css
        #main-header {
          border-bottom: 1px solid #000000;
        }
      ```
    - #### 將ID轉成類別
      多餘的ID被移除之後，其餘用到ID的選取器可以轉而使用類別。而且很容易就可以在需要的地方複用。
      若需要調整許多其他的選取器才能解決一個特定問題，比較好的方法是不將ID變成類別，等到有特定度更高的樣式需要被重構成較低特定度時，再來重構這部份的樣式碼。
    - #### 拆分工具樣式
      工具樣式是可運用 `!important` 例外的唯一樣式。當CSS併接的時候，工具樣式應該放在最後。
      使用瀏覽器的開發者工具進行分析。若分析後發現它並不需要用到 `!important` ，則應該可以放心地將它移除。
    - #### 定義可複用組件 (reusable components)
      是進行CSS重構時最棘手的工作之一。
      先選取一種常常被重複使用的介面模板 (interface pattern，如頁籤)，然後用一些時間檢視網站，看看有哪些地方使用。
      記下該模版任何不同的地方，然後更新所有現行的模版，轉而使用新寫的樣式碼。
      定義可複用組件有助於移除重複的CSS。
    - #### 移除行內CSS與過度模組化的類別
      移除行內 (inline) CSS與過度模組化的類別應該要同時進行，
      移除這二種東西，應該晚點做而不要太早做。
      在移除行內CSS之前，需要將它暫時放在樣式表末，也許還要用 `!important` 來維持它的特定度。
      檢查那些與基本及組件樣式不同的行內樣式，看看它是不是因設計或寫碼不一致所產生的。
      若是，則可放心地將該行內樣式移除。
      若樣式的不同是刻意做出來的，則應該透過元素的容器來使用該樣式。
      如果按照順序進行重構，應該：
        - 有一套自己的方法能一致地將CSS架構好。
        - 不能留有太多廢碼。
        - 已將CSS與JavaScript的耦合切斷。
        - 已建置好基本樣式。
        - 已透過移除多餘ID並將ID轉成類別的方式，將最高特定度降低。
        - 已將工具樣式拆分，並減少 `!important` 的使用。
        - 已定義可複用組件。
    - #### 隔離針對特定瀏覽器的CSS改裝
      為了克服瀏覽器的限制所做的改裝 (hacks)，很容易就會污染到CSS。
      在隔離之前，判斷是否不再支援該瀏覽器。
  - ### 成效評估
    - #### 網站壞了嗎？
      重構是在不改變樣式行為的前提下，進行重新寫碼的過程。
      先檢查外觀是否相同，若沒發現任何視覺回歸，再開始檢查其他的面向。
    - #### 低耦合
      將CSS與HTML間的耦合拆解掉。
      試著別讓選取器過度複雜化。
      `CSS Dig` 可協助找出複雜且超格的選取器，應盡量設法將它們一般化。
    - #### 低特定度
      選取器特定度是可以被估算，且被用來判斷CSS碼庫中是否含有許多不容易維護，且帶有高特定度之選取器的衡量標準。
      `CSS Dig` 能運用這個特質，篩選出選取器。
    - #### 檔案更少也更小
      「 併接 」 可減少需下載的檔案數，
      「 縮整 」 則可透過移除不必要之字元的方式，來降低檔案的大小。
    - #### UI錯誤數
      透過模版庫與視覺回歸測試這二種有效的方法，就可以越快偵測並診斷出問題。
    - #### 省下開發與檢測時間
      將CSS有條理地組織成幾個檔、建立編碼準則以及創建UI模版庫之後，建造並維護使用者介面的速度，會比之前要來得快上許多。
      除了縮短開發時程之外，檢測介面的速度也會變得更快。
