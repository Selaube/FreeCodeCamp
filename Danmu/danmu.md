FreeCodeCamp 的 design a danmu app 项目。

- 项目说明：[Design a danmu app | FreeCodeCamp中文社区](https://freecodecamp.cn/challenges/design-a-danmu-app)
- 示例：[A Pen by FCC](https://codepen.io/huluoyang/full/GZbBwL/)

分两个版本，一个一次只发送一条弹幕，另一个每发送一次，会重复发送多条。

[TOC]

**目标**

- 一个用来盛放弹幕的框
- 输入框，输入弹幕
- 发射和清屏按钮
- 不容颜色的弹幕从框的右侧随机高度出现，匀速运动到左端消失
- 弹幕在一段随机的时间内随机发射若干次

#### 页面

##### 弹幕区

使用一个带边框的 div 或 span

```html
<div class="container-fluid">
  <div id="pool" class="row m-3 p-2 border"></div>
</div>
```

##### 样式

```html
<style>
  .danmu {
    position: absolute;
    font: SimHei;
    font-weight: 550;
    left: 100%;
    white-space: nowrap;
  }
  #pool {
    position: relative;
    height: 400px;
    overflow: hidden;
  }
</style>
```

pool 的固定高度令其产生空白区域，overflow 属性表示其子元素在超出它的边界时是否隐藏，设为 hidden 可以做到弹幕从这个区域中出入的效果。

danmu 类用于每条弹幕，字体和粗细固定，距父元素（pool）左端的距离为 100%，也就是弹幕初始位置的最左端与 pool 的最右端对其，正好处于区域外。white-space 属性指定了禁止换行，否则弹幕在处于 pool 的边缘时会换行来适应这个宽度。

##### 表单区

一个 input 两个 button。后来发现在文本框里按回车会导致页面刷新，所以后来改用 div 代替。

```html
  <div class="form-row mx-5">
    <input id="input" type="text" class="form-control form-control-sm" placeholder="说点什么？">
  </div>
  <div class="form-row my-3 mx-5">
    <div class="col ml-5">
      <button id="btn-fire" type="button" class="btn btn-sm btn-outline-danger btn-block">发射</button>
    </div>
    <div class="col mr-5">
      <button id="btn-clear" type="button" class="btn btn-sm btn-outline-secondary btn-block">清屏</button>
    </div>
  </div>
```

#### 脚本

使用 jQuery，Bootstrap 文档中给出的“hello world”模板中已经导入了 jQuery 库，`<script>` 就写在导入的下面：

```html
<script>
    $(document).ready(function(){
        jQuery语句
    });
</script>
```

然而，后来在添加 jquery 动画的时候死活不动，最后发现 Bootstrap 导入的 jquery.js 是 jquery.slim.min.js，这个版本不包括动画效果，应该使用 jquery.min.js，于是重新导入了一个。地址可以到官网上右键下载链接，选择“复制链接地址”，就可以获取文件的 src 了。

注：这里发射、清屏、文本框、弹幕框 id 分别为 btn-fire、btn-clear、input、pool，弹幕的 class 为 danmu。

##### 发射按钮

当按下发射时，清空输入框并将其中的文字变成弹幕发送。按钮事件通过 `.click()` 事件触发。

`danmuFire()` 函数的功能是清空输入框并发射弹幕。

```javascript
$("#btn-fire").click(function(){
    danmuFire();
});
```

##### 清屏按钮

```javascript
// 获取pool的html内容放入这个变量，之后重置pool的html就清屏了
var poolHtml = $("#pool").html();

$("#btn-clear").click(function () {
  $("#pool").html(poolHtml);
  danmuCount = 0;
});
```

##### 输入框

在输入框中按下回车的话，也会发射弹幕（输入框不为空）并清空输入框。

- [event.which 的用法](http://www.w3school.com.cn/tiy/t.asp?f=jquery_event_which)

`event.which` 是"事件中按了哪个键"，回车的 id=13。

```javascript
$("#input").keydown(function (event) {
  // 在文本框回车，清空并发射弹幕
  if (event.which == 13) {
    danmuFire();
  }
});
```

##### 单条弹幕

这个页面写了两个版本，danmu.html 每次只发送一条弹幕，danmu_loop.html 每次发送弹幕是在一定的时间内以一定间隔发射多个弹幕，单条弹幕的行为是一样的。

```javascript
function oneDanmu(danmu) {
  // 生成随机的颜色、高度、字体大小
  var randomColor = "#" + Math.floor(Math.random() * 1000);
  var randomTop = Math.floor(Math.random() * 350);
  var randomFontsize = Math.floor(Math.random() * 10) + 15;
  // 向pool中放入弹幕
  var styleCss = "style='color: " + randomColor + "; top: " + randomTop + "px; font-size: " + randomFontsize + "px'";
  var id = "danmu" + danmuCount;
  danmuCount++;
  var danmuHtml = "<div class='danmu' " + styleCss + "id='" + id + "'>" + danmu + "</div>";
  $("#pool").append(danmuHtml);
  // 距离是pool的宽度+弹幕的宽度+一个常量，正好能使不同长度的弹幕到pool的左侧以外
  // -=表示从起始位置向左运动一个值，详见animate()的用法
  var distance = "-=" + ($("#pool").width() + $("#" + id).width() + 20) + "px";
  $("#" + id).animate({ left: distance }, 10000, "linear");
}
```

其中，id 根据一个定义在函数之外的数字 `var danmuCount = 0;` 得到，对每条弹幕都是唯一的，每生成一条弹幕就会+1，直到按下了“清屏”按钮，这个数字会被重置。

这个数字也相当于网页中总的弹幕数量，弹幕最后实际都停留在了 pool 的外侧而没有消失，直到清屏。

##### 发射弹幕

```javascript
function danmuFire(danmu) {
  var danmu = $("#input").val();
  oneDanmu(danmu);
  $("#input").val("");
}
```

这是单发版本的函数，每当触发了“发送弹幕”，就会从输入框中获取文本，然后清空输入框。将获取的弹幕传入 oneDanmu，发射一条弹幕。

#### 循环版本

##### 单重循环

- [Window setInterval() 方法 | 菜鸟教程](http://www.runoob.com/jsref/met-win-setInterval.html)
- [Window clearInterval() 方法 | 菜鸟教程](http://www.runoob.com/jsref/met-win-clearinterval.html)
- [Window setTimeout() 方法 | 菜鸟教程](http://www.runoob.com/jsref/met-win-settimeout.html)

```javascript
intervalVar = setInterval(function(){
    oneDanmu(danmu);
}, randomTime(2, 4));
setTimeout(function(){
    clearInterval(intervalVar);
}, 10000); // 计时10秒停止循环

// 生成a~b秒的随机时间
function randomTime(a, b) {
    return (Math.floor(Math.random() * (b - a)) + a) * 1000;
}
```

上面的代码是一个模板。

以 2~4 秒的随机时间间隔，重复执行 oneDanmu 发送弹幕。这个函数需要用 `clearInterval()` 停止，停止函数设置为一段时间后执行。为了使用停止函数，intervalVar 设置为一个全局变量（前面不加 var）

`setInterval()` 中的回调函数调用的 `oneDanmu` 使用了参数 `danmu`，但并不需要传参。因为这是个“匿名函数”，它的作用是执行其中的语句。

##### 多重循环

但遇到了一些问题：

发射弹幕的事件不会只触发一次，也就是会同时存在多个 interval 过程。那么就需要为每个 interval 过程准备一个变量名，代替这里的 intervalVar，需要使用动态变量名命名的方法，也就是使用数组。如果这样，就要有个指针为每次定义的 interval 过程指定一个 index。

```javascript
var fireCount = 0;
intervalArr = []; // 一个全局变量数组
function danmuFire(danmu) {
    ...
    intervalArr[fireCount] = setInterval(function() {
        oneDanmu(danmu);
    }, randomTime(2, 4));
    setTimeout(function () {
        clearInterval(intervalArr.shift());
        fireCount--;
    }, 10000);
    fireCount++;
    ...
}
```

上面的是这个函数的最终版本，中途也遇到了另外的问题，主要是指针的增减。

当增加了一个 interval 过程，arr 中就会相应的增加一个值，同时指针向后移动 1；当一个过程消失时，最前面的那个过程就会被取出来停止掉，最后面的指针向前移动一位

因为必须确定每次被停止的过程都是序列中最先发生的，所以要求 setTimeout 的时间必须是个固定的值，这样每个过程的倒计时才能按顺序完成（一开始打算做成随机的时长）

##### 清屏

[JavaScript forEach() 方法 | 菜鸟教程](http://www.runoob.com/jsref/jsref-foreach.html)

上面的方法用来为数组中每个对象执行相同的函数，注意括号中的函数名是不加括号的。`clearInterval()` 会将每个对象（interval 过程）停止，并将其消除，所以对整个 arr 执行完后 arr 自动就空了。

```javascript
$("#btn-clear").click(function () {
    $("#pool").html(poolHtml);
    intervalArr.forEach(clearInterval);
    danmuCount = 0;
    fireCount = 0;
});
```

