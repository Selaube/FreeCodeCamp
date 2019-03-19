[TOC]

## JavaScript

### 语法

#### 注释

```javascript
// commment

/*
comment
*/
```

#### 大小写

在 JavaScript 中所有的变量都是大小写敏感的。这意味着你要区别对待大写字母和小写字母。

`MYVAR` 与 `MyVar` 和 `myvar` 是截然不同的变量。这就有可能导致多个截然不同的变量却有着有相似的名字。所以强烈地建议你, *不要*使用这一特性。（以免给自己带来麻烦）

使用**驼峰命名法**来书写一个 Javascript 变量，在**驼峰命名法**中，变量名的第一个单词的首写字母小写，后面的单词的第一个字母大写。

```javascript
var someVariable;
var anotherVariableName;
var thisVariableNameIsTooLong;
```

#### 输出

`console.log();` 相当于 `print()`

#### 正则表达式

可以参考 [正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

`Regular expressions` 正则表达式被用来根据某种匹配模式来寻找 `strings` 中的某些单词。

* 如果我们想要找到字符串`The dog chased the cat` 中单词 `the`，我们可以使用下面的正则表达式: `/the/gi`。我们可以把这个正则表达式分成几段：
  * `/` 是这个正则表达式的头部
  * `the` 是我们想要匹配的模式
  * `/` 是这个正则表达式的尾部
  * `g` 代表着 `global`(全局)，意味着返回所有的匹配而不仅仅是第一个。
  * `i` 代表着忽略大小写，意思是当我们寻找匹配的字符串的时候忽略掉字母的大小写。

##### 匹配字符串

使用了 `String.match(str)` 函数

```javascript
var expression = /and/gi;

// 用 andCount 存储 testString 中匹配到 expression 的次数
var andCount = testString.match(expression).length;
```

##### 匹配数字

我们可以在正则表达式中使用特殊选择器来选取特殊类型的值。特殊选择器中的一种就是数字选择器`\d`，意思是被用来获取一个字符串的数字。

在JavaScript中, 数字选择器类似于: `/\d/g`。在选择器后面添加一个加号标记(`+`)，例如：`/\d+/g`，它允许这个正则表达式匹配一个或更多数字。

尾部的 `g` 是'global'的简写，意思是允许这个正则表达式找到所有的匹配而不是仅仅找到第一个匹配。

##### 空白、非空白字符

* 我们也可以使用正则表达式选择器 `\s` 来选择一个字符串中的空白。

  空白字符有 `" "` (空格符)、`\r` (回车符)、`\n` (换行符)、`\t` (制表符) 和 `\f`(换页符)。

  空白正则表达式类似于：`/\s+/g` 

* 你可以用正则表达式选择器的大写版本 来转化任何匹配。

  举个例子：`\s` 匹配任何空白字符，`\S` 匹配任何非空白字符。

### 变量

#### 七种类型

JavaScript提供七种不同的data types(数据类型)，它们是 `undefined`（未定义）, `null`（空）, `boolean`（布尔型）, `string`（字符串）, `symbol`(符号), `number`（数字）, and `object`（对象）。

`Variable` （变量）的名字可以由数字、字母、`$` 或者 `_` 组成，但是不能包含空格或者以数字为首。

#### 定义与初始化

如果不给变量赋值，它就是 `undefined`，运行可能出错。

```javascript
var ourName;
ourName = "Tom";

var ourName = "Tom";

var hisName = "Tom";
var ourName = hisName;
```

#### 运算符

| 符号           | 含义                                 |
| -------------- | ------------------------------------ |
| +              | 加、连接字符串、连接字符串和数字     |
| -              | 减                                   |
| *              | 乘，不能运算字符串                   |
| /              | 除                                   |
| %              | 取余数                               |
| ++、--         | 自增、自减 1                         |
| +=、-=、*=、/= | a += b => a = a + b，+= 能操作字符串 |
| ==、!=         | 相等、不等                           |
| ===、!==       | 不光值相等，变量类型也相等           |
| \>=、<=        | 大于等于、小于等于                   |

#### 字符串

`var str = "This is a string.";`

##### 转义

```javascript
\'（单引号），\"（双引号），\\（反斜杠），\n（换行）
\r（回车），\t（制表符），\b（退格），\f（换页符）

example:
var str = 'That\'s a dog\n';
```

##### 长度

`var lenStr = lastName.length`

##### 索引

可以通过 `str[index]` 获取字符串中某个序号上得字符，从 `[0]` 开始

```javascript
var firstName = "Charles";
var firstChar = firstName[0]; // firstChar = "C"
```

但是获取倒数的字符不能使用如 `str[-1]`，返回的是 `undefined`。而是使用 `str[str.length - 1]`

另外，JavaScript 没有索引切片（数组索引一个范围内的值时有对应的函数）。

当然，也没有格式化输出。

##### 不可变性

在 JavaScript 中，`字符串` 的值是 不可变的，这意味着一旦字符串被创建就不能被改变。例如：

```javascript
var myStr = "Bob";
myStr[0] = "J";
```

是不会把变量 `myStr` 的值改变成 "Job" 的，因为变量 `myStr` 是不可变的。注意，这 *并不* 意味着 `myStr` 永远不能被改变，只是字符串字面量 string literal 的各个字符不能被改变。改变 `myStr` 中的唯一方法是重新给它赋一个值，就像这样：

```javascript
var myStr = "Bob";
myStr = "Job";
```

##### str.split()

按指定方法将字符串分割为数组。参数一般是个字符，将按这个字符分割字符串，返回一个数组。

```javascript
var string = "Split me into an array";
var array = string.split(" ");
// array = ["Split", "me", "into", "an", "array"];
```

#### 数组

数组可以存储多个值，每个值可以是不同类型的变量，也可以定义多维数组，并通过索引访问

```javascript
var arr1 = [1, 2, 4];
var arr2 = ["dog", 3];
var arr3 = ["money", "car", "house"];
var arr4 = [["cat", 2], [5, "apple"]];
var arr5 = [arr1, arr2];
```

##### 索引

同样的，数组的索引也不能 `arr[-1]` 或 `arr[0: 2]`，后者有相应的函数

数组与字符串不同，是可变的，可以指定改变某个序号上的值，如

```javascript
var arr = [1, 4, 5, 7];
arr[1] // 4
arr[1] = 0;
arr[1] // 0
```

访问多位数数组的值也一样：

```javascript
var arr = [
    [1,2,3],
    [4,5,6],
    [7,8,9],
    [[10,11,12], 13, 14]
];
arr[0]; // 等于 [1,2,3]
arr[1][2]; // 等于 6
arr[3][0][1]; // 等于 11
```

##### arr.push()

一个简单的方法将数据追加到一个数组的末尾是通过 `push()` 函数。

`.push()` 接受把一个或多个参数，并把它“推”入到数组的末尾。

```javascript
var arr = [1,2,3];
arr.push(4);
// 现在arr的值为 [1,2,3,4]
```

##### arr.pop()

改变数组中数据的另一种方法是用 `.pop()` 函数。

`.pop()` 函数用来“抛出”一个数组末尾的值。我们可以把这个“抛出”的值赋给一个变量存储起来。

数组中任何类型的条目（数值，字符串，甚至是数组）可以被“抛出来” 。

举个例子, 对于这段代码
`var oneDown = [1, 4, 6].pop();`
现在 `oneDown` 的值为 `6` ，数组变成了 `[1, 4]`。

##### arr.shift()

`pop()` 函数用来移出数组中最后一个元素。如果想要移出第一个元素要怎么办呢？

这就是 `.shift()` 的用武之地。它的工作原理就像 `.pop()`，但它移除的是第一个元素，而不是最后一个。

##### arr.unshift()

你不仅可以 `shift`（移出）数组中的第一个元素，你也可以 `unshift`（移入）一个元素到数组的头部。

`.unshift()` 函数用起来就像 `.push()` 函数一样, 但不是在数组的末尾添加元素，而是在数组的头部添加元素。

##### arr.map()

`map()` 方法可以迭代数组的每个元素，并根据回调函数（map(function())）处理每个元素，最后返回一个新数组，**不会改变**原数组。

**回调函数**的 `val` 参数表示数组元素的值。另外也可以有更多参数，包括元素索引 `index`、原始数组 `arr`。记住回调函数必须有个 `return` 值，这个返回值会成为新元素。

```javascript
// 根据oldArr生成的新数组newArr中每个元素都是其两倍
var newArr = oldArr.map(function(val) {
    return val * 2;
})

// 输入的是数组序号和元素值，序号*元素值成为新元素
var newArr = oldArr.map(function(val, index) {
    return val * index;
})
```

##### arr.reduce()

`reduce` 用来迭代一个数组，并且把它累积到一个值中。

使用 `reduce` 方法时，你要传入一个回调函数，这个回调函数的参数是一个“累加器”（如例子中的 `previousVal`) 和当前值（`currentVal`）。

`reduce` 方法有一个可选的第二参数，它可以被用来设置累加器的初始值。如果没有在这定义初始值，那么初始值将变成数组中的第一项，而 `currentVal` 将从数组的第二项开始。如

```javascript
var array = [4,5,6,7,8];

// 让数组中所有元素相加，返回它们的和
singleVal = array.reduce(function (previousVal, currentVal) {
    return previousVal + currentVal;
});

// 让数组中所有值相减
singleVar = array.reduce(function(previousVal, currentVal) {
    return previousVal - currentVal;
}, 0);
```

注意第二个例子中的 `reduce` 有第二个参数 0，这样就是从 0 中逐个减去数组中的值（结果为 -30）。否则，将从第一个元素中，从第二个元素开始逐个减去所有的值（结果为 -22）

##### arr.filter()

`filter` 方法用来迭代一个数组，并且按给出的条件过滤出符合的元素。

其回调函数会携带一个参数，为当前迭代的项（`val`）。回调函数返回 `true` 的项会保留在数组中，返回 `false` 的项会被过滤出数组。

```javascript
// 过滤掉等于5的元素
array = array.filter(function(val) {
    return val !== 5;
});
```

##### arr.sort()

它将值全部转换为字符串，并根据编码逐个排序元素（如果不加回调函数），所以想按大小排序的话需要写个回调函数

详情参考 [Array.prototype.sort()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

与前面的方法不同，它会改变原数组，而不会有返回值。不过回调函数是有返回值的。传入回调函数的参数它的两个元素，二者相减，a>b 返回正数，a<b 返回负数，a=b 返回 0，sort() 根据返回值的符号排序这两个元素。

```javascript
var arr = [12, 21, 1, 3];

// 将元素从小到大排序
arr.sort(function(a, b) {
    return a - b;
});

// 如果不加回调函数：
arr.sort();
// arr = [1, 12, 21, 3]
```

##### arr.reverse()

翻转数组，改变原数组，无返回值。

```javascript
var arr = [1, 2, 3];
arr.reverse();
// arr = [3, 2, 1];
```

##### arr.concat()

将两个数组的内容合并到一个新数组中，返回新数组。

```javascript
var oldArray = [1,2,3];
var concatMe = [4,5,6];

var newArray = oldArray.concat(concatMe);
// newArray = [1,2,3,4,5,6]
```

##### arr.join()

与字符串的 `split()` 方法对应，将数组以指定的方法连接成字符串。传入的参数一般是一个字符串或空格等。

```javascript
var veggies = ["Celery", "Radish", "Carrot", "Potato"];
var salad = veggies.join(" and ");
// salad = "Celery and Radish and Carrot and Potato" 
```

### 函数

#### 定义、参数

```javascript
function func1() {
    console.log("hello");
}
func1();

// 有参数的函数
function func2(a, b) {
    return a - b;
}
console.log(func2(4, 2));
```

#### 变量作用域

在 JavaScript 中， 作用域涉及到变量的作用范围。在函数外定义的变量具有全局作用域。这意味着，具有全局作用域的变量可以在代码的任何地方被调用。

这些没有使用 `var` 关键字定义的变量，会被自动创建在全局作用域中，形成全局变量。当在代码其他地方无意间定义了一个变量，刚好变量名与全局变量相同，这时会产生意想不到的后果。因此你应该总是使用 var 关键字来声明你的变量。

**优先级**

一个程序中有可能具有相同名称的局部变量和全局变量。在这种情况下，局部变量将会优先于全局变量。

```javascript
var someVar = "Hat";
function myFun() {
  var someVar = "Head";
  return someVar;
}
```

函数 `myFun` 将会返回 `"Head"`，因为局部变量优先级更高。

#### 队列函数

队列（queue）是一个抽象的数据结构，队列中的条目都是有秩序的。新的条目会被加到队列的末尾，旧的条目会从队列的头部被移出。

写一个函数 `queue` ，用一个数组 `arr` 和一个数字 `item` 作为参数。数字 `item` 添加到数组的结尾，然后移出数组的第一个元素，最后队列函数应该返回被删除的元素。

```javascript
function queue(arr, item) {
  arr.push(item);
  item = arr.shift();
  return item;
}
```

#### 随机函数、Math

`Math.random()` 生成一个 `[0, 1)` 区间的随机小数，它可以用来生成随机数，使用时不需导入。

```javascript
// 生成0~9的整数
Math.floor(Math.random() * 10)

// 生成min~max的随机整数
Math.floor(Math.random() * (max - min + 1)) + min
```

### 语句

#### if

```javascript
if (condition 1) {
    statement 1;
} else if (condition 2) {
    statement 2;
} else (condition 3) {
    statement 3;
}
```

##### 条件语句

另一种数据类型是布尔（Boolean）。布尔值要么是true 要么是false。它非常像电路开关， true 是“开”，false 是“关”。这两种状态是互斥的。

一个表达式的结果如果能返回一个布尔值，或者 0、[]、null、""、undefined 等“空值”或“假值”，这个语句就是个布尔（条件）表达式，可以放在条件语句中作为判断的条件。如

```javascript
if (a >= b)
var arr = [];
if (arr) {} // 由于arr为空，会判断为false

arr = [1, 2];
if (arr) {} // 现在arr不为空，判断为true
```

##### 布尔运算符

多一个等号的结果会有所不同。如：

```javascript
1 != 2     // true
1 != 1     // false
1 != "1"   // false
1 !== "1"  // true
1 != true  // false
1 !== true // true
0 != false // false
```

#### switch

```javascript
switch (num) {
    case value1:
        statement1;
        break;
    case value2:
        statement2;
        break;
    ...
    case valueN:
        statementN;
        break;
    default:
        statement(N+1);
}
```

将 `switch` 后面的表达式 `()` 的结果逐个与 `value` 比较，如果不加 `break` 就会一直继续直到比较完所有的值，所以最后一项不用加 `break`。最后可以加个 `default`，它将在最后执行。

#### for

示例如下。其中 `var i = 0` 初始化了迭代器

`i < 10` 是迭代条件，表示当符合这个条件时，会执行下面的"计数器"

`i += 2` 是计数器，指定了迭代的方式（正反向、步长）

```javascript
// 循环偶数
var ourArray = [];
for (var i = 0; i < 10; i += 2) {
    ourArray.push(i);
}

// 逆向迭代
var ourArray = [];
for (var i=10; i > 0; i-=2) {
    ourArray.push(i);
}

// 迭代数组
var arr = [10,9,8,7,6];
for (var i=0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

#### while

```javascript
var ourArray = [];
var i = 0;
while(i < 5) {
    ourArray.push(i);
    i++;
}
```

### 对象

对象和数组很相似，数组是通过索引来访问和修改数据，对象是通过属性来访问和修改数据的。

对象适合用来存储结构化数据，就和真实世界的对象一模一样，比如一只猫。

```javascript
// 定义对象，逗号隔开属性
var testObj = {
  "hat": "ballcap",
  "shirt": "jersey",
  "an entree": "cleats",
  16: "Montana",
  19: "Unitas",
  "enemies": ["Water", "Dogs"]
};

// 访问
var hatValue = testObj.hat;
var entreeValue = testObj["an entree"]; // 有空格的属性必须用[]访问
var playerNumber = 16;
var player = testObj[playerNumber];

// 修改
testObj.shirt = "fsdaon";
testObj["an entree"] = "dffas";

var myObj = {
    top: "hat",
    bottom: "pants"
};
myObj.hasOwnProperty("top");    // true
myObj.hasOwnProperty("middle"); // false
```

#### JSON对象

JavaScript Object Notation 简称 `JSON`，它使用 JavaScript 对象的格式来存储数据。JSON是灵活的，因为它允许数据结构是字符串，数字，布尔值，字符串，和对象的任意组合。

这里是一个JSON对象的示例：

```javascript
var ourMusic = [
    {
        "artist": "Daft Punk",
        "title": "Homework",
        "release_year": 1997,
        "formats": [ 
            "CD", 
            "Cassette", 
            "LP" ],
        "gold": true
    },
    {
        "artist": "Daft Punk",
        "title": "Homework",
        "release_year": 1997,
        "formats": [ 
            "CD", 
            "Cassette", 
            "LP" ],
        "gold": true
    }
];

// 访问
ourMusic[0].formats[1];       // "Cassette"
ourMusic[1]["release_year"];  // 1997
```

这是一个对象数组，并且对象有各种关于专辑的 详细信息。它也有一个嵌套的 `formats` 的数组。附加专辑记录可以被添加到数组的最上层。

#### 构造函数

我们还可以使用构造函数来创建对象。

构造函数通常使用大写字母开头，以便把自己和其他普通函数区别开。

```javascript
var Car = function() {
  this.wheels = 4;
  this.engines = 1;
  this.seats = 1;
};
```

在构造函数中，`this` 指向被此构造函数创建出来的对象 。所以，当我们在构造函数中写：`this.wheels = 4;` 时，它创建出来的新对象将带有 wheels 属性，并且赋值为 4。你可以认为构造函数描述了它所创建出来的对象。

使用构造函数：`var myCar = new Car();`

`myCar` 现在成为了 `Car` 的一个 实例（instance）。记住：要使用 `new` 关键字 去调用构造函数。因为只有这样，JavaScript才知道这是要去构造一个新对象，并且把构造函数中的 `this` 指向这个新对象。

现在，当实例创建后，可以像普通对象一样被使用，如：`myCar.turboType = "twin";`

我们的 `myCar` 变量现在有了一个 `turboType` 属性了，且值为 `"twin"` 。

可以向构造函数中添加参数，并在调用时传入，用这组参数创建新对象：

```javascript
var Car = function(wheels, seats, engines) {
    this.wheels = wheels;
    this.seats = seats;
    this.engines = engines;
};
var myCar = new Car(6, 3, 1);
```

#### 对象的属性和方法

对象内使用 `var` 定义的变量无法在对象外部被访问，称为对象的"私有属性"。相对的，对象中使用 `this` 定义的属性是可以被外部访问的"公有属性"

"私有方法"是在对象内部定义的函数，同样不能在外部直接访问，通过 `obj.func()` 的形式使用，只对对象生效。相对的，用 `this` 定义的方法是公有方法，可以被外界调用。

```javascript
var Car = function() {
    // a private variable
    var speed = 10;

    // a private function
    this.accelerate = function(change) {
        speed += change;
    };

    // a public function
    this.getSpeed = function() {
        return speed;
    };
};

// use public function
var myCar = new Car();
myCar.getSpeed(); // return value of the private variable speed
```

