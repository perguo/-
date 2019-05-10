# 高级标签-输入框
##  简单版：
```
<form method="get" action="">
    <p>
       用户名：<input type="text" name="username">
    </p>
    <p>
       密 &nbsp;&nbsp;码：<input type="password" name="password">
    </p>
<input type="submit">
</form>
```

##  实现输入框有默认值，且包含聚焦和失焦
```
<form method="get" action="">
    <p>
       用户名：<input type="text" name="username" value="请输入用户名"
                  onfocus="this.value==''"
                  onblur="this.value=='请输入用户名'">
<!--  name表示名称、value表示参数-->
    </p>
    <p>
       密 &nbsp;&nbsp;码：<input type="password" name="password">
    </p>
<input type="submit">
</form>
```

## 实现失焦后再次聚焦时输入内容不会改变
```
<form method="get" action="">
    <p>
       用户名：<input type="text" name="username" value="请输入用户名"
                  onfocus="if(this.value==''){this.value===''}"
                  onblur="if(this.value==''){this.value=='请输入用户名'}">
<!--  name表示名称、value表示参数-->
    </p>
    <p>
       密 &nbsp;&nbsp;码：<input type="password" name="password">
    </p>
<input type="submit">
</form>
```

# 选择框
##  单选框:radio
```
<form method="get">
        male:<input type="radio" name="sex" value="male">
        female:<input type="radio" name="sex" value="female">
</form>
```

### 添加默认选项：checked="checked"
```
<form method="get">
        male:<input type="radio" name="sex" value="male">
        female:<input type="radio" name="sex" value="female">
</form>
```

##  复选框
```
<form method="get">
        apple:<input type="checkbox" name="fruit" value="apple">
        banana:<input type="checkbox" name="fruit" value="banana">
        orange:<input type="checkbox" name="fruit" value="orange">
</form>
```

##  多选框：select包含内部表单，故只写一个name即可
```
    <form method="get">
        <select name="fruit">
            <option>苹果</option>
            <option>橙子</option>
            <option>芒果</option>
        </select>
    </form>
```
