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

## 1. 静态属性

```javascript
// Number.POSITIVE_INFINITY 表示无穷大的数值
Number.POSITIVE_INFINITY; // Infinity

// Number.NEGATIVE_INFINITY 表示负无穷大的数值
Number.NEGATIVE_INFINITY; // -Infinity

// Number.NaN 表示非数值
Number.NaN; // NaN
isNaN(Number.NaN); // true

// Number.MAX_SAFE_INTEGER 表示能够精确表示的最大整数
Number.MAX_SAFE_INTEGER; // 9007199254740991
Math.pow(2, 53) - 1 === Number.MAX_SAFE_INTEGER; // true

// Number.MIN_SAFE_INTEGER; 表示能够精确表示的最小整数
Number.MIN_SAFE_INTEGER; // -9007199254740991
Number.MIN_SAFE_INTEGER === -Math.pow(2, 53) + 1; // true

// Number.MAX_VALUE 表示最大的正数
Number.MAX_VALUE; // 1.7976931348623157e+308
Number.MAX_VALUE < Infinity; // true

// Number.MIN_VALUE 表示最小的正数
Number.MAX_VALUE; // 5e-324
```

## 2. 实例方法
