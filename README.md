# cici
一、getComputedStyle() 用法
document.defaultView.getComputedStyle(element[,pseudo-element]);  
或者
window.getComputedStyle(element[,pseudo-element]);
首先是有两个参数，元素和伪类。第二个参数不是必须的，当不查询伪类元素的时候可以忽略或者传入 null。

使用示例：

let my_div = document.getElementById("myDiv");
let style = window.getComputedStyle(my_div, null);
关于 defaultView 引用一下 MDN 对于 defaultView 的描述:

defaultView

在许多在线的演示代码中, getComputedStyle 是通过 document.defaultView 对象来调用的。 大部分情况下，这是不需要的， 因为可以直接通过 window 对象调用。但有一种情况，你必需要使用 defaultView, 那是在 Firefox 3.6 上访问子框架内的样式 (iframe)。

而且除了在 IE8 浏览器中 document.defaultView === window 返回的是 false 外，其他的浏览器（包括 IE9 ）返回的都是 true。所以后面直接使用 window 就好，不用在输入那么长的代码了。
二、返回值
getComputedStyle 返回的对象是 CSSStyleDeclaration 类型的对象。取数据的时候可以直接按照属性的取法去取数据，例如 style.backgroundColor。需要注意的是，返回的对象的键名是 css 的驼峰式写法，background-color -> backgroundColor。

需要注意的是 float 属性，根据 《JavaScript 高级程序》所描述的情况 ，float 是 JS 的保留关键字。根据 DOM2 级的规范，取元素的 float 的时候应该使用 cssFloat。其实 chrome 和 Firefox 是支持 float 属性的，也就是说可以直接使用。

var float_property = window.getComputedStyle.style; // chrome 和 Firefox支持
而在任何版本的 IE 中都不能这样使用，并且在 IE 8 中仅支持 styleFloat ，这个下面的兼容性问题中谈到。

三、和 style 的异同
getComputedStyle 和 element.style 的相同点就是二者返回的都是 CSSStyleDeclaration 对象，取相应属性值得时候都是采用的 CSS 驼峰式写法，均需要注意 float 属性。

而不同点就是：

element.style 读取的只是元素的内联样式，即写在元素的 style 属性上的样式；而 getComputedStyle 读取的样式是最终样式，包括了内联样式、嵌入样式和外部样式。
element.style 既支持读也支持写，我们通过 element.style 即可改写元素的样式。而 getComputedStyle 仅支持读并不支持写入。我们可以通过使用 getComputedStyle 读取样式，通过 element.style 修改样式
我们可以通过使用 getComputedStyle 读取样式，通过 element.style 修改样式。

四、兼容性
关于 getComputedStyle 的兼容性问题，在 Chrome 和 Firefox 是支持该属性的，同时 IE 9 10 11 也是支持相同的特性的，IE 8并不支持这个特性。 IE 8 支持的是 element.currentStyle 这个属性，这个属性返回的值和 getComputedStyle 的返回基本一致，只是在 float 的支持上，IE 8 支持的是 styleFloat,这点需要注意。
