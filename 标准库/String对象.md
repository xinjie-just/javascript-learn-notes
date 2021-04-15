# String 对象

`String` 对象是 JavaScript 原生提供的三个包装对象之一，用来生成字符串对象。

```javascript
let s1 = "abc";
let s2 = new String("abc");

typeof s1; // 'string'
typeof s2; // 'object'

s2.valueOf(); // 'abc'
```

由于 `s2` 是字符串对象，`s2.valueOf()` 方法返回的就是它所对应的原始字符串。

```javascript
new String("abc");
// String {0, "a", 1: "b", 2: "c", length: 3}
new String("abc")[1]; // "b"
```

除了用作构造函数创建类似数组的对象外，`String` 还可以当做工具函数使用，将任意类型的值转换为字符串。

## 1. 静态方法

### 1.1. String.fromCharCode()

`String` 对象提供的静态方法（即定义在对象本身，而不是定义在对象实例的方法），主要是 `String.fromCharCode()`。该方法的参数是一个或多个数值，代表 `Unicode` 码点，返回值是这些码点组成的字符串。

```javascript
String.fromCharCode(); // ""
String.fromCharCode(97); // "a"
String.fromCharCode(104, 101, 108, 108, 111);
// "hello"
```

该方法不支持 `Unicode` 码点大于 `0xFFFF` 的字符，即传入的参数不能大于 `0xFFFF`（即十进制的 65535）。

```javascript
String.fromCharCode(0x20bb7);
// "ஷ"

String.fromCharCode(0x20bb7) === String.fromCharCode(0x0bb7);
// true
```

上面代码中，`String.fromCharCode` 参数 `0x20BB7` 大于 `0xFFFF`，导致返回结果出错。`0x20BB7` 对应的字符是汉字`𠮷`，但是返回结果却是另一个字符（码点 `0x0BB7`）。这是因为 `String.fromCharCode` 发现参数值大于 `0xFFFF`，就会忽略多出的位（即忽略 `0x20BB7` 里面的 2）。

## 3. 实例属性

### 3.1. String.prototype.length

```javascript
"abc".length; // 3
```

## 4. 实例方法

### 4.1. String.prototype.charAt()

`charAt()` 方法返回某个位置的字符，位置从 0 开始。

```javascript
let s = new String("abc");
s.charAt(); // "a"
s.charAt(0); // "a"
s.charAt(1); // "b"
s.charAt(s.length - 1); // "c"
s.charAt(-1); // ""
s.charAt(4); // ""
```

从上面代码可以看出，`charAt()` 方法：

- 不传参数时，返回第一个字符，相当于传参 `0`。
- 传参为负数时，返回空字符串。
- 传参为一个大于字符串长度的数时，返回空字符串。

### 4.2. String.prototype.charCodeAt()

`charCodeAt()`方法返回字符串指定位置的 `Unicode` 码点（十进制表示），相当于 `String.fromCharCode()`的逆操作。

```javascript
"d".charCodeAt(0); // 100
String.fromCharCode(100); // "d"
```

### 4.3. String.prototype.concat()

`concat` 方法用于连接多个字符，返回一个新字符串，不改变原字符串。

```javascript
let s11 = "qwe";
let s12 = "asd";
let s13 = s11.concat(s12);
s13; // "qweasd";
s11; // "qwe"

let s14 = "zxc";
let s15 = s14.concat(s12, s13);
s15; // "zxcasdqweasd"
```

如果参数不是字符串，`concat` 方法会将其先转为字符串，然后再连接。

```javascript
var one = 1;
var two = 2;
var three = "3";

"".concat(one, two, three); // "123"
one + two + three; // "33"
```

### 4.4. String.prototype.search()

`search()` 匹配字符串，返回匹配到的第一个位置。如果没有匹配到，返回 `-1`。类似于 `indexOf()`。

```javascript
"dog,pig,monkey".search("mo"); // 8
"dog,pig,monkey".search("money"); // -1

"dog,pig,monkey".indexOf("mo"); // 8
"dog,pig,monkey".indexOf("money"); // -1
```

### 4.5. String.prototype.split()

`split` 方法按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组。

```javascript
"abc".split("abc"); // ["", ""]
"a|b|c".split(""); // ["a", "|", "b", "|", "c"]
"a|b|c".split(); // ["a|b|c"]
"a||c".split("|"); // ['a', '', 'c']
"|b|c".split("|"); // ["", "b", "c"]
"a|b|".split("|"); // ["a", "b", ""]
```

从上面代码可以看出：

- 如果分割的字符串和原字符串相同，则返回两个空字符串成员组成的数组。
- 如果分割的字符串是空字符串，则返回数组的成员是原字符串的每一个字符。
- 如果省略参数，则返回数组的唯一成员就是原字符串。
- 如果满足分割规则的两个部分紧邻着（即两个分割符中间没有其他字符），则返回数组之中会有一个空字符串。
- 如果满足分割规则的部分处于字符串的开头或结尾（即它的前面或后面没有其他字符），则返回数组的第一个或最后一个成员是一个空字符串。

`split` 方法还可以接受第二个参数，限定返回数组的最大成员数。

```javascript
"a|b|c".split("|", 0); // []
"a|b|c".split("|", 1); // ["a"]
"a|b|c".split("|", 2); // ["a", "b"]
"a|b|c".split("|", 3); // ["a", "b", "c"]
"a|b|c".split("|", 4); // ["a", "b", "c"]
```
