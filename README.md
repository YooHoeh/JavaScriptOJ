<!-- TOC -->

- [JavascriptOJ](#JavascriptOJ)
  - [0. Hello World](#0-Hello-World)
  - [1. 用 React.js 在页面上渲染标题](#1-用-Reactjs-在页面上渲染标题)
  - [2. 使用 React.js 构建一个未读消息组件 Notification](#2-使用-Reactjs-构建一个未读消息组件-Notification)
  - [3. JSX 元素变量](#3-JSX-元素变量)
  - [4. 用 React.js 组建的房子](#4-用-Reactjs-组建的房子)
  - [5. 不能摸的狗（一）](#5-不能摸的狗一)
  - [6. 不能摸的狗（二）](#6-不能摸的狗二)
  - [8. 打印章节标题](#8-打印章节标题)
  - [9. 百分比换算器](#9-百分比换算器)
  - [11. 获取文本的高度](#11-获取文本的高度)
  - [19. 获取文件的扩展名](#19-获取文件的扩展名)
  - [23. 肥猫列表](#23-肥猫列表)
  - [24. +1s 程序](#24-1s-程序)
  - [30. curry 函数](#30-curry-函数)
  - [54. 你是五年的程序员吗](#54-你是五年的程序员吗)
  - [98. 判断两个矩形是否重叠](#98-判断两个矩形是否重叠)
  - [99. safeGet](#99-safeGet)
  - [102. 记忆化斐波那契函数（Memoization）](#102-记忆化斐波那契函数Memoization)

<!-- /TOC -->

# JavascriptOJ

[ScriptOJ](http://scriptoj.mangojuice.top/) Web 前端开发评测系统, 从大量实战代码、面试题目中总结出精华题库和相应的测试,这里记录了题库的答案,

> 答案均为记录自己测试时通过的代码，每道题可能存在更优解，如有更好解决方案可以一起讨论。

---

## 0. Hello World

在 id 为 content 的 div 中只显示 Hello World 字样。（注意不要有多余空白字符）

```html
<div id="content">Hello World</div>
```

---

## 1. 用 React.js 在页面上渲染标题

在页面上增加一个 `id` 为 `root` 的 `<div>` 元素。然后请你完成一个 `renderContent` 函数，这个函数会把传入的任意字符串都包装到一个 `<h1>` 元素中并且渲染到页面上。例如：

```js
renderContent("Hello World");
```

页面上就有相应的内容：

```html
<div id="root"><h1>Hello World</h1></div>
```

只能通过 React.js 来实现。

```html
<div id="root"></div>
```

```js
/* 环境中已经注入了 React，ReactDOM */
function renderContent(content) {
  ReactDOM.render(<h1>{content}</h1>, document.getElementById("root"));
}
```

---

## 2. 使用 React.js 构建一个未读消息组件 Notification

通过 `getNotificationsCount()` 来获取未读消息的数量 ，如果有未读消息 N 条，而且 N > 0，那么 Notification 组件渲染显示：

```html
<span>有(N)条未读消息</span>
```

否则显示：

```html
<span>没有未读消息</span>
```

（你只需要完成组件部分，不需要调用 ReactDOM）

```js
// 函数 getNotificationsCount 已经可以直接调用

class Notification extends Component {
  render() {
    const count = getNotificationsCount();
    return count > 0 ? (
      <span>
        有(
        {count}
        )条未读消息
      </span>
    ) : (
      <span>没有未读消息</span>
    );
  }
}
```

---

## 3. JSX 元素变量

用 JSX 完成两个变量的定义：
第一个变量 `title` 为一个具有类名为 `title` 的 `<h1>` 元素，其内容为 ScriptOJ；

第二个变量 `page` 为一个具有类名为 `content` 的 `<div>` 元素，将之前定义的 `title` 变量插入其中作为它的内容。

```js
const title = <h1 className="title">ScriptOJ</h1>;
const page = <div className="content">{title}</div>;
```

---

## 4. 用 React.js 组建的房子

一个房子里面有一个房间和一个洗手间，房间里面有一个人和两条狗。
请你完成组件：House，Room，Bathroom，Man，Dog，它们的最外层都用 div 标签包裹起来，类名分别为：house，room，bathroom，man，dog。组件的实现应该具有上述的嵌套关系。

```js
// Component 已经可以直接使用

class House extends Component {
  render() {
    return (
      <div className="house">
        <Room />
      </div>
    );
  }
}

class Room extends Component {
  render() {
    return (
      <div className="room">
        <Bathroom />
        <Man />
        <Dog />
        <Dog />
      </div>
    );
  }
}

class Bathroom extends Component {
  render() {
    return <div className="bathroom" />;
  }
}

class Man extends Component {
  render() {
    return <div className="man" />;
  }
}

class Dog extends Component {
  render() {
    return <div className="dog" />;
  }
}
```

---

## 5. 不能摸的狗（一）

有一只狗，不允许别人摸它，一旦摸它就会叫，然后就跑了。
完成 Dog 组件，当用户点击的时候会执行自身的 bark 和 run 方法。

```js
class Dog extends Component {
  bark() {
    console.log("bark");
    this.run();
  }

  run() {
    console.log("run");
  }

  render() {
    return <div onClick={this.bark.bind(this)}>DOG</div>;
  }
}
```

---

## 6. 不能摸的狗（二）

有一只狗，不允许别人摸它，一旦摸它就会叫，然后就跑了；这只狗跑一段时间（20~50ms）以后就会停下来，也不叫了。

完成 Dog 组件，当用户点击的时候会执行自身的 bark 和 run 方法。给这个 Dog 组件加上状态 isRunning 和 isBarking，在进行相应的动作的时候设置为 true，停下来的时候设置为 false。

```js
class Dog extends Component {
  constructor() {
    super();
    this.state = {
      isRunning: false,
      isBarking: false
    };
  }

  bark() {
    this.setState({ isBarking: true });
    setTimeout(() => this.setState({ isBarking: false }), 20);
    this.run();
  }

  run() {
    this.setState({ isRunning: true });
    setTimeout(() => this.setState({ isRunning: false }), 20);
  }

  render() {
    return <div onClick={this.bark.bind(this)}>DOG</div>;
  }
}
```

---

## 8. 打印章节标题

现在需要在页面上显示一本书的章节，章节内容存放到一个数组里面：

```js
const lessons = [
  { title: 'Lesson 1: title', description: 'Lesson 1: description' },
  { title: 'Lesson 2: title', description: 'Lesson 2: description' },
  { title: 'Lesson 3: title', description: 'Lesson 3: description' },
  { title: 'Lesson 4: title', description: 'Lesson 4: description' }
  ...
]
```

现在需要你构建两个组件。一个组件为 Lesson 组件，渲染特定章节的内容。可以接受一个名为 lesson 的 props，并且把章节以下面的格式显示出来：

```html
<h1>Lesson 1: title</h1>
<p>Lesson 1: description</p>
```

点击每个章节的时候，需要把章节在列表中的下标和它的标题打印（console.log）出来，例如第一个章节打印： 0 - Lesson 1: title，第二个章节打印：1 - Lesson 2: title。
另外一个组件为 LessonsList，接受一个名为 lessons 的 props，它会使用 Lesson 组件把章节列表渲染出来。

```js
class Lesson extends Component {
  handleClick(title, key) {}
  render() {
    const { lesson, index } = this.props;
    return (
      <div onClick={() => console.log(index + " - " + lesson.title)}>
        <h1>{lesson.title}</h1>
        <p>{lesson.description}</p>
      </div>
    );
  }
}

class LessonsList extends Component {
  renderList(lessonsList) {
    return lessonsList.map((item, index) => (
      <Lesson lesson={item} key={index} index={index} />
    ));
  }

  render() {
    const { lessons } = this.props;
    return <div>{this.renderList(lessons)}</div>;
  }
}
```

---

## 9. 百分比换算器

做一个百分比换算器，需要你完成三个组件：`<Input />`：封装了原生的`<input />`，可以输入任意数字`<PercentageShower />`：实时 显示 `<Input />` 中的数字内容，但是需要把它转换成百分比，例如 `<Input />` 输入的是 0.1，那么就要显示 10.00%，保留两位小数。`<PercentageApp />`：组合上述两个组件。

```js
class Input extends Component {
  render() {
    const { value, handleChange } = this.props;
    return (
      <div>
        <input type="number" value={value} onChange={handleChange} />
      </div>
    );
  }
}

class PercentageShower extends Component {
  render() {
    const { value } = this.props;
    return <div>{(value * 100).toFixed(2) + "%"}</div>;
  }
}

class PercentageApp extends Component {
  state = {
    value: 2
  };

  handleChange(e) {
    this.setState({
      value: e.target.value
    });
  }
  render() {
    return (
      <div>
        <PercentageShower value={this.state.value} />
        <Input
          handleChange={this.handleChange.bind(this)}
          value={this.state.value}
        />
      </div>
    );
  }
}
```

---

## 11. 获取文本的高度

完成 `Post` 组件，接受一个字符串的 `content` 作为 `props`，`Post` 会把它显示到自己的 `<p>` 元素内。

并且，点击 `<p>` 元素的时候，会使用 `console.log` 把元素的高度打印出来。

```js
class Post extends Component {
  showEleHeight(e) {
    console.log(e.target.clientHeight);
  }
  render() {
    const { content } = this.props;

    return <p onClick={this.showEleHeight.bind(this)}>{content}</p>;
  }
}
```

---

## 19. 获取文件的扩展名

完成 extname 函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入 emoji.png，返回 .png。

```js
const extname = filename => {
  const dot = filename.lastIndexOf(".");
  if (dot === -1 || dot === 0) return "";
  return filename.slice(dot);
};
```

---

## 23. 肥猫列表

现在有很多只猫，都很肥：

```js
const cats = [
  { name: 'Tom', weight: 300 },
  { name: 'Lucy', weight: 400 },
  { name: 'Lily', weight: 700 },
  { name: 'Jerry', weight: 600 },
  ...
]
```

现在你需要把它们按照由胖到瘦的顺序把它们渲染到 id 为 cats-list 的 div 元素当中：

```html
<div id="cat-list">
  <div class="cat">
    <span class="cat-name">Lily</span> <span class="cat-weight">700</span>
  </div>
  <div class="cat">
    <span class="cat-name">Jerry</span> <span class="cat-weight">600</span>
  </div>
  <div class="cat">
    <span class="cat-name">Lucy</span> <span class="cat-weight">400</span>
  </div>
  <div class="cat">
    <span class="cat-name">Tom</span> <span class="cat-weight">300</span>
  </div>
  ...
</div>
```

完成 `renderFatCats` 函数，接受一个 `cats` 数组作为参数，然后它会往 div#cats-list 元素内渲染类似以上的结果。注意类名需要保持一致；另外`renderFatCats` 可能会被多次调用，注意清空上一次渲染的数据。

你可以使用 `jQuery`、`React.js` 等方式来完成。

（你不需要调用 `renderFatCats`）。

```html
<div id="cats-list"></div>
```

```js
function renderFatCats(cats) {
  const list = document.getElementById("cats-list");
  list.innerHTML = "";
  cats.sort((a, b) => {
    return a.weight > b.weight ? -1 : 1;
  });

  let renders = "";
  cats.forEach(item => {
    renders += `<div class="cat">
                                  <span class="cat-name">${item.name}</span>
                                  <span class="cat-weight">${item.weight}</span>
                                </div>`;
  });
  list.innerHTML = renders.trim();
}
```

---

## 24. +1s 程序

完成一个生成计数器的函数 `plusFor`，调用它会返回一个计数器。计数器本身也是一个函数，每次调用会返回一个字符串。达到以下的效果：

```js
const counter1 = plusFor('小明')
counter1() // => 为小明+1s
counter1() // => 为小明+2s
counter1() // => 为小明+3s
...

const counter2 = plusFor('李梅')
counter2() // => 为李梅+1s
counter2() // => 为李梅+2s
counter2() // => 为李梅+3s
...
```

注意你只需要完成 `plusFor` 函数，不要使用额外的全局变量。

```js
const plusFor = name => {
  let count = 0;
  return () => {
    count++;
    return `为${name}+${count}s`;
  };
};
```

---

## 30. curry 函数

函数式编程当中有一个非常重要的概念就是 函数柯里化。一个接受 任意多个参数 的函数，如果执行的时候传入的参数不足，那么它会返回新的函数，新的函数会接受剩余的参数，直到所有参数都传入才执行操作。这种技术就叫柯里化。请你完成 curry 函数，它可以把任意的函数进行柯里化，效果如下：

```js
const f = (a, b, c d) => { ... }
const curried = curry(f)

curried(a, b, c, d)
curried(a, b, c)(d)
curried(a)(b, c, d)
curried(a, b)(c, d)
curried(a)(b, c)(d)
curried(a)(b)(c, d)
curried(a, b)(c)(d)
// ...
// 这些函数执行结果都一样

// 经典加法例子
const add = curry((a, b) => a + b)
const add1 = add(1)

add1(1) // => 2
add1(2) // => 3
add1(3) // => 4
//注意，传给 curry 的函数可能会有任意多个参数。
```

ES5 做法：

```js
function curry(fn) {
  var curArgs = arguments[1] && arguments.length > 1 ? arguments[1] : [];
  return function() {
    //  let args = Array.from(arguments); //es6
    var args = Array.prototype.slice(arguments);
    if (curArgs.length + arguments.length < fn.length) {
      return curry(fn, curArgs.concat(args));
    } else {
      return fn.apply(undefined, curArgs.concat(args));
    }
  };
}
```

ES6 做法：

```js
const curry = (f, arr = []) => {
  return (...args) => {
    return (a) => {
      return a.length === f.length ? f(a) : curry(f, a);
    }([...arr, ...args]);
  };
```

---

## 54. 你是五年的程序员吗

请写出一个函数 initArray ，接受两个参数 m 和 n，返回一个数组，它的长度是 m，每个值都是 n,不能用循环.

```js
const initArray = (m, n) => {
  return new Array(m).fill(n);
};
```

---

## 98. 判断两个矩形是否重叠

用一个对象的数据来表示一个矩形的位置和大小：

```js
{
x: 100,
y: 100,
width: 150,
height: 250
}
```

它表示一个宽为 150 高为 250 的矩形在页面上的 (100, 100) 的位置。

请你完成一个函数 isOverlap 可以接受两个矩形作为参数，判断这两个矩形在页面上是否重叠。例如：

```js
const rect1 = { x: 100, y: 100, width: 100, height: 100 };
const rect2 = { x: 150, y: 150, width: 100, height: 100 };
isOverlap(rect1, rect2); // => true
```

```js
const isOverlap = (rect1, rect2) => {
  let left, right, top, bottom;
  if (rect1.x < rect2.x) {
    left = rect1;
    right = rect2;
  } else {
    left = rect2;
    right = rect1;
  }
  if (left.x + left.width < right.x) return false;

  if (rect1.y > rect2.y) {
    top = rect1;
    bottom = rect2;
  } else {
    top = rect2;
    bottom = rect1;
  }
  if (top.y > bottom.y + bottom.height) return false;
  return true;
};
```

---

## 99. safeGet

有时候我们需要访问一个对象较深的层次，但是如果这个对象某个属性不存在的话就会报错，例如：

```js
var data = { a: { b: { c: 'ScriptOJ' } } }
data.a.b.c // => scriptoj
data.a.b.c.d // => 报错，代码停止执行
console.log('ScriptOJ') // => 不会被执行
```

请你完成一个 safeGet 函数，可以安全的获取无限多层次的数据，一旦数据不存在不会报错，会返回 undefined，例如：

```js
var data = { a: { b: { c: 'ScriptOJ' } } }
safeGet(data, 'a.b.c') // => scriptoj
safeGet(data, 'a.b.c.d') // => 返回 undefined
safeGet(data, 'a.b.c.d.e.f.g') // => 返回 undefined
console.log('ScriptOJ') // => 打印 ScriptOJ
```

```js
const safeGet = (data, path) => {
 if(data == undefined) return undefined;

 const pathArr = path.split('.');
 let result = data;
 for(let i = 0; i < pathArr.length; i++) {
   if(result[pathArr[i]] == undefined) return undefined;
   result = result[pathArr[i]];
 }
 return result
}

```

---

## 102. 记忆化斐波那契函数（Memoization）

斐波那契数列指的是类似于以下的数列：

1, 1, 2, 3, 5, 8, 13, ....

也就是，第 n 个数由数列的前两个相加而来：f(n) = f(n - 1) + f(n -2)

请你完成 fibonacci 函数，接受 n 作为参数，可以获取数列中第 n 个数，例如：

```js
fibonacci(1); // => 1
fibonacci(2); // => 1
fibonacci(3); // => 2
```

测试程序会从按顺序依次获取斐波那契数列中的数，请注意程序不要超时，也不要添加额外的全局变量。

```js
const fibonacci = n => {
  // 这里添加一个方法内变量cache来保存前1000000个值
  if (!fibonacci.cache) {
    fibonacci.cache = [];
    for (let i = 1; i <= 1000000; i++) {
      if (i === 1 || i === 2) {
        fibonacci.cache[i] = 1;
      } else if (i > 2) {
        fibonacci.cache[i] = fibonacci.cache[i - 1] + fibonacci.cache[i - 2];
      }
    }
  }

  return fibonacci.cache[n];
};
```
