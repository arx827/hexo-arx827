---
title: '[速查表]_Emmet'
date: 2021-02-23 15:12:52
tags: [Emmet, 速查表]
---

### <font color=#FF6600>基本階層語法</font> ###
  - #### ``nav>ul>li`` ####
  ```html
    <nav>
      <ul>
        <li></li>
      </ul>
    </nav>
  ```


<!-- more -->

---
### <font color=#FF6600>加入運算式「*」</font> ###
  - #### ``ul>li*5`` ####
  ```html
    <ul>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  ```
---
### <font color=#FF6600>加入字元變數「$」</font> ###
  - #### ``ul>li.item$*5`` ####
  ```html
    <ul>
      <li class="item1"></li>
      <li class="item2"></li>
      <li class="item3"></li>
      <li class="item4"></li>
      <li class="item5"></li>
    </ul>
  ```
  - #### ``h$[title=item$]{Header $}*3`` ####
  ```html
    <h1 title="item1">Header 1</h1>
    <h2 title="item2">Header 2</h2>
    <h3 title="item3">Header 3</h3>
  ```
  - #### ``ul>li.item$$$*5`` ####
  ```html
    <ul>
      <li class="item001"></li>
      <li class="item002"></li>
      <li class="item003"></li>
      <li class="item004"></li>
      <li class="item005"></li>
    </ul>
  ```
  - #### ``ul>li.item$@-*5`` ####
  ```html
    <ul>
      <li class="item5"></li>
      <li class="item4"></li>
      <li class="item3"></li>
      <li class="item2"></li>
      <li class="item1"></li>
    </ul>
  ```
  - #### ``ul>li.item$@3*5`` ####
  ```html
    <ul>
      <li class="item3"></li>
      <li class="item4"></li>
      <li class="item5"></li>
      <li class="item6"></li>
      <li class="item7"></li>
    </ul>
  ```
  - #### ``form#search.wide`` ####
  ```html
    <form id="search" class="wide"></form>
  ```
  - #### ``p.class1.class2.class3`` ####
  ```html
    <p class="class1 class2 class3"></p>
  ```
---
### <font color=#FF6600>ID and CLASS attributes 快速輸出id和class標籤結構</font> ###
  - #### ``#header`` ####
    ```html
      <div id="header"></div>
    ```
  - #### ``.header`` ####
    ```html
      <div class="header"></div>
    ```
---
### <font color=#FF6600>Sibling: + 組合標籤</font> ###
  - #### ``div+p+bq`` ####
    ```html
      <div></div>
      <p></p>
      <blockquote></blockquote>
    ```
---
### <font color=#FF6600>Climb-up: ^</font> ###
  - #### ``div+div>p>span+em^bq`` ####
    ```html
      <div></div>
      <div>
        <p>
            <span></span>
            <em></em>
        </p>
        <blockquote></blockquote>
      </div>
    ```
  - #### ``div+div>p>span+em^^bq`` ####
    ```html
      <div></div>
      <div>
        <p>
            <span></span>
            <em></em>
        </p>
      </div>
      <blockquote></blockquote>
    ```
---
### <font color=#FF6600>Grouping: ()</font> ###
  - #### ``div>(header>ul>li*2>a)+footer>p`` ####
    ```html
      <div>
        <header>
          <ul>
            <li><a href=""></a></li>
            <li><a href=""></a></li>
          </ul>
        </header>
        <footer>
          <p></p>
        </footer>
      </div>
    ```
  - #### ``(div>dl>(dt+dd)*3)+footer>p`` ####
    ```html
      <div>
        <dl>
          <dt></dt><dd></dd>
          <dt></dt><dd></dd>
          <dt></dt><dd></dd>
        </dl>
      </div>
      <footer>
        <p></p>
      </footer>
    ```
---
### <font color=#FF6600>Custom attributes 自定義對象</font> ###
  - #### ``p[title="Hello world"]`` ####
    ```html
      <p title="Hello world"></p>
    ```
  - #### ``td[rowspan=2 colspan=3 title]`` ####
    ```html
      <td rowspan="2" colspan="3" title=""></td>
    ```
  - #### ``[a='value1' b="value2"]`` ####
    ```html
      <div a="value1" b="value2"></div>
    ```
---
### <font color=#FF6600>Text: {}</font> ###
  - #### ``a{Click me}`` ####
    ```html
      <a href="">Click me</a>
    ```
  - #### ``p>{Click }+a{here}+{ to continue}`` ####
    ```html
      <p>Click<a href="">here</a>to continue</p>
    ```
---
### <font color=#FF6600>Implicit tag names</font> ###
  - #### ``.class`` ####
    ```html
      <div class="class"></div>
    ```
  - #### ``em>.class`` ####
    ```html
      <em><span class="class"></span></em>
    ```
  - #### ``ul>.class`` ####
    ```html
      <ul><li class="class"></li></ul>
    ```
  - #### ``table>.row>.col`` ####
    ```html
      <table>
        <tr class="row">
          <td class="col"></td>
        </tr>
    </table>
    ```
  - #### ``html:5`` ####
    ```html
      <!doctype html>
      <html lang="en">
          <head><meta charset="UTF-8" />
          <title>Document</title>
          </head>
      <body>
      </body>
      </html>
    ```
---
### <font color=#FF6600>html元素快速輸出</font> ###
  - #### ``a`` ####
    ```html
      <a href=""></a>
    ```
  - #### ``a:link`` ####
    ```html
      <a href="http://"></a>
    ```
  - #### ``a:mail`` ####
    ```html
      <a href="mailto:"></a>
    ```
  - #### ``abbr`` ####
    ```html
      <abbr title=""></abbr>
    ```
  - #### ``acronym`` ####
    ```html
      <acronym title=""></acronym>
    ```
  - #### ``base`` ####
    ```html
      <base href="" />
    ```
  - #### ``basefont`` ####
    ```html
      <basefont />
    ```
  - #### ``br`` ####
    ```html
      <br />
    ```
  - #### ``frame`` ####
    ```html
      <frame />
    ```
  - #### ``hr`` ####
    ```html
      <hr />
    ```
  - #### ``bdo`` ####
    ```html
      <bdo dir=""></bdo>
    ```
  - #### ``bdo:r`` ####
    ```html
      <bdo dir="rtl"></bdo>
    ```
  - #### ``bdo:l`` ####
    ```html
      <bdo dir="ltr"></bdo>
    ```
  - #### ``col`` ####
    ```html
      <col />
    ```
  - #### ``link`` ####
    ```html
      <link rel="stylesheet" href="" />
    ```
  - #### ``link:css`` ####
    ```html
      <link rel="stylesheet" href="style.css" />
    ```
  - #### ``link:print`` ####
    ```html
      <link rel="stylesheet" href="print.css" media="print" />
    ```
  - #### ``link:favicon`` ####
    ```html
      <link rel="shortcut icon" type="image/x-icon" href="favicon.ico" />
    ```
  - #### ``link:touch`` ####
    ```html
      <link rel="apple-touch-icon" href="favicon.png" />
    ```
  - #### ``link:rss`` ####
    ```html
      <link rel="alternate" type="application/rss+xml" title="RSS" href="rss.xml" />
    ```
  - #### ``link:atom`` ####
    ```html
      <link rel="alternate" type="application/atom+xml" title="Atom" href="atom.xml" />
    ```
  - #### ``meta`` ####
    ```html
      <meta />
    ```
  - #### ``meta:utf`` ####
    ```html
      <meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
    ```
  - #### ``meta:win`` ####
    ```html
      <meta http-equiv="Content-Type" content="text/html;charset=windows-1251" />
    ```
  - #### ``meta:vp`` ####
    ```html
      <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0" />
    ```
  - #### ``meta:compat`` ####
    ```html
      <meta http-equiv="X-UA-Compatible" content="IE=7" />
    ```
  - #### ``style`` ####
    ```html
      <style></style>
    ```
  - #### ``script`` ####
    ```html
      <script></script>
    ```
  - #### ``script:src`` ####
    ```html
      <script src=""></script>
    ```
  - #### ``img`` ####
    ```html
      <img src="" alt="" />
    ```
  - #### ``iframe`` ####
    ```html
      <iframe src="" frameborder="0"></iframe>
    ```
  - #### ``embed`` ####
    ```html
      <embed src="" type="" />
    ```
  - #### ``object`` ####
    ```html
      <object data="" type=""></object>
    ```
  - #### ``param`` ####
    ```html
      <param name="" value="" />
    ```
  - #### ``map`` ####
    ```html
      <map name=""></map>
    ```
  - #### ``area`` ####
    ```html
      <area shape="" coords="" href="" alt="" />
    ```
  - #### ``area:d`` ####
    ```html
      <area shape="default" href="" alt="" />
    ```
  - #### ``area:c`` ####
    ```html
      <area shape="circle" coords="" href="" alt="" />
    ```
  - #### ``area:r`` ####
    ```html
      <area shape="rect" coords="" href="" alt="" />
    ```
  - #### ``area:p`` ####
    ```html
      <area shape="poly" coords="" href="" alt="" />
    ```
  - #### ``form`` ####
    ```html
      <form action=""></form>
    ```
  - #### ``form:get`` ####
    ```html
      <form action="" method="get"></form>
    ```
  - #### ``form:post`` ####
    ```html
      <form action="" method="post"></form>
    ```
  - #### ``label`` ####
    ```html
      <label for=""></label>
    ```
  - #### ``input`` ####
    ```html
      <input type="text" />
    ```
  - #### ``inp`` ####
    ```html
      <input type="text" name="" id="" />
    ```
  - #### ``input:hidden`` 或 ``input[type=hidden name]`` 或 ``input:h`` 或 ``input:hidden`` ####
    ```html
      <input type="hidden" name="" />
    ```
  - #### ``input:text`` 或 ``input:t`` 或 ``inp`` ####
    ```html
      <input type="text" name="" id="" />
    ```
  - #### ``input:search`` 或 ``inp[type=search]`` ####
    ```html
      <input type="search" name="" id="" />
    ```
  - #### ``input:email`` 或 ``inp[type=email]`` ####
    ```html
      <input type="email" name="" id="" />
    ```
  - #### ``input:url`` 或 ``inp[type=url]`` ####
    ```html
      <input type="url" name="" id="" />
    ```
  - #### ``input:password`` 或 ``inp[type=password]`` 或 ``input:p`` 或 ``input:password`` ####
    ```html
      <input type="password" name="" id="" />
    ```
  - #### ``input:datetime`` 或 ``inp[type=datetime]`` ####
    ```html
      <input type="datetime" name="" id="" />
    ```
  - #### ``input:date`` 或 ``inp[type=date]`` ####
    ```html
      <input type="date" name="" id="" />
    ```
  - #### ``input:datetime-local`` 或 ``inp[type=datetime-local]`` ####
    ```html
      <input type="datetime-local" name="" id="" />
    ```
  - #### ``input:month`` 或 ``inp[type=month]`` ####
    ```html
      <input type="month" name="" id="" />
    ```
  - #### ``input:week`` 或 ``inp[type=week]`` ####
    ```html
      <input type="week" name="" id="" />
    ```
  - #### ``input:time`` 或 ``inp[type=time]`` ####
    ```html
      <input type="time" name="" id="" />
    ```
  - #### ``input:number`` 或 ``inp[type=number]`` ####
    ```html
      <input type="number" name="" id="" />
    ```
  - #### ``input:color`` 或 ``inp[type=color]`` ####
    ```html
      <input type="color" name="" id="" />
    ```
  - #### ``input:c`` 或 ``input:checkbox`` ####
    ```html
      <input type="checkbox" name="" id="" />
    ```
  - #### ``input:radio`` 或 ``inp[type=radio]`` 或 ``input:r`` ####
    ```html
      <input type="radio" name="" id="" />
    ```
  - #### ``input:range`` 或 ``inp[type=range]`` ####
    ```html
      <input type="range" name="" id="" />
    ```
  - #### ``input:file`` 或 ``inp[type=file]`` 或 ``input:f`` ####
    ```html
      <input type="file" name="" id="" />
    ```
  - #### ``input:submit`` 或 ``input:s`` ####
    ```html
      <input type="submit" value="" />
    ```
  - #### ``input:image`` ####
    ```html
      <input type="image" src="" alt="" />
    ```
  - #### ``input:image`` 或 ``input:i`` ####
    ```html
      <input type="image" src="" alt="" />
    ```
  - #### ``input:button`` ####
    ```html
      <input type="button" value="" />
    ```
  - #### ``input:button`` 或 ``input:b`` ####
    ```html
      <input type="button" value="" />
    ```
  - #### ``isindex`` ####
    ```html
      <isindex />
    ```
  - #### ``input:reset`` 或 ``input:button[type=reset]`` ####
    ```html
      <input type="reset" value="" />
    ```
  - #### ``select`` ####
    ```html
      <select name="" id=""></select>
    ```
  - #### ``option`` ####
    ```html
      <option value=""></option>
    ```
  - #### ``textarea`` ####
    ```html
      <textarea name="" id="" cols="30" rows="10"></textarea>
    ```
  - #### ``menu:context`` 或 ``menu[type=context]>`` 或 ``menu:c`` ####
    ```html
      <menu type="context"></menu>
    ```
  - #### ``menu:toolbar`` 或 ``menu[type=toolbar]>`` 或 ``menu:t`` ####
    ```html
      <menu type="toolbar"></menu>
    ```
  - #### ``video`` ####
    ```html
      <video src=""></video>
    ```
  - #### ``audio`` ####
    ```html
      <audio src=""></audio>
    ```
  - #### ``html:xml`` ####
    ```html
      <html xmlns="http://www.w3.org/1999/xhtml"></html>
    ```
  - #### ``keygen`` ####
    ```html
      <keygen />
    ```
  - #### ``command`` ####
    ```html
      <command />
    ```
  - #### ``bq`` 或 ``blockquote`` ####
    ```html
      <blockquote></blockquote>
    ```
  - #### ``acr`` 或 ``acronym`` ####
    ```html
      <acronym title=""></acronym>
    ```
  - #### ``fig`` 或 ``figure`` ####
    ```html
      <figure></figure>
    ```
  - #### ``figc`` 或 ``figcaption`` ####
    ```html
      <figcaption></figcaption>
    ```
  - #### ``ifr`` 或 ``iframe`` ####
    ```html
      <iframe src="" frameborder="0"></iframe>
    ```
  - #### ``emb`` 或 ``embed`` ####
    ```html
      <embed src="" type="" />
    ```
  - #### ``obj`` 或 ``object`` ####
    ```html
      <object data="" type=""></object>
    ```
  - #### ``src`` 或 ``source`` ####
    ```html
      <source></source>
    ```
  - #### ``cap`` 或 ``caption`` ####
    ```html
      <caption></caption>
    ```
  - #### ``colg`` 或 ``colgroup`` ####
    ```html
      <colgroup></colgroup>
    ```
  - #### ``fst`` 或 ``fset`` 或 ``fieldset`` ####
    ```html
      <fieldset></fieldset>
    ```
  - #### ``btn`` 或 ``button`` ####
    ```html
      <button></button>
    ```
  - #### ``btn:b`` 或 ``button[type=button]`` ####
    ```html
      <button type="button"></button>
    ```
  - #### ``btn:r`` 或 ``button[type=reset]`` ####
    ```html
      <button type="reset"></button>
    ```
  - #### ``btn:s`` 或 ``button[type=submit]`` ####
    ```html
      <button type="submit"></button>
    ```
  - #### ``optg`` 或 ``optgroup`` ####
    ```html
      <optgroup></optgroup>
    ```
  - #### ``opt`` 或 ``option`` ####
    ```html
      <option value=""></option>
    ```
  - #### ``tarea`` 或 ``textarea`` ####
    ```html
      <textarea name="" id="" cols="30" rows="10"></textarea>
    ```
  - #### ``leg`` 或 ``legend`` ####
    ```html
      <legend></legend>
    ```
  - #### ``sect`` 或 ``section`` ####
    ```html
      <section></section>
    ```
  - #### ``art`` 或 ``article`` ####
    ```html
      <article></article>
    ```
  - #### ``hdr`` 或 ``header`` ####
    ```html
      <header></header>
    ```
  - #### ``ftr`` 或 ``footer`` ####
    ```html
      <footer></footer>
    ```
  - #### ``adr`` 或 ``address`` ####
    ```html
      <address></address>
    ```
  - #### ``dlg`` 或 ``dialog`` ####
    ```html
      <dialog></dialog>
    ```
  - #### ``str`` 或 ``strong`` ####
    ```html
      <strong></strong>
    ```
  - #### ``prog`` 或 ``progress`` ####
    ```html
      <progress></progress>
    ```
  - #### ``datag`` 或 ``datagrid`` ####
    ```html
      <datagrid></datagrid>
    ```
  - #### ``datal`` 或 ``datalist`` ####
    ```html
      <datalist></datalist>
    ```
  - #### ``kg`` 或 ``keygen`` ####
    ```html
      <keygen />
    ```
  - #### ``out`` 或 ``output`` ####
    ```html
      <output></output>
    ```
  - #### ``det`` 或 ``details`` ####
    ```html
      <details></details>
    ```
  - #### ``cmd`` 或 ``command`` ####
    ```html
      <command />
    ```
  - #### ``ol+`` 或 ``ol>li`` ####
    ```html
      <ol><li></li></ol>
    ```
  - #### ``ul+`` 或 ``ul>li`` ####
    ```html
      <ul><li></li></ul>
    ```
  - #### ``dl+`` 或 ``dl>dt+dd`` ####
    ```html
      <dl><dt></dt><dd></dd></dl>
    ```
  - #### ``map+`` 或 ``map>area`` ####
    ```html
      <map name=""><area shape="" coords="" href="" alt="" /></map>
    ```
  - #### ``table+`` 或 ``table>tr>td`` ####
    ```html
      <table><tr><td></td></tr></table>
    ```
  - #### ``colgroup+`` 或 ``colg+`` 或 ``colgroup>col`` ####
    ```html
      <colgroup> <col /> </colgroup>
    ```
  - #### ``tr+`` 或 ``tr>td`` ####
    ```html
      <tr><td></td></tr>
    ```
  - #### ``select+`` 或 ``select>option`` ####
    ```html
      <select name="" id=""> <option value=""></option> </select>
    ```
  - #### ``optgroup+`` 或 ``optg+`` 或 ``optgroup>option`` ####
    ```html
      <optgroup><option value=""></option></optgroup>
    ```
  - #### ``!!!`` ####
    ```html
      <!doctype html>
    ```
  - #### ``!!!4t`` ####
    ```html
      <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    ```
  - #### ``!!!4s`` ####
    ```html
      <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
    ```
  - #### ``!!!xt`` ####
    ```html
      <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    ```
  - #### ``!!!xs`` ####
    ```html
      <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    ```
  - #### ``!!!xxs`` ####
    ```html
      <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
    ```
  - #### ``c`` ####
    ```html
      <!-- ${child} -->
    ```
  - #### ``cc:ie6`` ####
    ```html
      <!--[if lte IE 6]> ${child} <![endif]-->
    ```
  - #### ``cc:ie`` ####
    ```html
      <!--[if IE]> ${child} <![endif]-->
    ```
  - #### ``cc:noie`` ####
    ```html
      <!--[if !IE]><!--> ${child} <!--<![endif]-->
    ```



> [[參考] Emmet語法大全（補充中）](https://alrin0000.blogspot.com/2014/05/emmet.html)