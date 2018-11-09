# JavascriptOJ
ScriptOJ Web 前端开发评测系统, 从大量实战代码、面试题目中总结出精华题库和相应的测试,这里记录了题库的答案

## 初级题目

1. 完成 extname 函数，它会接受一个文件名作为参数，你需要返回它的扩展名。例如，输入 emoji.png，返回 .png。
```js
const extname = (filename) => {
  const dot = filename.lastIndexOf('.');
  if(dot === -1 ||dot === 0) return "";
  return filename.slice(dot)
}
```
