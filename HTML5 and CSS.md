[TOC]

# HTML5 and CSS

## 语法

### 注释

```html
<!--
中间的部分都是注释
-->
```

### 元素

元素是html中不同类型的东西，包括标题、段落、图片、列表等

大部分有开始和结束标记。`<element_name>xxxx</element_name>`

有的元素没有结束标记。`<element_name>`

### div（层）

div元素，也被称作division(层)元素，是一个盛装其他元素的通用容器。

所以可以利用CSS的继承关系把div上的CSS传递给它所有子元素。

```html
<div class="...">
    ...
</div>
```

### body

每一个 HTML 页面都有一个 body 元素。

通过在 style 中设置其 background-color，我们可以证明 body 元素的存在。

你可以像对其他 HTML 元素一样对你的 body 元素应用样式，并且所有其他元素将继承你的 body 元素的样式，它作用于整个页面。

```html
<style>
    body {
        background-color: black;
        color: green;
        font-family: Monospace;
    }
</style>
```

### 文字

#### 标题

`<h1>title</h1>`（一级标题，共有h1~h6）

#### 段落

`<p>paragraph</p>`

### 图片

`<img src="https://www.xxxx.xxx/.../xxx.jpg">`

图片不需要结束标记

#### alt属性

alt属性，也被称为alt text, 是当图片无法加载时显示的替代文本。alt属性对于盲人或视觉损伤的用户理解一幅图片中所描绘的内容非常重要，搜索引擎也会搜索alt属性。

`<img src="www.your-image-source.com/your-image.jpg" alt="your alt text">`

### 链接

a元素，也叫anchor（锚点）元素，既可以用来链接到外部地址实现页面跳转功能，也可以链接到当前页面的某部分实现内部导航功能。

#### 文本链接

```html
<p>Here's a 
    <a href="http://freecodecamp.cn">
        link to FreeCodeCamp
    </a>
    for you to follow.
</p>
```

#### 死链接

可以通过写为 `href="#"` 创建一个死链接，如果暂时不知道要链接到哪。

#### 图片链接

`<a href="#"><img src="/images/relaxing-cat.jpg"></a>`

### 列表

#### 无序列表

```html
<ul>
  <li>milk</li>
  <li>cheese</li>
</ul>
```

将会创建一个带项目符号（每项之前有个圆点之类的）的"milk"和"cheese"列表。

#### 有序列表

```html
<ol>
  <li>Garfield</li>
  <li>Sylvester</li>
</ol>
```

每项之前是数字编号。

### form表单

#### 输入框

`<input type="text">`

* 可以设置输入框内的默认内容：

`<input type="text" placeholder="this is placeholder text">`

* 可以设置某个输入框为必填项：

`<input type="text" required>`

#### 选择框

* 选择框是input输入框的另一种形式。每个选择按钮都必须嵌入 `<label></label>` 元素中

* 所有关联的单选或复选按钮应该使用相同的name属性。

* 可以设置某个选择按钮为默认选中，在input元素中添加checked属性：

  `<input type="radio" name="test-name" checked>`

##### 单选标签

`<label><input type="radio" name="indoor-outdoor"> Indoor</label>`

##### 复选标签

`<label><input type="checkbox" name="personality">Loving</label>`

#### 按钮

`<button type="submit">this button submits the form</button>` 这是一个提交按钮。

#### form

表单元素涵盖输入框、按钮等，它应该有个提交的action属性，指定表单提交的地址

```html
<form action="/submit-cat-photo">
    <input type="text" placeholder="cat photo URL">
    <button type="submit">Submit</button>
</form>
```

## Style/Class/ID

style是一个特殊的元素，其中规定了整个html的样式。

文字的style或class包括字体颜色、字体、字号等一系列属性，样式可以直接写在元素中，也可以将元素定义为一个类，这个类在css中做规定，或者从外界导入，那么所有该类的元素都会使用这一属性。但这些属性也可以进行覆盖。

也可以为元素赋予一个唯一的ID，这些元素可以在CSS中通过其ID被指定操作。

### 写法

#### 写在元素中

```html
<h2 style="color: red">title</h2>
<h3 class="blue-text">title</h3>
<form id="cat-photo-app">...</form>
```

#### 在CSS中定义

```html
<style>
    选择器 {
        属性名称: 属性值;
    }
    
    <!--元素选择器-->
    h2 {color: red;}
    
    <!--类选择器-->
    .blue-text {
        color: blue;
    }
    
    <!--ID选择器-->
    #cat-photo-element {
        backgound-color: green;
    }
</style>
```

css写在代码最顶端，后面要加分号。类选择器之前是“.”，ID选择器前加“#”不要空格

#### 从外界导入

下面是个例子，写在代码顶端，导入后可以调用其中的字体等

`<link href="https://fonts.gdgdocs.org/css?family=Lobster" rel="stylesheet" type="text/css">`

#### 覆写

有时元素的样式会冲突，这时会产生覆盖。

浏览器读取 CSS 的顺序是从上到下，这意味着，在发生冲突时，浏览器会使用最后的 CSS 声明。下面的程序如果没有 ID 属性，会显示为蓝色，因为蓝色类在 CSS 中更靠下。

但是并非只有这些，如果声明一个橙色的 ID 样式，最后会显示为橙色。你声明的这个 CSS 在 pink-text类选择器的上面还是下面是无所谓的，因为 id 属性总是具有更高的优先级。

```html
<style>
    body {
        background-color: black;
        font-family: Monospace;
        color: green;
    }
    .pink-text {
        color: pink;
    }
    .blue-text {
        color: blue;
    }
    #orange-text {
        color: orange;
    }
</style>

<h1 id="orange-text" class="pink-text blue-text">Hello World!</h1>
```

### 自定义属性

#### 字体

##### 直接在元素中写style

`<h2 style="color: red">title</h2>`

##### 在css中定义类，将元素添加为该类

```html
<style>
    .text1 {
        font-size: 20px;
        font-family: Monospace;
        color: orange;
    }
</style>
```

##### 备选字体（字体自动降级）

指定几种字体，当前面的字体不可用时使用后面的字体。如

```html
p {
    font-family: Helvetica, Sans-Serif;
}
```

#### 图片

##### 尺寸

CSS包含一个控制元素宽度的width属性（只有一个width）。像控制字体一样，我们使用px（像素）来指定图片的宽度。例如，如果我们想要创建一个名为larger-image的类选择器，把HTML元素的宽度设定为500像素，我们使用：

```html
<style>
  .larger-image {
    width: 500px;
  }
</style>
```

##### 圆角

和下面的边框圆角一样，只是添加到图像的类中。

#### 布局

所有的 HTML 元素本质上是小的矩形块，代表着某一小块区域。

有三个影响HTML元素布局的重要属性：padding(内边距)、margin(外边距)、border(边框)。

##### 边框

CSS 边框的属性有style(样式)、color(颜色)、width(宽度)、height(高度)等。举个例子，如果我们想要让一个HTML元素的边框颜色为红色、边框宽度为5像素(px)、边框样式为固体(solid)，代码如下:

```html
<style>
  .thin-red-border {
    border-color: red;
    border-width: 5px;
    border-style: solid;
  }
</style>
```

还可让边框变成圆角，添加 `border-radius: 10px;` 或 `border-radius: 50%` 属性，可以添加在边框类如 `.thin-red-border` 中，也可以添加在图像类如 `.smaller-image` 中。

##### 内边距

元素的 padding 控制元素内容 content 和元素边框 border 之间的距离。

CSS 允许你使用 padding-top、padding-right、padding-bottom 和 padding-left来控制元素上右下左四个方向的 padding。也可以写为一行，顺序是顺时针，上右下左，空格分开。

```html
<style>
    .green-box {
        background-color: green;
        padding-top: 40px;
        padding-bottom: 20px;
        padding-left: 40px;
        padding-right: 20px;
    }
    .yellow-box {
        background-color: yellow;
        padding: 20px 40px 20px 40px;
    }
</style>
```

##### 外边距

元素的外边距 margin 控制元素边框 border 和元素实际所占空间的距离。如果你将一个元素的 margin 设置为负值，元素将会变大，直至将父容器的横向宽度填满。

也可用 margin-top、margin-right、margin-bottom 和 margin-left 来控制元素上右下左四个方向的 margin，或者按上右下左的顺序写为一行。

```html
<style>
    .green-box {
        background-color: green;
        padding: 20px;
        margin: -15px;
    }
    .red-box {
        background-color: red;
        margin-top: 40px;
        margin-right: 20px;
        margin-bottom: 20px;
        margin-left: 40px;
    }
    .yellow-box {
        background-color: yellow;
        margin: 20px 30px 20px 30px;
    }
</style>
```

#### 层

`<div>...</div>` 中间包裹的元素都会继承层的样式。层也可以像上面一样设置颜色、

```html
<style>
    .green-background {
        background-color: green;
    }
</style>

<div class="gray-background">
    ...
</div>
```

#### 颜色

```html
<style>
    body {
        background-color: red;
    }
    body {
        background-color: #FF0000;
    }
    body {
        background-color: #F00;
    }
    body {
        background-color: rgb(255,0,0);
    }
</style>
```

##### 单词表示

包括red、blue、green、black、gray、white、orange、brown等

##### 十六进制编码

在CSS中，我们可以使用6位十六进制数字来表示颜色，每2位分别表示红色(R)、绿色(G)和蓝色(B)成分。例如#000000是黑色，#FFFFFF是白色，#FF0000、#00FF00、#0000FF是红、绿、蓝，灰色可以是#808080。

也可以缩写为3位十六进制，每一位分别表示R、G、B，如#FF0000可缩写为#F00

##### RGB

写为 `rgb(0~255, 0~255, 0~255)`