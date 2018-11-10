# JavascriptOJ

[ScriptOJ](http://scriptoj.mangojuice.top/) Web 前端开发评测系统, 从大量实战代码、面试题目中总结出精华题库和相应的测试,这里记录了题库的答案,

> 答案均为记录自己测试时通过的代码，一道题可能存在更优解，学艺不深请谅解。

---

#0. **Hello World**

在 id 为 content 的 div 中只显示 Hello World 字样。（注意不要有多余空白字符）

```html
<div id='content'>Hello World</div>
```

#1. **用 React.js 在页面上渲染标题**

在页面上增加一个 id 为 root 的 <div> 元素。然后请你完成一个 renderContent 函数，这个函数会把传入的任意字符串都包装到一个 \<h1\> 元素中并且渲染到页面上。例如：

```js
renderContent("Hello World");
```

页面上就有相应的内容：

```html
<div id='root'>
  <h1>Hello World</h1>
</div>
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

#2.**使用 React.js 构建一个未读消息组件 Notification。**

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

#3 **JSX 元素变量**
用 JSX 完成两个变量的定义：

第一个变量 title 为一个具有类名为 title 的 \<h1\> 元素，其内容为 ScriptOJ；

第二个变量 page 为一个具有类名为 content 的 \<div\> 元素，将之前定义的 title 变量插入其中作为它的内容。

```js
const title = <h1 className="title">ScriptOJ</h1>;
const page = <div className="content">{title}</div>;
```

#4 **用 React.js 组建的房子**

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

#5 **不能摸的狗（一**

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
 #6 **不能摸的狗（二）**


  有一只狗，不允许别人摸它，一旦摸它就会叫，然后就跑了；这只狗跑一段时间（20~50ms）以后就会停下来，也不叫了。

  完成 Dog 组件，当用户点击的时候会执行自身的 bark 和 run 方法。给这个 Dog 组件加上状态 isRunning 和 isBarking，在进行相应的动作的时候设置为 true，停下来的时候设置为 false。
```js
class Dog extends Component {
  constructor () {
    super()
    this.state = {
      isRunning: false,
      isBarking: false
    }
  }

  bark () {
    this.setState({ isBarking: true })
    setTimeout(() => this.setState({ isBarking: false }), 20)
    this.run()
  }

  run () {
    this.setState({ isRunning:true })
    setTimeout(() => this.setState({ isRunning: false }), 20)
  }
  

  render() {
    return (
      <div onClick={this.bark.bind(this)}>DOG</div>
    )
  }
}
```



#19. **获取文件的扩展名**

完成 extname 函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入 emoji.png，返回 .png。

```js
const extname = filename => {
  const dot = filename.lastIndexOf(".");
  if (dot === -1 || dot === 0) return "";
  return filename.slice(dot);
};
```
