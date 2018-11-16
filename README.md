# JavascriptOJ

[ScriptOJ](http://scriptoj.mangojuice.top/) Web 前端开发评测系统, 从大量实战代码、面试题目中总结出精华题库和相应的测试,这里记录了题库的答案,

> 答案均为记录自己测试时通过的代码，每道题可能存在更优解，如有更好解决方案可以一起讨论。

---

**#0. Hello World**

在 id 为 content 的 div 中只显示 Hello World 字样。（注意不要有多余空白字符）

```html
<div id="content">Hello World</div>
```

---

**#1. 用 React.js 在页面上渲染标题**

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

**#2. 使用 React.js 构建一个未读消息组件 Notification。**

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

**#3. JSX 元素变量**

用 JSX 完成两个变量的定义：
第一个变量 `title` 为一个具有类名为 `title` 的 `<h1>` 元素，其内容为 ScriptOJ；

第二个变量 `page` 为一个具有类名为 `content` 的 `<div>` 元素，将之前定义的 `title` 变量插入其中作为它的内容。

```js
const title = <h1 className="title">ScriptOJ</h1>;
const page = <div className="content">{title}</div>;
```

---

**#4. 用 React.js 组建的房子**

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

**#5. 不能摸的狗（一**

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

**#6. 不能摸的狗（二）**

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

**#8. 打印章节标题**

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

**#9. 百分比换算器**

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

#19. **获取文件的扩展名**

完成 extname 函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入 emoji.png，返回 .png。

```js
const extname = filename => {
  const dot = filename.lastIndexOf(".");
  if (dot === -1 || dot === 0) return "";
  return filename.slice(dot);
};
```

---

**#24 +1s 程序**

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

**#54 你是五年的程序员吗？**

请写出一个函数 initArray ，接受两个参数 m 和 n，返回一个数组，它的长度是 m，每个值都是 n,不能用循环.

```js
const initArray = (m, n) => {
  return new Array(m).fill(n);
};
```

---

**#98 判断两个矩形是否重叠**
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
