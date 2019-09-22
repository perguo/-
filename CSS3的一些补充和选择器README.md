# CSS-introduction
## 预处理器(pre-processor): less/sass, cssNext(插件)
### sass：按照它给定的一套语法规则来写代码，然后经过它的解析生成正常的CSS。虽然效率不高，但方便管理代码。
```
$font-stack: arail, ...;
$mysituation-color: #444;
div{
   span{
      color: $mysituation-color;
   }
   p{
      font: 100% $font-stack;
   }
}
```
  等价于
```
<div>
   <span style="color:#444"></span>
   <p style="font:arail"></p>
</div>
```
### cssNext举例
```
:root{
   --headLine-color: #333;
}
@custom-selector: --healine h1, h2, h3, h4, h5, h6;//把h1, h2, h3, h4, h5, h6打包成--healine
:--healine{
   color: var( --headLine-color );
}
```
  等价于
  ```
  h1,
  h2,
  h3,
  h4,
  h5,
  h6{
     color: #333;
  }
  
  ```

### cssNext: 是一个更加简练的less/sass，也可能是CSS4的发展方向。它用来实现一些未来的标准（未完全在各大浏览器实现的功能）


## 后处理器(post-processor): autoprefixed(插件)
  比如自动补全css在各大浏览器的兼容性问题：border-shadow:; --> border-shadow:;-mso-border-shadow:;
##  postCss: 一个工具，用js实现CSS的抽象`语法树`(AST: Abstract Syntax Tree)，剩下的事留给后人来做。
    cssNext和autoprefixer都是基于postCss来实现功能
### postCss + 插件（充分体现了扩展性，200多个）
* postCss + cssNext: 预处理器
* postCss + autoprefixer: 后处理器


# selector(选择器)
##  RelationShip Selectors: E+F E~F (`下一个`满足条件的`兄弟元素节点`)
```
<div>div</div>
<p>1</p>
<p>2</p>
<p>3</p>
<p>4</p>
div + p{/* 选择1，背景色变红色 */
            background-color: red;
        }

```

```
<div>div</div>
<span>0</span>
<p>1</p>
<p>2</p>
<p>3</p>
<p>4</p>

div ~ p{/* 选择1,2,3,4，背景色变红色 */
            background-color: red;
        }
```

##  Attribute Selector(属性选择器): E[attr~="var"](只有var或var+空格+其他的), E[attr|="val"(以var 开头或以-开头的); E[attr^="val"(以var 开头),E[attr&="val"(以var结尾),E[attr*="val"](含有var的)

##  Pseudo-Element Selector(伪元素选择器): E::placeholder(只能改颜色，wekit), E::selection(改变字体选中后的状态，只有3个能用：color,background-color,text-shadow)
  E::selection 鼠标选中字体的时候，字体的状态会发生改变
```
<div>努力</div>
<div>从来不只是说说而已</div>

div:nth-of-type(1)::selection{
           color: #fff;
           background-color: #7dd9ff;
       }
        div:nth-of-type(2)::selection{
            color: yellow;
            background-color: green;
        }
```

##  `Pseudo-Classes Selector`(伪类选择器):`被选中元素`的状态
### E:not(s), :root(根标签选择器，在html里：:root{}=html{}), E:target（目标，被锚点所标记）
  实现将除了最后一个，所有的li底部加上横线
```
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
</ul>

ul{
            border: 1px solid gray;
            width: 400px;
            padding: 0;
        }
        li{
            list-style: none;
            margin: 10px 0;
        }
       li:not(:last-of-type){
           border-bottom: 1px solid black;
       }
```
  点击box1时，1变的有边框；点击box2时，2变得有边框
```
<a href="#box1">box1</a>
<a href="#box2">box2</a>
<div id="box1">1</div>
<div id="box2">2</div>

div:target{
            border: 1px solid red;
        }
```
####  拓展题：三个按钮，点击不同的按钮，显示不同的背景色
```
<div class="buttonWrapper">
    <a href="#red">red</a>
    <a href="#green">green</a>
    <a href="#yellow">yellow</a>
</div>
<div id="red"></div>
<div id="green"></div>
<div id="yellow"></div>

:root,
        body{
            margin: 0;
            height: 100%;
        }
        div.buttonWrapper{
            position: absolute; /*让按钮飘起来，不占用位置*/
            top: 400px;
            width: 600px;
        }
        div.buttonWrapper a{
            text-decoration: none;
            color: #fff;
            font-size: 30px;
            background-color: blue;
            margin: 0 10px;
            border-radius: 20%;
        }
        #red,
        #green,
        #yellow{
            height: 100%;
            width: 100%;
        }
        #red{
            background-color: red;
        }
        #green{
            background-color: green;
        }
        #yellow{
            background-color: yellow;
        }
        div:empty:not(:target){
            display: none;
        }
        /*div[id]:not(:target){
            display: none;
        }*/
```


### E:first-child, E:last-child, E:only-child, E:nth-child(n), E:nth-last-child(n)
```
<div>
    <p>1</p>
    <p>2</p>
    <p>3</p>
</div>
<p>4</p>

 p:first-child{
            background-color: red;
        }
```
  1背景色为红色
```
<div>
    <span>0</span>
    <p>1</p>
    <p>2</p>
    <p>3</p>
</div>
<p>4</p>

 p:first-child{
            background-color: red;
        }
```
  没有被选中的
### `E:first-of-type, E:last-of-type, E:only-of-type, E:nth-of-type(n), E:nth-of-last-type`（倒着查）。(只看指定类型)
```
<div>
    <p>1</p>
    <p>2</p>
    <p>3</p>
</div>
<p>4</p>

 p:first-of-type{
            background-color: red;
        }
```
  1，4背景色为红色
  
```
<div>
    <span>0</span>
    <p>1</p>
    <p>2</p>
    <p>3</p>
    <p>4</p>
    <p>5</p>
</div>

 p:nth-of-type(2n+1){
            background-color: red;
        }
```
  1,3,5背景色为红色

### E:empty, E:checked, E:enabled, E:disabled, E:read-only, E:read-write
   checked. 实现被点击时，span中出现文字
```
<label>
    一个小惊喜
    <input type="checkbox">
    <span></span>
</label>

 input:checked + span{
           background-color: green;
       }
 input:checked +span::after{
           content: '全场一件九折，两件八折，三件七折';
           color: #fff;
       }
```






