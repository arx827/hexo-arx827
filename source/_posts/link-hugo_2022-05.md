---
title: '[link]_hugo'
date: 2022-05-28 11:57:50
tags: [hugo, link]
---

<!-- more -->

# 入門
  - ## 快速開始
    - ### 第 1 步 安裝 Hugo
      ```sh
        brew install hugo
      ```
      驗證新安裝
      ```sh
        hugo version
      ```
    
    - ### 第 2 步 創建新站點
      ```sh
        hugo new site siteName
      ```
      以上將在名為 `siteName`。
    
    - ### 第 3 步 添加主題
      [相關主題列表](https://themes.gohugo.io/)
      首先，從GitHub 下載主題並將其添加到您網站的themes目錄中：

      <small>以[Ananke](https://themes.gohugo.io/themes/gohugo-theme-ananke/)主題為例</small>

      ```sh
        cd siteName
        git init
        
        git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
        # or
        git clone https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
      ```

      然後，將主題添加到站點配置中：

      ```sh
        echo theme = \'ananke\' >> config.toml
      ```
    
    - ### 第 4 步 添加一些內容
      ```sh
        hugo new posts/my-first-post.md
      ```
      新建內容文字如下：
      ```sh
        ---
        title: "My First Post"
        date: 2019-03-26T08:47:11+01:00
        draft: true
        ---
      ```
    
    - ### 第 5 步 啟動 Hugo 服務器
      ```sh
        hugo server -D
      ```
      預設server站點為 http://localhost:1313/
    
    - ### 第 6 步 自定義主題
      在發布之前，需要進行一些調整
      - #### 站點配置
        將 config.toml 開啟
        ```sh
          baseURL = 'http://example.org/'
          languageCode = 'en-us'
          title = 'My New Hugo Site'
          theme = 'ananke'
        ```
        更改title為個人網站名稱。
    
    - ### 第 7 步 建構靜態頁面
      ```sh
        hugo -D
      ```
      默認情況下，會產生在`./public/`目錄中。
  
  - ## 資料夾結構說明
    ```
      .
      ├── archetypes
      ├── content
      ├── data
      ├── layouts
      ├── static
      ├── themes
      └── config.toml
    ```
    - ### archetypes
      放文章模板文件的地方，當你 new 一個新的 content files 時，會根據這邊的模板產生 markdown 文件，例如 archetypes/default.md，若你 new 的文章頂層資料夾名稱 (top level path) 對應不到模板時，會使用 default.md 作為模板生成文件。

    - ### content
      所有 new 出來的文章都會放在這；
      如果你想要把文章個別分不同的 setion (top level path)，
      例如 drafts（草稿）、posts（已發布文章），可透過新增文章指令，指定的不同頂層路徑，生成文件到不同資料夾中。
      ```sh
        hugo new drafts/my-drafts.md # 新增一份草稿
      ```
      補充說明: 此例你必須透過定義 drafts.md 模板內容 draft: true，
      讓生成 草稿文件 真的是 草稿狀態，
      否則文件一樣會是已發布狀態。

    - ### data
      可以把一些資料集放在這，支援格式有 YAML, JSON, 或是 TOML；
      換句話說，這可以當作你的資料庫使用，例如你的網站是專門介紹咖啡的，
      你有一組每個縣市最好喝的咖啡清單，就可以在這邊創建：
      ```json
        {
          "taipei_no_1": "鐵定好喝咖啡店",
          "taichung_no_1": "1976 咖啡館",
          ...
        }
      ```
    
    - ### layouts
      靜態網站的 .html 文件都會放在這，但你 new 的專案一開始會是空的，主要都是由佈景建構 layouts。

    - ### static
      靜態資源檔案，例如圖片、js、css 等會放在這邊。

    - ### themes
      放各種佈景的地方，如果不常換來換去的話，底下只會放一種佈景，
      你可以建置一個 sandbox，透過 --theme 參數去切換嘗試各種不同佈景，在本地跑起來看看他們的樣子。

    - ### config.toml
      網站 environments 配置檔，所有網站建置參數都可在此設置。


<div style="text-align: center; color:#aaa;"><small>/... 未完待續 .../</small></div>



- ## 參考資源：
  - [Hugo 官網](https://gohugo.io/)