# `__proto__` 和`constructor` 和 `prototype` 的联系和区别

> - 每个 `class` 都有显示原型 `prototype`
> - 每个实例都有隐式原型 `__proto__`
> - 实例的 `__proto__` 指向对应 `class` 的 `prototype`

## `constructor`

```javascript
(1).constructor === Number;  // true

'a'.constructor === String;  // true

true.constructor === Boolean;  // true

(function(){}).constructor === Function;  // true

({}).constructor === Object;  // true

[].constructor === Array;  // true

/* ----------------------------------- */

Number.constructor === Function;  // true

String.constructor === Function;  // true

Boolean.constructor === Function;  // true

Array.constructor === Function;  // true

Object.constructor === Function;  // true

Function.constructor === Function;  // true
```

## `__proto__`

`__proto__` 指向他们的原型对象，即父对象。`b.__proto__` 可以读作 **b的原型对象** （或 `b` 的父对象）。

```javascript
let n = 1;
n.__proto__ === Number.prototype;  // true
Number.prototype.__proto__ === Object.prototype;  // true

/* ----------------------------------- */

let s = 'a';
s.__proto__ === String.prototype;  // true
String.prototype.__proto__ === Object.prototype;  // true

/* ----------------------------------- */

let b = true;
b.__proto__ === Boolean.prototype;  // true
Boolean.prototype.__proto__ === Object.prototype;  // trun

/* ----------------------------------- */

let a = [1];
a.__proto__ === Array.prototype;  // true
Array.prototype.__proto__ === Object.prototype;  // true

/* ----------------------------------- */

let f = function () {};
f.__proto__ === Function.prototype;  // true
Function.prototype.__proto__ === Object.prototype;  // true

/* ----------------------------------- */

let o = {a: 1};
o.__proto__ === Object.prototype;  // true

/* ----------------------------------- */

Object.prototype.__proto__ === null;  // true
```
