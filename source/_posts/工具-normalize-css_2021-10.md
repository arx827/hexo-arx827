---
title: '[工具]_normalize.css'
date: 2021-10-26 03:23:46
tags: [工具, CSS]
---

normalize.css 最大的特色就是保留原本預設 HTML 標籤的樣式，
僅針對不同瀏覽器與各版本間不相容的標籤進行些微調整。
目的在一開始將各瀏覽器之間的差異進行調整。

<!-- more -->

```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document 文件
   ========================================================================== */

/**
 * 1. 修正所有瀏覽器中的行高。
 * 2. 避免在 iOS 中，因螢幕方向的改變而調整字型大小。
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections 段落
   ========================================================================== */

/**
 * 移除所有瀏覽器中的 margin。
 */

body {
  margin: 0;
}

/**
 * 在 IE 中一致地呈現 `main` 元素。
 */

main {
  display: block;
}

/**
 * 在 Chrome、Firefox 與 Safari 瀏覽器中，修正寫在 `section` 與 `article` 內之 `h1` 元素
 * 的字型大小與邊寬。
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content 群組內容
   ========================================================================== */

/**
 * 1. 在 Firefox 中新增正確的盒框尺寸。
 * 2. 在 Edge 與 IE 中顯示 overflow。
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. 在所有瀏覽器中，修正繼承與字型大小的調整。
 * 2. 在所有瀏覽器中，修正突兀的 `em` 字型大小單位。
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics 文本層級語意
   ========================================================================== */

/**
 * 在 IE10 中，移除套用在 active link 上的灰色背景。
 */

a {
  background-color: transparent;
}

/**
 * 1. 去除 Chrome 57- 的底部邊框。
 * 2. 在 Chrome、Edge、IE、Opera 和 Safari 瀏覽器中，新增正確的文本修飾。
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * 在 Chrome、Edge 和 Safari 瀏覽器中，新增正確的字型粗細。
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. 在所有瀏覽器中，修正字型大小的繼承與縮放。
 * 2. 在所有瀏覽器中，修正突兀的 `em` 字型大小單位。
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * 在所有瀏覽器中，新增正確的字型大小。
 */

small {
  font-size: 80%;
}

/**
 * 避免 `sub` 與 `sup` 元素影響到所有瀏覽器中的行高。
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content 嵌入內容
   ========================================================================== */

/**
 * 在 IE10 與之前瀏覽器中，移除連結中影像的邊框。
 */

img {
  border-style: none;
}

/* Forms 表單
   ========================================================================== */

/**
 * 1. 在所有瀏覽器中，調整字型樣式 (視需要調整)。
 * 2. 在 Firefox 和 Safari 中，移除邊距。
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * 在 IE 中顯示 overflow
 * 1. 在 Edge 中顯示 overflow
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * 在 Edge、Firefox 與 IE 中，移除字型形變的繼承。
 * 1. 在 Firefox 中，移除字型形變的繼承。
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * 在 iOS 和 Safari 中，修正無法調整可點按類型樣式的問題。
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * 在 Firefox 中，移除內邊框與內距。
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * 回存之前規則未設定的 focus 樣式。
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * 在 Firefox 中，修正 padding。
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. 在 Edge 和 IE 中，修正文字換行。
 * 2. 在 IE 中，修正由 `fieldset` 元素繼承而來的顏色。
 * 3. 在所有瀏覽器中，移除內距，讓開發者不會因將 `fieldset` 設為0而造成問題。
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * 在 Chrome、Firefox 和 Opera 中，新增正確的垂直對齊。
 */

progress {
  vertical-align: baseline;
}

/**
 * 在 IE 10+ 中，刪除預設的垂直捲軸。
 */

textarea {
  overflow: auto;
}

/**
 * 1. 在 IE10 與之前的瀏覽器中，新增正確的盒框大小。
 * 2. 在 IE10 與之前的瀏覽器中，移除內距。
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * 在 Chrome 中，為遞增或遞減按鈕修正游標樣式。
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. 在 Chrome 和 Safari 中，修正突兀的外觀。
 * 2. 在 Safari 中，修正外框樣式。
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * 在 macOS 上的 Chrome 和 Safari 中，移除內距。
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. 在 iOS 和 Safari 中，修正無法調整可點按類型樣式的問題。
 * 2. 在 Safari 中，將字型屬性改為 `inherit`。
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive 互動
   ========================================================================== */

/*
 * 在 Edge、IE 10+ 和 Firefox 中，新增正確的 display。
 */

details {
  display: block;
}

/*
 * 在所有瀏覽器中，新增正確的 display。
 */

summary {
  display: list-item;
}

/* Misc 雜項
   ========================================================================== */

/**
 * 在 IE 10+ 中，新增正確的 display。
 */

template {
  display: none;
}

/**
 * 在 IE 10 中，新增正確的 display。
 */

[hidden] {
  display: none;
}
```
