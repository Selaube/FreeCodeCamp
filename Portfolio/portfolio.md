### Build a Personal Portfolio Webpage

* [项目说明](https://freecodecamp.cn/challenges/build-a-personal-portfolio-webpage)
* [示例](https://codepen.io/freeCodeCamp/full/YqLyXB/)

*日期：2019-03-18*

[TOC]

#### 分析

##### Layout

* 顶部：导航栏
  * 左头像？，鼠标移到上面显示一行字
  * 右三个标签的导航按钮，点击跳转到页内相应位置
* 中部：分为三块，每块边缘都有阴影效果，从上到下：
  * 左侧是能力介绍和职业，右侧是一张照片及说明
  * 标题 portfolio，放作品集
  * 标题 contact me。下方左侧是四个输入文本的表单，有“send”按钮。右侧是一段文字说明
* 底部 1：署名和其他页面链接，有网站对应的图标
* 底部 2

##### 目标

* 可以通过滚动来浏览这个页面的所有内容
* 可以通过点击不同的按钮来跳到不同的社交媒体页
* 可以看到不同项目的缩略图
* 可以点击导航条上的按钮来调到网页上的不同区域
* 可以填写和发送表单

#### 组件

##### container、row、col

container 容纳一个区域，row 和 col 要在这个区域内分割出更小的块。也就是一个 `<div class="container">` 是二者的前置父元素。

col 的上一层不一定是 row，二者没有先后关系。可以将 col 放在 row 里，也可以反过来，不过问题是 row 不像 col 可以通过 class 定义宽度，也就是一个放置在 col 内的 row 宽度等于 col，高度取决于其内容。

可以使用如 `<div class="col-6 offset-3 offset-3"> 定义一个居中的 col（父级元素的宽度为 12），两个 offset 分别指定了自左和自右侧的偏移网格数，第二个 offset 保证了这个 col 右侧的边界。

一个典型的网格布局如：

```html
<div class="container">
  <div class="row">
    <div class="col-4">
      #
    </div>
    <div class="col-8">
      #
    </div>
  </div>
</div>
```

##### navs、navbar

顶部的导航栏元素。`navs` 可以作为指向某个元素位置的按钮，基本形式为：

`<a class="nav-link" href="#">Link</a>`

其中 `href` 指向一个元素的 ID

有几种风格，参见 Bootstrap 文档。可以使用 `navbar` 组合成一个导航栏。这个导航栏的三个按钮靠右对齐，左侧是个图片，作为这个导航栏的 `navbar-brand`

其中 `fixed-top` 类将 navbar 固定在页面顶部。这会遮挡最前面的内容，所以需要为其设置一个高度，并将 body 下移这个高度，见下文的"body"部分

`body style="margin-top"

```html
<nav class="navbar fixed-top" style="background-color: rgb(0, 85, 140); height: 60px; box-shadow: 0px 0px 10px 0px">
  <a class="navbar-brand"><img src="#" alt="gh | web development" title="gh | web development"></a>
  <ul class="nav nav-pills justify-content-end">
    <li class="nav-item">
      <a class="nav-link active" href="#">About</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Portfolio</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Contact</a>
    </li>
  </ul>
</nav>
```

##### card

用来展示作品。下面的代码构成了一个 card，包括图片、标题、介绍。点击图片可以跳转页面。因为直接从页面生成缩略图需要"生成快照"，所以目前必须准备作品的图片。

```html
<div class="card">
  <a herf="#"><img src="#" class="card-img-top" alt="#"></a>
  <div class="card-body">
    <h5 class="card-title">card title</h5>
    <p class="card-text">
      this is the introduction of the work
    </p>
  </div>
</div>
```

##### form

下面的表单包含三个文本输入框，分别输入名字、email、备注，其中 email 框下面有一行小字：我不会泄露您的 email 给别人。最下面是个“提交按钮”，可以发送表单信息（待完成）

```html
<form>
  <div class="form-group">
    <label for="inputName">Name</label>
    <input type="text" class="form-control" id="inputName" placeholder="What should I call you?">
  </div>
  <div class="form-group">
    <label for="inputEmail">Email</label>
    <input type="email" class="form-control" id="inputEmail" aria-describedby="emailHelp"
      placeholder="Enter your email.">
    <small id="emailHelp" class="form-text">I'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="inputRemarks">Rmarks</label>
    <input type="text" class="form-control" id="inputRemarks" placeholder="Anything else want to tell me?">
  </div>
  <button type="submit" class="btn btn-primary">Send</button>
</form>
```

##### icons

使用 font awesome 图标，在 headers 中导入并调用，做成图标链接

```html
<header>
  <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.7.2/css/all.css"
    integrity="sha384-fnmOCqbTlWIlj8LyTjo7mOUStjsKC4pOpQbqyi7RrhN7udi9RwhKkMHpvLbHG9Sr" crossorigin="anonymous">
</header>

<ul>
  <li>
    <a herf="https://github.com/Selaube"><i class="fab fa-github"></i></a>
  </li>
  <li>
    <a herf="#"><i class="fab fa-alipay"></i></a>
  </li>
  <li>
    <a herf="https://freecodecamp.cn/selaube"><i class="fab fa-free-code-camp"></i></a>
  </li>
  <li>
    <a herf="#"><i class="fab fa-weibo"></i></a>
  </li>
</ul>
```

##### div 阴影

样本中的每个 div 边缘处都有阴影效果，形成了立体感。可以使用 div 阴影做到。在 header 中增加 style 或设置元素中的 style 如：

```html
<div class="row p-5 bg-white" style="box-shadow: 0px 0px 10px 0px">a</div>
```

这样生成的阴影层次是由该 div 所在的层次决定的，有时需要改变阴影的层次，就需要改变这个元素在 style 中的层次（参考：[[Chuan's blog - CSS: 用box-shadow实现相邻div的阴影效果](http://blog.shaochuancs.com/css-box-shadow/)）：

```html
<div class="row p-5 bg-white" style="box-shadow: 0px 0px 10px 0px;
                                     z-index: 3; position: relative">a</div>
```

其中 `z-index` 是层次序号，越大越靠上，它只在 position 值为 absolute、relative 或 fixed 的情况下才起作用

##### body

因为示例页面有个背景色，于是将背景色设置在了 container 中，结果 footer 下面总有一点空白。后来发现将背景色设置写在 body 里就可以了，这时 footer 宽了一些，盖住了这点空白。

另外将 body 下移一个高度，避免被固定在顶部的导航栏挡住。

`<body style="background-color: #333; margin-top: 60px>"`

##### 跳转偏移

点击一个 nav 按钮跳转的位置比该元素的实际位置偏低，以至于该元素顶部的一部分跑到了屏幕外。可以通过改变其锚点的位置解决这个问题。跳转时也是跳转到锚点的 ID，而不是跳到元素的 ID。例：

```html
<div class="row p-5 bg-white" style="box-shadow: 0px 0px 10px 0px">
  <a id="portfolio-part" style="position: relative; top: -100px"></a>
</div>
```

##### 导航栏随页面滚动

一开始遇到了以下的问题：

使用 Bootstrap 的 navs 时，像 navbar 的 class 中添加 pills 属性可以让按钮在被点击后变色。为了达到这个效果，还要在每个 nav 中添加 toggle 属性，这样每点下一个按钮就会变色。

然而这时，点击按钮就无法跳转到指定位置，只能变色。这个问题难以解决，于是舍弃了这个效果。

后来在 Bootstrap 文档中看到了 [scrollspy](https://getbootstrap.com/docs/4.3/components/scrollspy/)，试了之后发现应该用它解决问题。具体做法类似该页面中“Example in navbar”的示例，将 `data-spy="scroll" data-target="#navbar-example2" data-offset="0"` 的属性添加到 body，并将 data-target 指向 navbar 的 id。

