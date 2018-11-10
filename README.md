# JavascriptOJ
[ScriptOJ](http://scriptoj.mangojuice.top/) Web 前端开发评测系统, 从大量实战代码、面试题目中总结出精华题库和相应的测试,这里记录了题库的答案,
>答案均为记录自己测试时通过的代码，一道题可能存在更优解，学艺不深请谅解。

## JavaScript基础

0. **Hello World**
在 id 为 content 的 div 中只显示 Hello World 字样。（注意不要有多余空白字符）
```html
<div id='content'>Hello World</div>
```


19. 	**获取文件的扩展名**
完成 extname 函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入 emoji.png，返回 .png。
```js
const extname = (filename) => {
  const dot = filename.lastIndexOf('.');
  if(dot === -1 ||dot === 0) return "";
  return filename.slice(dot)
}
```
