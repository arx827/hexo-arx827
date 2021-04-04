---
title: '[議題]_關於那些被IE排擠的屬性'
date: 2021-02-23 10:18:31
tags: [CSS, 被IE排擠, 議題]
---

- #### CSS
  - ##### 多行文本溢出顯示...
    - ``-webkit-line-clamp``
    - 需搭配 -webkit-box-orient 使用
    - 目前支援line-clamp的，只有Chrome與Safari
    - Firefox與IE，需用高度來將超出的文字給隱藏起來

    ```css
      p{
        overflow: hidden;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 3;
        line-height: 24px;
        height: 72px;
      }
    ```

    > [[Can I use] -webkit-line-clamp](https://caniuse.com/?search=line-clamp)
    > [[Can I use] -webkit-box-orient](https://caniuse.com/?search=-webkit-box-orient)
    > [[參考] 免寫程式！透過CSS3將多行文字自動省略，並出現… - 梅問題教學網](https://www.minwt.com/webdesign-dev/css/18447.html) - 2017
    > [[參考] 多行文本溢出顯示...的方法 - ITREAD](https://www.itread01.com/content/1502438188.html) - 2017
    > [[參考] line-clamp - CSS-TRICKS](https://css-tricks.com/almanac/properties/l/line-clamp/) - 2018
    > [[參考] [iT邦] line-clamp - futian_shen](https://ithelp.ithome.com.tw/articles/10245872) - 2020
    > [[參考] 想知道嗎：Text-overflow把行尾變成… - Medium](https://wsw0615.medium.com/%E6%83%B3%E7%9F%A5%E9%81%93%E5%97%8E-text-overflow%E6%8A%8A%E8%A1%8C%E5%B0%BE%E8%AE%8A%E6%88%90-e86ad8bf827c) - 2020
  
  - ##### Flex
    - ``flex: 1;``

<!-- more -->


