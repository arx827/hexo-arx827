---
title: '[筆記]_NVM_Windows'
date: 2021-10-27 01:59:58
tags: ['筆記', 'NVM', '管理工具']
---

- ## NVM (Node Version Manager) for Windows
  是 Node.js 的版本管理工具，
  因為不同的專案可能使用不同 Node.js 版本，在同一台主機上安裝多個版本環境時，
  可利用 NVM 來管理 Node.js 的版本控制和快速切換。

  <!-- more -->

  安裝流程：
  1. 卸載(移除)原有的node相關目錄、檔案 (含npm、node)
  2. 安裝NVM
  3. 使用NVM 安裝Node指定版本


  - ### 卸載(移除)原有的node相關目錄、檔案 (含npm、node)
    - 在移除軟體中，卸載node.js
    - 在環境變數中刪除所有與node相關的路徑
    - 刪除以下路徑的文件
      > C:\Program Files (x86)\nodejs
      > C:\Program Files\nodejs
      > C:\Users{User}\AppData\Roaming\npm
      > C:\Users{User}\AppData\Roaming\npm-cache
      > C:\Users{User}\node_modules (電腦上的路徑)
  
  - ### 安裝NVM
    到[GitHub](https://github.com/coreybutler/nvm-windows/releases)的項目下載地址，
    選擇下載 `nvm-setup.zip`，解壓縮後開啟安裝程式即可。
    找到 install.cmd 檔案並執行設定Path，直接按Enter進行設定
      #### 確認是否安裝成功
      ```shell
        > nvm version
      ```

      - 查詢結果
        ```shell
          > 1.1.7
        ```

  - ### 使用NVM 安裝Node指定版本
    - #### 查看可安裝的nodejs版本
      ```shell
        > nvm list available
      ```
    
    - #### 查看已安裝的nodejs版本
      ```shell
        > nvm list
      ```
      - 如果是第一次安装，使用該命令結果如下：
        ```shell
          No installations recognized.
        ```
    
    - #### 安裝指定Nodejs版本
      ```shell
        > nvm install <version>
      ```
    
    - #### 切換到指定Nodejs版本
      ```shell
        > nvm use <version>
      ```
    
    - #### 設定預設使用該版本的node 避免下次重啟後又恢復預設
      ```shell
        > nvm alias default <version>
      ```
    - #### 刪除指定版本
      ```shell
        > nvm uninstall <version>
      ```