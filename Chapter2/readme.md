#### 在使用`<script>`嵌入JavaScript代码时，记住不要在代码中的任何地方出现"`<script>`"字符串。例如，浏览器在加载下面所示的代码时就会产生一个错误:
```html
<script>
    function sayScript() {
        alert("</script>");
    }
</script>
```
#### 因为按照解析嵌入式代码的规则，当浏览器遇到字符串"`<script>`"时，就会认为那是结束的`<script>`标签。而通过转义字符"\"解决这个问题，例如：
```html
<script>
    function sayScript() {
        alert("<\/script>");
    }
</script>
```

#### 需要注意的是，带有src属性的`<script>`元素不应该在其`<script>`和`</script>`标签之间再包含额外的JavaScript代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略。
#### 另外，通过`<script>`元素的src属性还可以包含外部域的JavaScript文件。（jsonp）
### 标签的位置
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Example HTML Page</title>
    </head>
    <body>
        <!-- 这里放内容 -->
        <script type="text/javascript" src="example1.js"></script>
        <script type="text/javascript" src="example2.js"></script>
    </body>
</html>
```

### defer属性
#### 这个属性的用途是表明脚本在执行时候不会影响页面的构造。也就是说，脚本会被延迟到整个页面都解析完毕后再运行。
#### HTML5规范要求脚本按照它们出现的现后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于DOMContentLoaded事件执行。在现实当中，延迟脚本并不一定按照顺序执行，也不一定会在DOMContendLoaded事件触发前执行，因此最好包含一个延迟脚本。([例子test1](./test1.html))

### async属性
#### 同样与defer类似，async只适用于外部脚本文件，标记为async的脚本并不保证按照指定它们的先后顺序执行。指定async属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。异步脚本一定会在页面的load事件前执行，但可能会在DOMContentLoaded事件触发之前或之后执行。([例子test2(./test2.html)])