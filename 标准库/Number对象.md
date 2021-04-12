# Number 对象

`Number` 对象是数值对应的包装对象，可以作为构造函数使用，也可以作为工具函数使用。

作为构造函数时，它主要用于生成值为数值的对象。

```javascript
let n = new Number(1);
n; // Number {1}
typeof n; // "object"
```

作为工具函数时，她可以将任意类型的值转换为数值。

有两个值转换为 `NaN`, 有四个转换为 `0`，

```javascript
Number(0);
```
