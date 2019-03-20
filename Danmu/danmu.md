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

一个 input 两个 button

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

##### 发射按钮

##### 清屏按钮

##### 弹幕