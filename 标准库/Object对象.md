# Object 对象

## 1. `Object` 对象的原生方法

`Object` 对象的原生方法分成两类：`Object` 本身的方法与 `Object` 的实例的方法。

### 1.1. Object 本身的方法

```javascript
Object.print = function (o) {
  console.log(o);
};
```

原生的方法就是上面那种，直接定义在 `Object` 对象上。

### 1.2. Object 的实例的方法

定义在 `Object` 原型对象 `Object.prototype` 上的方法。可以被 `Object` 实例直接使用。

```javascript
Object.prototype.print = function () {
  console.log(this);
};

let obj = new Object();
obj.print(); // Object
```

## 2. Object()

`Object` 本身是一个函数，可以当作工具函数使用，将任意值转换为对象。

如果参数为空（或者是 `undefined` 或 `null`）, `Object()` 返回一个空对象。

```javascript
let obj = Object(undefined);
// 等价于
let obj = Object(null);
// 等价于
let obj = Object();

obj instanceof Object; // true
```

是将 `undefined` 和 `null` 转为对象，结果得到了一个空对象 `obj`。

`instanceof` 运算符用来验证，一个对象是否为指定的构造函数的实例。`obj instanceof Object` 返回 `true`，就表示 `obj` 对象是 `Object` 的实例。

同样的，可以验证其他类型的对象是否是它对应的构造函数的实例。

```javascript
Object(0) instanceof Number;
Object("") instanceof String;
Object(true) instanceof Boolean;
Object(false) instanceof Boolean;
```

其他类型的对象都是 `Object` 对象的实例。

```javascript
Number instanceof Object;
String instanceof Object;
Boolean instanceof Object;
Array instanceof Object;
Function instanceof Object;
```

## 3. Object 构造函数

`Object` 不仅可以当作工具函数使用，还可以当作构造函数使用，即前面可以使用 `new` 命令。

`Object` 构造函数的首要用途，是直接通过它来生成新对象。

```javascript
let obj = new Object();
```

> 通过 `let obj = new Object()` 的写法生成新对象，与字面量的写法 `let obj = {}` 是等价的。或者说，后者只是前者的一种简便写法。

`Object` 构造函数的用法与工具方法很相似，几乎一模一样。

虽然用法相似，但是 `Object(value)`与 `new Object(value)`两者的语义是不同的，`Object(value)`表示将 `value` 转成一个对象，`new Object(value)`则表示新生成一个对象，它的值是 `value`。

```javascript
let o1 = { a: 1 };
let o2 = new Object(o1);
o1 === o2; // true
```

## 4. Object 的静态方法

静态方法就是部署在 `Object` 对象自身的方法。

### 4.1. Object.keys()

`Object.keys()`方法用来遍历对象的属性。

`Object.keys()` 方法的参数是一个对象，返回一个数组。该数组的成员都是该对象自身的（而不是继承的）所有属性名。

```javascript
let o = { a: 1, b: 2 };
let a = Object.keys(o);
console.table(a);
```

| (index) | Value |
| ------- | ----- |
| 0       | "a"   |
| 1       | "b"   |

### 4.2. Object.getOwnPropertyNames()

`Object.getOwnPropertyNames()` 方法与 `Object.keys()` 类似，也是接受一个对象作为参数，返回一个数组，包含了这个对象自身的所有属性名。

```javascript
let o = { a: 2, b: 3 };
let a = Object.getOwnPropertyNames(o);
console.table(a);
```

| (index) | Value |
| ------- | ----- |
| 0       | "a"   |
| 1       | "b"   |

对于一般的对象来说，`Object.keys()`和 `Object.getOwnPropertyNames()`返回的结果是一样的。只有涉及不可枚举属性时，才会有不一样的结果。

`Object.getOwnPropertyNames()` 方法还返回不可枚举的属性名。

```javascript
let a89 = ["x", "y"];
Object.keys(a89);
// (2) ["0", "1"]
let a89 = ["x", "y"];
Object.getOwnPropertyNames(a89);
// (3) ["0", "1", "length"]
```

一般情况下，几乎总是使用 `Object.keys()` 方法，遍历对象的属性。
