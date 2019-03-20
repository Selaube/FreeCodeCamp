FreeCodeCamp 的 design a danmu app 项目。

- 项目说明：[Design a danmu app | FreeCodeCamp中文社区](https://freecodecamp.cn/challenges/design-a-danmu-app)
- 示例：[A Pen by FCC](https://codepen.io/huluoyang/full/GZbBwL/)

[TOC]

#### 功能

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
  <div class="row m-3 border">
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
  </div>
  <form class="col-4 offset-4 offset-4">
  </form>
</div>
```

##### 表单区

一个 input 两个 button。后来发现在文本框里按回车会导致页面刷新，所以后来改用 div 代替。

```html
<form class="col-4 offset-4 offset-4">
  <div class="form-row">
    <input type="text" class="form-control form-control-sm" placeholder="说点什么？">
  </div>
  <div class="form-row m-3">
    <div class="col-6">
      <button type="button" class="btn btn-sm btn-outline-danger btn-block">发射</button>
    </div>
    <div class="col-6">
      <button type="button" class="btn btn-sm btn-outline-secondary btn-block">清屏</button>
    </div>
  </div>
</form>
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

注：这里发射、清屏、文本框、弹幕框 id 分别为 btn-fire、btn-clear、input、pool

##### 发射按钮

当按下发射时，清空输入框并将其中的文字变成弹幕发送。按钮事件通过 `.click()` 事件触发，可以使用 `$("#input").val()` 获取弹幕内容

```javascript
$("#btn-fire").click(function(){
    var danmu = $("#input").val();
});
```

##### 清屏按钮

按钮原理同上。停止这个过程并清除所有弹幕。

##### 输入框

在输入框中按下回车的话，也会发射弹幕（输入框不为空）并清空输入框。

- [event.which 的用法](http://www.w3school.com.cn/tiy/t.asp?f=jquery_event_which)

##### 弹幕

当触发"发射弹幕"事件，在弹幕区（div）的右侧生成一条随机高度、随机色彩的弹幕，并以某个速度向左移动，直到弹幕区的左侧（示例是一直出了网页），这个过程持续一个随机的时间，因此需要一个计时

当点击“清屏”，停止这个过程并清除所有弹幕。

##### 随机计时

- `setTimeout()` 未来的某时执行代码
- `clearTimeout()` 取消setTimeout()