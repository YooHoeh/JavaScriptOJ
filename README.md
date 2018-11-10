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

#19. **获取文件的扩展名**

完成 extname 函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入 emoji.png，返回 .png。

```js
const extname = filename => {
  const dot = filename.lastIndexOf(".");
  if (dot === -1 || dot === 0) return "";
  return filename.slice(dot);
};
```
