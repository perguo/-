##  第一种margin的BUG
```
<div class="wrap">
    <div class="content"></div>
</div>

        .wrap{
            width: 100px;
            height: 100px;
            background-color: black;
            margin-left: 100px;
            margin-top: 100px;
        }
        .content{
            width: 50px;
            height: 50px;
            background-color: red;
            margin-left: 50px;
            margin-top: 50px;
        }
```
### 此时`margin-top: 50px;`并不能显示效果。这就是margin的塌陷问题，子类的margin在垂直方向会出bug。 只有当子类的垂直方向的margin值大于父类时，才能挪动位置，但，却是父类随子类一起挪动

##  解决方法：BFC(block format context),块级格式化上下文
### 原理：让渲染规则发生改变。特定的盒子会遵循另一套语法规则。
### 如何触发一个盒子的bfc：
    position:absolute;
    display:inline-block;
    float:left/right;
    overflow:hidden;
### 第一种解决方案：添加overflow:hidden;改变父级渲染规则，让父级变成BFC
```
.wrap{
            width: 100px;
            height: 100px;
            background-color: black;
            margin-left: 100px;
            margin-top: 100px;
            overflow:hidden;
        }
 ```
 ### 第二种解决方案：添加display:inline-block;改变父级渲染规则，让父级变成BFC
```
.wrap{
            width: 100px;
            height: 100px;
            background-color: black;
            margin-left: 100px;
            margin-top: 100px;
            display:inline-block;
        }
 ```
 ### 第三种解决方案：添加opsition:absolute;改变父级渲染规则，让父级变成BFC
```
.wrap{
            width: 100px;
            height: 100px;
            background-color: black;
            margin-left: 100px;
            margin-top: 100px;
            opsition:absolute;
        }
 ```
 
 ##  第二种margin的BUG
 ```
 <div class="demo1">1</div>
<div class="demo2">2</div>

.demo1{
            background-color: red;
            margin-bottom: 100px;
        }
        .demo2{
            background-color: green;
            margin-top: 100px;
        }
```
####  页面效果只显示一个margin的值
####  解决方案:(一般情况不推荐)
```
<div class="div">
    <div class="demo1">1</div>
    <div class="demo2">2</div>
</div>
 .div{
         overflow: hidden;
     }
 ```
 ## 浮动float
 #### 浮动元素产生了浮动流
 #### 所有产生浮动流的元素，块级元素看不到他们
 #### 产生了bfc的元素和文本类属性(inline)的元素以及文本都能看到浮动元素
 #### 清除浮动流：clear:left/right/both;
 
 
 #  CSS要点补充说明
 ## 对于行级元素，如：span，不能设置宽高。但当加上'position:absolute'或者'float:left/right'时，宽高就可以设置了。
 ## 这是因为：'position:absolute'和'float:left/right'一旦加上，就将布局改为了'display:inline-block'。
 
