##  vertical-align:-1px;调文字水平位置
##### ----------------------------------------------------------------------------------
##  white-space:nowrap;强制性换行
##### ----------------------------------------------------------------------------------
##  flex布局：`display:flex`;
### flex-direction（排列方向）: row | row-reverse | column | column-reverse  
### flex-wrap属性：在一条轴线上排不下时如何进行换行
#### flex-wrap: nowrap(默认，不换行) | wrap（换行，在第一行下方） | wrap-reverse（换行，在第一行上方）;
### `justify-content`属性:定义了项目在主轴上的对齐方式。
####   justify-content: flex-start(默认，左对齐) | flex-end（右对齐） | center（居中） | space-between（两端对齐，中间等间距） | space-around（项目两侧间距相等）;
### `align-items`属性定义项目在交叉轴上如何对齐。
####  align-items: flex-start(起点对齐) | flex-end（终点） | center（中点） | baseline（第一行文字的基线） | stretch（占满整个高度）
```
      display: flex;
      align-items: center;        /* 垂直居中 */
      justify-content: center;    /* 水平居中 */
```
