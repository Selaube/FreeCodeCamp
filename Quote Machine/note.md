[Build a Random Quote Machine | FreeCodeCamp中文社区](https://freecodecamp.cn/challenges/build-a-random-quote-machine)

例：[Random Quote Machine](https://codepen.io/hezag/full/ZGxOLX/)

[TOC]

#### reference

- api 和 分享方法参考[随机格言生成器（Random Quote Machine）的制作 - 吟游诗人——吟唱生命的不朽 - CSDN博客](https://blog.csdn.net/qq_32623363/article/details/75187852)
- 句子api使用了[Hitokoto - 一言](https://hitokoto.cn/)
- 分享链接参考了 bilibili 分享视频时产生的链接，分享到微博的 appkey 也用了B站的。

#### 功能：

- 颜色：打开页面和更换时，随机生成一种亮度不太高的颜色，作为背景色、按钮背景色、引号颜色。因为使用的字体变成彩色效果不好，所以句子字体始终是黑色的。
- 分享按钮：为了线上显示方便，用 font-awesome 上相似的东西凑合了一下，眼睛图标分享到微博，星星分享到qq空间，鼠标移上去也有说明。分享页面会自动填入句子内容，qq空间会附带一言的链接。

#### 获取句子

按着一言api的说明和参考，一开始怎么试都获取不到，后来发现又是因为 Bootstrap 导入的 jquery.js 是 slim 版本导致的，**jquery.slim.js 不包括动画和 ajax 模块**，而 `getJSON()` 是属于 ajax 模块的。

```javascript
function getHitokoto() {
  $.get("https://v1.hitokoto.cn/", function (json) {
    sentence = json.hitokoto;
    author = json.from;
    var pattern = new RegExp("[A-Za-z]+");
    // 这个if解决句子过短时自动换行的问题。
    if (sentence.length < 20) {
      $("blockquote").css("white-space", "nowrap");
    } else if (sentence.length < 35 && pattern.test(sentence)) {
      $("blockquote").css("white-space", "nowrap");
    } else {
      $("blockquote").css("white-space", "normal");
    }
    $("#hitokoto").text(sentence);
    $("#from").text(" —— " + json.from);
  });
}
```

然而用 `getJSON()` 死活弄不到数据，用 `alert()` 输出的话显示的是 `[Object, Object]`，不知怎么回事，然后试着改用 `get()` 就能正确获取了。

另一个问题是因为将句子的容器设置了 `class="justify-content-center"` 属性，导致句子字数不多的时候也会换行，很别扭，所以增加了一个辨别字数的 `if` 语句，将字数小于一定程度的中文或英文设置为强制不换行。

#### 分享

分析一下分享页面的 url，然后把某些地方填进去，最后用 `window.open()` 方法打开一个新标签。每次获取的句子都存放在了变量里，这里就直接调用。

```javascript
$("#share2").click(function () {
  var link = "http://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url=https%3A%2F%2Fhitokoto.cn%2F&desc=" + sentence + " —— " + author + "&summary=我发现了一个好句子" + "&title=句子分享";
  window.open(link);
});
```

#### 按钮动态

这次没有使用 Bootstrap 的按钮样式，因为那个移动上去之后文字会变色，而需要的是放上去时按钮背景色变浅，所以增加了一个鼠标移入移出时透明度变化的效果。

```javascript
$(".tab").mouseover(function () {
  $(this).css("opacity", "0.8");
});
$(".tab").mouseout(function () {
  $(this).css("opacity", "1.0");
});
```

#### 随机颜色函数

颜色不能太浅，在 rgb 号的规律就是最小的值要小于一定的值，所以一个值是 0~120 的随机数，另外两个值是 0~255 的随机数，那个 0~120 的值放在哪个位置由一个 0~3 的随机数决定。

```javascript
function randomColor() {
  var c = Math.random() * 3;
  var color1 = Math.floor(Math.random() * 120);
  var color2 = Math.floor(Math.random() * 255);
  var color3 = Math.floor(Math.random() * 255);
  if (c < 1) {
    var rgbCode = "rgb(" + color1 + ", " + color2 + ", " + color3 + ")";
  } else if (c < 2) {
    var rgbCode = "rgb(" + color2 + ", " + color1 + ", " + color3 + ")";
  } else {
    var rgbCode = "rgb(" + color3 + ", " + color2 + ", " + color1 + ")";
  }
  return rgbCode;
}
```

