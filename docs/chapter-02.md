# 第二章 在HTML中使用JavaScript

## script元素的属性

- charset：可选。指定代码的编码集，可是大多数浏览器会忽略它，这个属性很少人用

- src：可选。表示执行代码的外部文件路径

- type：可选。指定脚本的内容类型（也称MIME类型），该属性的默认值是 `text/javascript` 。实际上，服务器在传输JS时所用的MIME类型通常是 `application/x-javascript` ，在type设置自定义值可能会被忽略

- defer：可选。只适用于外部脚本文件，表示脚本会被延迟到整个页面都解析完毕后再运行，该属性只对外部引入的脚本文件有效。相当于告诉浏览器立即加载该脚本，但延迟到`</html>`之后执行；HTML5规范要求脚本按照它们出现的先后顺序执行。<u>在现实当中，延迟脚本并不会按照顺序执行，也不会在`DOMContentLoaded`事件触发之前执行，因此最好一个页面包含一个延迟脚本</u>(这个说法暂时测试没出现，留下个疑问)

- async：可选。只适用于外部脚本文件，表示多个脚本异步加载，即不保证按照指定的脚本顺序执行。故在设置该属性时，脚本之间互不依赖是非常重要的。
指定`async`属性的目的是不让页面等待这几个脚本的下载和执行，从而异步加载页面其他内容。为此，建议异步脚本中不要在加载期间修改`DOM` 。

## 标签的位置

大多数新手总会把`script`标签放在`</head>`的前面，如下所示：

```html
<!doctype html>
 <html lang="zh-CN">
 <head>
     <meta charset="UTF-8">
     <meta http-equiv="X-UA-Compatible" content="ie=edge">
     <title>Document</title>
     <script src="first.js"></script>
     <script src="second.js"></script>
     <script src="third.js"></script>
 </head>
 <body>
        ...
 </body>
 </html>
 ```
 这样将会导致页面在加载完 `</head>` 前面的所有JS文件后才能呈现页面（加载body标签里面的内容）。对于那些需要很多JS代码的页面来说，这无疑会导致浏览器在呈现页面时出现明显的延迟，而延迟期间浏览器窗口将会一片 **空白** 
 。想想用户要等待一段时间才能看到页面，这将是一件多么糟糕的事情。
 
 为了避免这个问题，现代web应用程序一般都把全部JS引用放在`</body>`标签的前面，如下所示：
 
 ```html
 <!doctype html>
  <html lang="zh-CN">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
  </head>
  <body>
         ...
         <script src="first.js"></script>
         <script src="second.js"></script>
         <script src="third.js"></script>
  </body>
  </html>
 ```
 
 ## 文档模式
 
 - 混杂模式：页面以一种宽松的向后兼容的方式显示，其通常模拟老式浏览器的行为以防止老站点无法工作
 - 标准模式：浏览器以其支持的最高标准呈现页面
 
 如果在文档开始处没有发现文档类型声明或文档类型声明不正确，则所有浏览器都会默认开启混杂模式
 
 如果XHTML、HTML4.01文档包含形式完整的DOCTYPE，那么它一般以标准模式呈现
 
 包含过渡DTD和URI的DOCTYPE页面以标准模式呈现，但是有过渡DTD而没有URI会导致页面以混杂模式呈现
 
 ## `<noscript>` 元素
 
 - 用于在不支持JS的浏览器或脚本被禁用的情况下显示替代的内容
 
 - 这个元素可以出现在文档`<body>`中的任何HTML元素（非`<script>`元素）
 
 如下所示：
 
 ```html
 <!doctype html>
 <html lang="zh-CN">
 <head>
     <meta charset="UTF-8">
     <meta http-equiv="X-UA-Compatible" content="ie=edge">
     <title>Document</title>
 </head>
 <body>
     <noscript>本页面需要浏览器支持，请启用JavaScript</noscript>
     <script src="first.js"></script>
     <script src="second.js"></script>
     <script src="thrid.js"></script>
 </body>
 </html>
 ```
