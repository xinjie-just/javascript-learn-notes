# Array 对象

`Array` 是 JavaScript 的原生对象，同时也是一个构造函数，可以用它生成新的数组。

## 1. 实例方法

### 1.1. join()

`join()` 方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

```javascript
let a = [1, 2, 3, 4];

a.join(" "); // '1 2 3 4'
a.join(" | "); // "1 | 2 | 3 | 4"
a.join(); // "1,2,3,4"
```

如果数组成员是 `undefined` 或 `null` 或空位，会被转成空字符串。

```javascript
[undefined, null].join('#')
// '#'

['a',, 'b'].join('-')
// 'a--b'
```

通过 `call` 方法，这个方法也可以用于字符串或类似数组的对象。

```javascript
Array.prototype.join.call("hello", "-");
// "h-e-l-l-o"

var obj = { 0: "a", 1: "b", length: 2 };
Array.prototype.join.call(obj, "-");
// 'a-b'
```

### 1.2 concat()

`concat()` 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

`concat()` 方法内的参数可以是任意类型。

```javascript
["hello"].concat(["world"]);
// (2) ["hello", "world"]

["hello"].concat(1);
// (2) ["hello", 1]

["hello"].concat("!");
// (2) ["hello", "!"]

["hello"].concat(true);
// (2) ["hello", true]

["hello"].concat(function () {});
// (2) ["hello", ƒ]

["hello"].concat({ a: 1 });
// (2) ["hello", { a: 1 }]
```

### 1.3. reverse()

`reverse()` 方法用于颠倒排序数组元素，返回改变后的数组。该方法将改变原数组。

```javascript
let a4 = [1, 2, 3, 4, 5];
let a5 = a4.reverse();

a4; // [5, 4, 3, 2, 1]
a5; // [5, 4, 3, 2, 1]
```

### 1.4. slice()

`slice()` 方法用于提取目标数组的一部分，返回一个新数组，原数组不变。

```javascript
let a6 = [1, 2, 3, 4, 5];
let a7 = a6.slice(-3, -1);

a6; // (5) [1, 2, 3, 4, 5]
a7; // (5) [3, 4]
```

从以上代码可以看出：

> - 负数表示倒数计算的位置
> - `slice()` 方法不改变原数组，返回一个新数组
> - 返回的新数组的长度等于第二个数减去第一个数的值

如果第一个参数大于等于数组长度，或者第二个参数小于第一个参数，则返回空数组。

```javascript
var a = ["a", "b", "c"];
a.slice(4); // []
a.slice(2, 1); // []
```

`slice()` 方法的一个重要应用，是将类似数组的对象转为真正的数组。

类似数组的对象有字符串、DOM 集合、arguments 对象。以及其他定义了 `length` 属性和以自然数作为属性的对象。如 `{0: 'a', length: 1}`。

```javascript
Array.prototype.slice.call({ 0: "a", 1: "b", length: 2 });
// ['a', 'b']

Array.prototype.slice.call(document.querySelectorAll("div"));
Array.prototype.slice.call(arguments);
```

### 1.5. splice()

`splice()` 方法删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素组成的数组。该方法可以接收一个到 `n` 个参数，表示不同的含义。

> - 第一个参数表示开始删除的位置，如果只提供一个参数，表示从此位置开始删除后面的全部元素。第一个参数是负数表示从倒数计算位置。
> - 第二个参数表示删除的元素个数，返回的数组的长度和改值相同。第二个参数为 `0` 或负数 表示不删除。
> - 后面的参数表示要添加在被删除元素的位置的元素。

```javascript
let a1 = [1, 2, 3, 4];
a1.splice(2); // [3, 4]
a1; // [1, 2]

let a2 = ["a", "b", "c", "d", "e", "f"];
a2.splice(-4, 2); // ["c", "d"]

var a3 = [1, 1, 1];
a3.splice(1, 0, 2); // []
a3; // [1, 2, 1, 1]
```
