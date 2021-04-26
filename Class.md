# Class

## constructor 方法

`constructor()` 方法是类的默认方法，通过 `new` 命令生成对象实例时，自动调用该方法。一个类必须有 `constructor()` 方法，如果没有显式定义，一个空的 `constructor()` 方法会被默认添加。

```javascript
class Func {
  constructor() {
    console.log('x');
  }
}
new Func(); // "x"
```

实例化一个类时，类中的 `constructor()` 方法会被自动调用。

## 静态方法

类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上 `static` 关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod(); // "hello"
```

上面代码，在类中定义了一个 `classMethod` 的静态方法，可以通过类直接调用。但不可以通过类的实例对象来调用

```javascript
let foo = new Foo();
foo.classMethod();
// Uncaught TypeError: foo.classMethod is not a function
```

另一方面，如果没有通过 `static` 关键字来定义静态方法，这个方法就只能通过实例对象来调用，不能通过这个类来直接调用。

```javascript
class Foo3 {
  classMethod() {
    return 'hello';
  }
}

Foo3.classMethod();
// Uncaught TypeError: Foo3.classMethod is not a function

new Foo3().classMethod(); // "hello"
```

如果静态方法包含 this 关键字，这个 this 指的是类，而不是实例。

```javascript
class Foo {
  static bar() {
    return this;
  }
}
Foo.bar() === Foo; // true

let foo = new Foo();
Foo.bar() === foo; // false
foo instanceof Foo.bar(); // true
```

在看另一例子，静态方法可以和非静态方法重名，表示不同的方法。

```javascript
class Foo {
  static bar() {
    this.baz();
  }
  static baz() {
    console.log('hello');
  }
  baz() {
    console.log('world');
  }
}

Foo.bar(); // "hello"
```

父类的静态方法，可以被子类继承。

```javascript
class ParentClass {
  static bar() {
    console.log('bar');
  }
}
class childClass extends ParentClass {}
childClass.bar(); // "bar"
```
