# Document 节点

`document` 节点对象代表整个文档，每张网页都有自己的 `document` 对象。`window.document` 属性就指向这个对象。只要浏览器开始载入 HTML 文档，该对象就存在了，可以直接使用。

`document` 对象有不同的办法可以获取。

- 正常的网页，直接使用 `document` 或 `window.document`。
- `iframe` 框架里面的网页，使用 `iframe` 节点的 `contentDocument` 属性。
- `Ajax` 操作返回的文档，使用 `XMLHttpRequest` 对象的 `responseXML` 属性。
- 内部节点的 `ownerDocument` 属性。
- `document` 对象继承了 `EventTarget` 接口和 `Node` 接口，并且混入（mixin）了 `ParentNode` 接口。这意味着，这些接口的方法都可以在 `document` 对象上调用。除此之外，`document` 对象还有很多自己的属性和方法。

```javascript
document === window.document  //true
```

## 1. 属性

### 1.1. 快捷方式属性

以下属性是指文档内部的某个节点的快捷方式。

#### 1.1.1 document.defaultView

`document.defaultView` 属性返回 `document` 对象所属的 `window` 对象。如果当前文档不属于 `window` 对象，该属性返回 `null`。

```javascript
document.defaultView === window  // true
```

#### 1.1.2. document.doctype

对于 HTML 文档来说，`document` 对象一般有两个子节点。第一个子节点是 document.doctype，即文档类型（Document Type Declaration，简写DTD）节点。HTML 的文档类型节点，一般写成 `<!DOCTYPE html>`。如果网页没有声明 DTD，该属性返回null。

```javascript
document.firstChild === document.doctype  //true
typeof document.doctype  // "object"
document.doctype instanceof DocumentType  // true
document.doctype.name  // "html"
```

以上代码说明：

- `document` 的第一个子节点是 `document.doctype`。
- `document.doctype` 是一种对象。
- `document.doctype` 是 `DocumentType` 的实例。
- 文档类型是 `HTML`。

#### 1.1.3. document.documentElement

`document.documentElement` 属性返回当前文档的根元素节点（root）。它通常是 `document` 节点的第二个子节点，紧跟在 `document.doctype` 节点后面。HTML网页的该属性，一般是 `<html>` 节点。

```javascript
document.documentElement === document.lastChild  // true
document.documentElement instanceof HTMLHtmlElement  // true
HTMLHtmlElement.__proto__ === HTMLElement  // true
```

以上代码说明：

- `document` 的最后一个子节点（第二个）是 HTML 节点。
- `document.documentElement` 是 `HTMLHtmlElement` 的实例。
- `HTMLHtmlElement` 的原型对象是 `HTMLHtmlElement`。

#### 1.1.4. document.body，document.head

`document.body` 属性指向 `<body>` 节点，`document.head` 属性指向 `<head>` 节点。

这两个属性总是存在的，如果网页源码里面省略了 `<head>` 或 `<body>` ，浏览器会自动创建。另外，这两个属性是可写的，如果改写它们的值，相当于移除所有子节点。

#### 1.1.5. document.scrollingElement

```javascript
document.scrollingElement.scrollTop = 0  // 网页将滚动到顶部
```

`document.scrollingElement` 属性返回文档的滚动元素。也就是说，当文档整体滚动时，到底是哪个元素在滚动。

标准模式下，这个属性返回的文档的根元素 `document.documentElement`（即 `<html>`）。IE 浏览器下没有返回。

#### 1.1.6. document.activeElement

`document.activeElement` 属性返回获得当前焦点（focus）的 DOM 元素。通常，这个属性返回的是`<input>`、`<textarea>`、`<select>` 等表单元素，如果当前没有焦点元素，返回 `<body>` 元素或`null`。

#### 1.1.7. document.fullscreenElement

`document.fullscreenElement` 属性返回当前以全屏状态展示的 DOM 元素。如果不是全屏状态，该属性返回 `null`。

```javascript
document.fullscreenElement  // null
```

### 1.2 节点集合属性

- `document.forms` 返回所有 `<form>` 表单节点
- `document.images` 返回所有 `<img>` 图片节点
- `document.links` 返回所有 `<a>` 和 `<area>` 节点
- `document.scripts` 返回所有 `<script>` 节点
- `document.embeds` 返回所有`<embed>` 节点。
- `document.plugins` 返回所有 `<embed>`节点。
- `document.styleSheets` 属性返回文档内嵌或引入的样式表集合

```javascript
document.embeds === document.plugins // true
```

除了 `document.styleSheets`，以上的集合属性返回的都是 `HTMLCollection` 实例。

```javascript
document.links instanceof HTMLCollection // true
document.images instanceof HTMLCollection // true
document.forms instanceof HTMLCollection // true
document.embeds instanceof HTMLCollection // true
document.scripts instanceof HTMLCollection // true
```

### 1.3. 文档静态信息属性

#### 1.3.1. document.documentURI 和 document.URL

`document.documentURI` 属性和 `document.URL` 属性都返回一个字符串，表示当前文档的网址。不同之处是它们继承自不同的接口，`documentURI` 继承自 `Document` 接口，可用于所有文档；URL继承自 `HTMLDocument` 接口，只能用于 HTML 文档。

如果文档的锚点（#anchor）变化，这两个属性都会跟着变化。

```javascript
document.URL === document.documentURI
```

#### 1.3.2. document.domain

`document.domain` 属性返回当前文档的域名，**不包含协议和端口**。比如，网页的网址是 `http://www.example.com:80/hello.html`，那么 `document.domain` 属性就等于 `www.example.com`。如果无法获取域名，该属性返回 `null`。

```javascript
documentURL  // http://news.baidu.com/internet
document.domain // "news.baidu.com"
```

`document.domain` 基本上是一个只读属性，只有一种情况除外。次级域名的网页，可以把 `document.domain` 设为对应的上级域名。比如，当前域名是 `a.sub.example.com`，则 `document.domain` 属性可以设置为 `sub.example.com`，也可以设为 `example.com`。修改后，`document.domain` 相同的两个网页，可以读取对方的资源，比如设置的 `Cookie`。

```javascript
document.URL
// "http://news.baidu.com/internet"

document.domain
// "news.baidu.com"

document.domain = "baidu.com"
// "baidu.com"

document.domain
// "baidu.com"
```

## 2. 方法