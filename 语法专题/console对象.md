# console 对象

## console.log()

如果第一个参数是格式字符串（使用了格式占位符，`console.log` 方法将依次使用后面的参数替换占位符，然后再进行输出。

```javascript
console.log("%d + %d = %d", 1, 1, 2);
// 1 + 1 = 2
```

`console.log` 方法支持以下占位符，不同类型的数据必须使用对应的占位符。

- `%s` 字符串
- `%d` 整数
- `%i` 整数
- `%f` 浮点数
- `%o` 对象的链接
- `%c` `CSS` 格式字符串

```javascript
console.log("%o", "https://www.baidu.com");
// "https://www.baidu.com"   可以点击直接跳转到百度

console.log(
  "%cThis text is styled!",
  "background-color: #f00; color: #fff; font-size: 20px;"
);
// 这段代码将输出红底白字
```

![console.log的%c占位符输出]('./../images/console-log-%c.png')
