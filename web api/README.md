# DOM

## 1. DOM简介

### 1.1 什么是DOM

文档对象模型（DOM）是处理页面文档的标准`编程接口`。

- 文档：一个页面就是一个文档，DOM中使用document表示。
- 元素：页面中所有的标签都是元素，DOM中使用element表示。
- 节点：页面中所有内容都是节点（标签、属性、文本等），DOM中使用node表示。

`DOM把以上内容都看成对象`

## 2. 获取元素

### 2.1 如何获取元素

DOM在实际开发中主要用来操作元素。

####  2.1.1 根据ID获取

使用`getElementById()`方法获取带有 ID 元素对象，返回的是对象。

`console.dir()`打印返回的元素对象，更好的查看里面的属性和方法。

#### 2.1.2 根据标签名获取

使用`getElementsByTagName()`方法可以返回带有指定标签名的`对象集合`，以伪数组的形式存储。

注：

- 因为得到的是一个对象的集合，所有想要操作里面的元素就需要遍历。
- 得到元素是动态的。

`element.getElementsByTagName`可以得到元素里面的某些标签。

```javascript
<ul>
     <li>12</li>
     <li>12</li>
     <li>12</li>
 </ul>
<ul id="nav">
     <li>123</li>
     <li>123</li>
     <li>123</li>
</ul>
<script>
     var nav = document.getElementById('nav');
     var navs = nav.getElementsByTagName('li');
      console.log(navs);
</script>
```

#### 2.2.3 根据类名获取

`document.getElementsByClassName('类名')`根据类名返回+元素对象合集。

`document.querySelector('选择器')`根据指定选择器返回第一个元素对象，里面的选择器需要加符号，类选择器要加点。

`document.querySelectorAll('选择器')`返回指定选择器的所有元素对象集合。

#### 2.2.4 获取特殊元素（html、body）

**获取body元素**

`document.body`返回body元素对象。

**获取html元素**

`document.documentElement`返回html元素对象。

## 3. 事件基础

| 鼠标事件    | 触发条件     |
| ----------- | ------------ |
| onclick     | 鼠标点击     |
| onmouseover | 鼠标经过     |
| onmouseout  | 鼠标离开     |
| onfocus     | 获得鼠标焦点 |
| onblur      | 失去鼠标焦点 |
| onmousemove | 鼠标移动     |
| onmouseup   | 鼠标弹起     |
| onmousedown | 鼠标按下     |

## 4. 操作元素

### 4.1 改变元素内容

```
element.innerText
```

```
element.innerHTML
```

innerText 和 innerHTML 区别：

1. innerText 不识别 html 标签。
2. innerHTML识别 html 标签 W3C标准，保留空格和换行。
3. 这两个属性是可读写的 可以回去元素里面的内容。

### 4.2 常用元素的属性操作

1. innerText、innerHTML
2. src、href
3. id、alt、title

### 4.3 表单元素的属性操作

type、value、checked、selected、disable

### 4.4 样式属性操作

通过JavaScript修改元素的大小、颜色、位置等。

> element.style   行内样式操作。适合样式较少或功能简单的情况。
>
> element.className   类名样式操作，适合样式较多或功能复杂的情况。

注：

1. js 里面的样式采取的时驼峰命名法 font Size、background Color。
2. js 修改style 样式操作，产生的是行内样式，css权重比较高。
3. className 会直接更改元素的 类名，会覆盖原先的类名。

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
        
        .change {
            background-color: purple;
            color: #fff;
            font-size: 25px;
            margin-top: 100px;
        }
    </style>
</head>


<body>
    <div class="first">文本</div>
    <script>
        // 1. 使用 element.style 获得修改元素样式  如果样式比较少 或者 功能简单的情况下使用
        var test = document.querySelector('div');
        test.onclick = function() {
            // this.style.backgroundColor = 'purple';
            // this.style.color = '#fff';
            // this.style.fontSize = '25px';
            // this.style.marginTop = '100px';
            // 让我们当前元素的类名改为了 change

            // 2. 我们可以通过 修改元素的className更改元素的样式 适合于样式较多或者功能复杂的情况
            // 3. 如果想要保留原先的类名，我们可以这么做 多类名选择器
            // this.className = 'change';
            this.className = 'first change';
        }
    </script>
</body>

</html>
```

#### 4.5 排他思想

如果有一组元素，想要某一个元素实现某种样式，需要用到循环的排他思想。

1. 所有元素全部清除样式
2. 给当前元素设置样式
3. 注意顺序不能颠倒，先 1 后 2；

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        var btn = document.getElementsByTagName('button');
        for (var i = 0; i < btn.length; i++) {
            btn[i].onclick = function() {
                // 1. 先把所有按钮背景颜色去掉
                for (var i = 0; i < btn.length; i++) {
                    btn[i].style.backgroundColor = '';
                }
                // 2. 然后再给当前的背景颜色
                this.style.backgroundColor = 'pink';
            }
        }
    </script>
</body>

</html>
```

#### 4.6 自定义属性操作

##### 4.6.1 获取属性值

`element.属性`

`element.getAttribute('属性')`;

```javascript
<div id="demo" index="1"> <div>
<script>
	var div = document.querySelector('div');
	// element.属性
	console.log(div.id);
	// element.getAttribute('属性')
	console.log(element.getAttribute('id'));
	console.log(element.getAttribute('index')); // 自定义属性
</script>
```

区别：

element.属性 获取内置属性值（元素本身自带的而属性）

element.getAttribute('属性') 主要获取`自定义`属性

##### 4.6.2 设置属性值

`element.属性= '值'`设置内置属性

`element.setAttribute('属性', '值')`自定义属性

`element.removeAttribute('属性')`移除属性

```javascript
<div id="demo" index="1"> <div>
<script>
	var div = document.querySelector('div');
	// (1) element.属性= '值'
        div.id = 'test';
        div.className = 'navs';
        // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // class 特殊  这里面写的就是class 不是className
        // 3 移除属性 removeAttribute(属性)    
        div.removeAttribute('index');
</script>
```

##### 4.6.3 H5自定义属性

自定义属性的目的：为了保存并使用数据，有些数据可以保存到页面中而不用保存到数据库中。

有些自定义属性很容易引起歧义，不容易判断是元素内置属性还是自定义属性。

所以H5新增了自定义属性：

H5规定自定义属性date-开头 作为属性名并赋值。

如：<div date-index = "1" > </div>

或使用js设置：

element.setAttribute('date-index',2)。

### 4.5 节点操作

#### 4.5.1 节点概述

一般节点至少拥有nodeTyoe（节点类型）、nodeName（节点名称）、nodeValue（节点值）三个基本属性。

元素节点：nodeTyoe 为1

属性节点：nodeTyoe 为2

文本节点： nodeTyoe 为3（文本节点包括文字、空格、换行等）。

`在实际开发中，节点操作主要操作是元素节点`。

#### 4.5.2 节点层次

利用DOM树可以把节点划分为不同的层级关系，常见的是`父子兄层关系`。

1. 父级节点

> node.parentNode

- node.parentNode 属性可返回某节点的父节点，返回的是`最近的一个父节点`。
- 如果指定的节点没有父节点则返回 null

```javascript
<div class="demo">
     <div class="box">
          <span class="erweima">×</span>
      </div>
</div>
 <script>
    // 1. 父节点 parentNode
    var erweima = document.querySelector('.erweima');
    // var box = document.querySelector('.box');
    // 得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null
	erweima.parentNode
	console.log(erweima.parentNode);
 </script>
```

2. 子节点

> parentNode.children

parentNode.children 是一个只读属性，返回`所有`子元素节点，只返回子元素节点，其余节点不返回。

```JavaScript
 <ul>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>

</ul>
<ol>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
        <li>我是li</li>
</ol>
 <script>
        // DOM 提供的方法（API）获取
        var ul = document.querySelector('ul');
        var lis = ul.querySelectorAll('li')；
        // 2. children 获取所有的子元素节点 也是我们实际开发常用的
        console.log(ul.children);
</script>
```

> parentNode.firstElementChild

parentNode.firstElementChild 返回`第一个`子元素节点，找不到则返回null

> parentNode.lastElementChild

parentNode.lastElementChild 返回`最后`一个子元素，找不到则返回 null

注意：这两个方法有兼容性问题，IE9以上支持。



在实际开发中，既没有兼容性问题又返回`第一个元素`

```javascript
 <ol>
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>我是li5</li>
</ol>
<script>
        // 3. 实际开发的写法  既没有兼容性问题又返回第一个子元素
        console.log(ol.children[0]); // 返回第一个元素
        console.log(ol.children[ol.children.length - 1]); // 返回最后一个元素
</script>
```

#### 4.5.3 兄弟节点

> node.nextElementSibling

node.nextElementSibling 返回当前元素`下一个兄弟节点`，找不到返回null。

> node.previousElementSibling 

node.previousElementSibling 返回当前元素上一个兄弟节点`，找不到返回null。

注：这两个方法有兼容性问题，IE9以上才支持。

#### 4.5.4 创建节点

> document.createElement('tageName')

document.createElement( ) 方法创建由tageName指定的HTML元素。因此这些元素原先是不存在的，是根据我们的需求动态生成的，也成为了动态创建元素节点。

```JavaScript
<ul></ul>
<script>
     // 1. 创建节点元素节点
     var li = document.createElement('li');
</script>
```

#### 4.5.5 添加节点

> node.appendChild(child)  node 父级   child 子级

node.appendChild( ) 方法将一个节点添加到指定父节点的子节点列表`末尾`。

> node.insertBefore(child ， 指定元素)

node.insertBefore() 方法将一个节点添加到父节点的指定子节点`前面`。

想要在页面中添加一个新的元素：1. 创建元素  2. 添加元素。

```javascript
<ul>
        <li>123</li>
</ul>
<script>
	var ul = document.querySelector('ul');
	// 1. 创建节点元素节点
	var li = document.createElement('li');
	// 2. 添加节点 node.appendChild(child)  node 父级  child 是子级 后面追加元素  类似于数组中的push
	ul.appendChild(li);
	// 3. 添加节点 node.insertBefore(child, 指定元素);
	 var lili = document.createElement('li');
	 ul.insertBefore(lili, ul.children[0]);
	// 4. 我们想要页面添加一个新的元素 ： 1. 创建元素 2. 添加元素
</script>
```

#### 4.5.6 删除节点

> node.removeChild(child)

node.removeChild(child) 方法从DOM中删除一个子节点。返回删除的节点。

阻止链接跳转：`JavaScript:;`

#### 4.5.7 复制节点

> node.cloneNode( )

node.cloneNode( ) 返回调用该方法的节点的一个副本，也成为了克隆节点。

```JavaScript
 <ul>
        <li>1111</li>
        <li>2</li>
 </ul>
<script>
        var ul = document.querySelector('ul');
        // 1. node.cloneNode(); 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容
        // 2. node.cloneNode(true); 括号为true 深拷贝 复制标签复制里面的内容
        var lili = ul.children[0].cloneNode(true);
        ul.appendChild(lili);
</script>
```

如何括号参数为`空或者为false`，则是

# 事件高级

## 1. 注册事件（绑定事件）

### 1.1addEventListener 事件监听方式

```javascript
 btns[1].addEventListener('click', function() {
            alert(22);
 })
```

## 2. 删除事件（解绑事件）

### 2.1 删除事件的方式

```javascript
<div>1</div>
<div>2</div>
<div>3</div>
<script>
        var divs = document.querySelectorAll('div');
        divs[0].onclick = function() {
                alert(11);
            // 1. 传统方式删除事件
                divs[0].onclick = null;
            }
            // 2. removeEventListener 删除事件
        divs[1].addEventListener('click', fn) // 里面的fn 不需要调用加小括号

        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn);
        }
        // 3. detachEvent IE
        divs[2].attachEvent('onclick', fn1);

        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick', fn1);
        }
</script>
```

## 3. DOM事件流



## 4. 事件对象

```\
eventTarge.onclick = function(e){
	// event就是事件对象，可以写成e或event
}
eventTarge.addEventListener('click',function(){
	
})
```

- vent 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看
-  事件对象只有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
-  事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
-   这个事件对象我们可以自己命名 比如 event 、 evt、 e
- 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法 e = e || window.event;

### 4.1 事件对象的常见属性和方法

`e.target`返回的是触发事件的对象   this 返回的是绑定事件的对象

区别：e.target点击了那个元素，就返回那个元素。this那个元素绑定了这个点击事件，那么就返回谁。

`e.type`返回事件类型 如：mouseover

`e.preventDefault()`阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交,dom标准写法。

- *普通浏览器 e.preventDefault(); 方法*
-  e.preventDefault();
-  低版本浏览器 ie678 returnValue 属性
-  e.returnValue;
-  我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式

## 5. 阻止事件冒泡

`e.stopPropagation()`阻止事件冒泡，dom标准。

`e.cancelBubble = true` 非标准 cancel 取消 bubble 泡泡

## 6. 事件委托（代理、委托）

事件委托的原理：`不是每一个子节点单独设置事件监听器，而是事件监听器设置在父节点上，然后利用冒泡原理影响设置每一个子节点。`

```javascript
<ul>
        <li>天官赐福，百无禁忌！</li>
        <li>天官赐福，百无禁忌！</li>
        <li>天官赐福，百无禁忌！</li>
        <li>天官赐福，百无禁忌！</li>
        <li>天官赐福，百无禁忌！</li>
</ul>
<script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('天官赐福，百无禁忌！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';


        })
</script>
```

## 7. 常用的鼠标事件

### 7.1 鼠标事件对象

`event`对象代表事件状态，跟事件一系列的相关集合。主要是用鼠标事件对象`mouseEvent`和键盘事件对象`keyboardEvent`。

1. `client` 鼠标在可视区的x和y坐标

```javascript
 document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.clientX);
        	console.log(e.clientY);
 })   
```

2. ``page` 鼠标在页面文档的x和y坐标

```javascript
 document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.pageX);
            console.log(e.pageY);
 }) 
```

3. `screen` 鼠标在电脑屏幕的x和y坐标

```javascript
 document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
             console.log(e.screenX);
            console.log(e.screenY);
 }) 
```

## 8. 常用的键盘事件

| 键盘事件   | 触发条件                                        |
| ---------- | ----------------------------------------------- |
| onkeyup    | 某个键盘按键被松开时触发                        |
| onkeydown  | 某个键盘按键被按下时触发                        |
| onkeypress | 某个键盘按键被按下时触发  不能识别功能键 如Ctrl |

### 8.1 键盘事件对象

`keyCode` 返回ASCII码值来判断用户按下了那个健。

注：onkeydown和onkeyup不区分字母大小写，onkeypress区分字母大小写。

​		keyCode属性能区分大小写，返回不同的ASCII值。

# BOM

## 1. window 对象的常见事件

### 1.1 窗口加载事件

> window.onload = function( ) { } 或 window.addEventListener('load' , function( ) { })

window.onload是窗口（页面）加载事件，当文档内容完全加载完成会触发事件，就是调用处理函数。

注：

1. window.onload 可以把js 代码写在页面元素的上方，onload是等页面全部加载完毕，再去执行处理函数。
2. window.onload传统注册事件方式只能写一次，如有多个，会以最后一个window.onload为准。
3. 使用addEvenListener则没有限制。

> document.add.addEventListener('DOMcontentLoaded' , function() { })

load 是等页面内容全部加载完毕，包含页面dom元素 图片 flash css等等。

如果页面图片很多，用DOMcontentLoaded事件比较合适，是DOM加载完毕，不包含图片 flash css等 加载速度比load快。

### 1.2 调整窗口大小事件

> window.onresize = function ( )  或 window.addEventListener('resize' , function( ) { })

window.onresize是调整窗口大小加载事件，当触发就调用的处理函数。

注：

1. 只要窗口发生变化，就会触发这个事件。
2. 经常利用这个事件完成响应式布局。window.innerWith当前屏幕的宽度。

```JavaScript
 <script>
        window.addEventListener('load', function() {
            var div = document.querySelector('div');
            window.addEventListener('resize', function() {
                console.log(window.innerWidth);
                console.log('变化了');
                if (window.innerWidth <= 800) {
                    div.style.display = 'none';
                } else {
                    div.style.display = 'block';
                }

            })
        })
</script>
<div></div>
```

## 2. 定时器

### 2.1 setTimeout( )定时器

> window.setTimeout( 调用函数，[延迟的毫秒数]);

setTimeout( )方法用于设置一个定时器，该定时器在定时器到期后执行调用函数。

注：

- window可以省略。
- 调用函数可以直接写函数或写成函数名。
- 延迟毫秒数默认是0，如果写，必须是毫秒。
- 定时器可能有很多种，经常给定时器设置一个标识符。

### 2. 2 停止定时器 setTimeout()定时器

> window.clearTimeout(timeoutID)

clearTimeout( )方法取消了先前通过调用setTimeout建立的定时器。

注：

- window可以省略。
- 里面的参数就是定时器的标识符。

```JavaScript
 <button>点击停止定时器</button>
<script>
        var btn = document.querySelector('button');
        var timer = setTimeout(function() {
            console.log('爆炸了');

        }, 5000);
        btn.addEventListener('click', function() {
            clearTimeout(timer);
        })
 </script>
```

### 2.3 setInterval( )定时器

>window.setInterval( 调用函数，[延迟的毫秒数]);

setInterval( )方法重复调用一个函数，每隔这个时间，就去调用一次回调函数。

**setTimeout和setInterval的区别：**

setTimeout 延时时间到了，就去调用这个回调函数，只调用一次 就结束这个定时器。

setInterval 每隔这个延时时间，就去调用这个回调函数，重复调用这个函数。

### 2.4 停止setInterval（）定时器

> window.clearInterval(interval ID)；

setInterval( ) 方法取消了先前通过调用函数setInterval（）建立的定时器。

```JavaScript
<button class="begin">开启定时器</button>
<button class="stop">停止定时器</button>
<script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var timer = null; // 全局变量  null是一个空对象
        begin.addEventListener('click', function() {
            timer = setInterval(function() {
                console.log('ni hao ma');

            }, 1000);
        })
        stop.addEventListener('click', function() {
            clearInterval(timer);
        })
</script>
```

## 3. js 的执行机制

![image-20210126112226839](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210126112226839.png)

![image-20210126112248692](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210126112248692.png)

## 4. location对象

location属性用于获取或设置窗体的URL，并且可以用于解析URL，因为这个属性返回的是一个对象，将这个属性成为location对象。

### 4.1 URL

`统一资源定位符（URL)`是互联网上标准资源地址，互联网上每个文件都有一个唯一的URL，包含的信息指出文件的位置以及浏览器应该怎么处理。

### 4.2 location对象

`location.href`获取或者设置整个URL。

`location.search` 返回参数。

| location对象        | 返回值                                               |
| ------------------- | ---------------------------------------------------- |
| location.assign( )  | 和href一样，可以跳转页面，记录历史，能后退页面       |
| location.replace( ) | 替换当前页面，不记录历史，不能后退页面               |
| location.reload( )  | 重新加载页面，相当于刷新按钮，如果参数为true强制刷新 |

## 5. navigator对象

navigator 对象包含有关浏览器的信息，最常用的属性 userAgent ，该属性可以返回由客户机发送服务器 user-agent头部信息。

## 6. history 对象

`history.back()` 后退功能。

`history.forward()`前进功能。

`history.go(参数)`前进后退功能 参数如果是 1 前进一个页面 如果-1后退一个页面。

# pc端网页特效

## 1. 元素偏移量 offset 系列

### 1.1 offset 概述

使用offset 系列相关属性可以`动态`得到该元素的位置（偏移）、大小等。

- 获取元素距离带有定位父元素的位置
- 获取元素自身的大小（宽度高度）
- 注：返回的数值都不带单位

offset系列属性：

| element.offsetParent | 返回作为该元素带有定位的父级元素，如果父级都没有定位则返回body |
| -------------------- | ------------------------------------------------------------ |
| element.offsetTop    | 返回元素相对定位父元素上方的偏移                             |
| element.offsetLeft   | 返回元素相对定位父元素左边框的偏移                           |
| eleement.offsetWidth | 返回自身包括padding、边框、内容区的宽度，返回数值不带参数    |
| element.offsetHeight | 返回自身包括padding、边框、内容                              |

### 1.2 offset和style的区别

offset：`想要获取元素大小位置，用offset更合适，offsetWidth等属性是只读属性，只能获取不能赋值。`

style：`想要给元素更改值，需要用style改变，style.width是可读属性，可以获取也可以赋值。` 

## 2. 元素可视区client系列

| client系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.clientTop    | 返回元素上边框的大小                                         |
| element.clientLeft   | 返回元素左边框的大小                                         |
| element.clientWidth  | 返回自身包括padding、内容区的宽度，返回数值不带单位，不包含边框 |
| element.clientHeight | 返回自身包括padding、内容区域的高度，返回数值不带单位、不包含边框 |

## 3. 立即执行函数

立即执行函数：不需要调用，立马能够自己执行。

写法：

> （function( ) { } ) ( )    或   （function( ) { } ( ) )

```javascript
(function(a, b) {
            console.log(a + b);
            var num = 10;
 })(1, 2); // 第二个小括号可以看做是调用函数
```

```javascript
(function sum(a, b) {
            console.log(a + b);
            var num = 10; // 局部变量
}(2, 3));
```

立即执行函数最大的作用：独立创建了一个作用域, 里面所有的变量都是局部变量 不会有命名冲突的情况。

## 4. 元素scroll系列属性

使用scroll系列的相关属性可以动态的得到该元素的大小、滚动距离等。 

| scroll               | 作用                                           |
| -------------------- | ---------------------------------------------- |
| element.scrollTop    | 返回被卷去的上侧距离，返回数值不带单位         |
| element.scrollLeft   | 返回被卷去的左侧距离，返回数值不带单位         |
| element.scrollWidth  | 返回自身实际的宽度，不含边框，返回数值不带单位 |
| element.scrollHeight | 返回自身实际的高度，不含边框，返回数值不带单位 |

三大系列总结：

- offset系列经常用于获取元素的位置：offsetLeft，offset Top。
- client用于获取元素的大小：client Width、clientHeight。
- scroll经常用于获取滚动距离：scrollTop、scrollLeft。
- `页面的滚动距离通过`window.pageXoffset获得。

## 5. mouseenter和mouseover的区别

- mouseover鼠标经过自身盒子会触发，经过子盒子还会触发，有冒泡事件。mouseenter只会经过自身盒子触发，mouseenter不会冒泡。
- 跟mouseenter搭配鼠标离开mouseleave同样不会冒泡。

# 移动端特效

## 1. 触屏事件概述

常见的触屏事件：

| 触屏touch事件 | 说明                          |
| ------------- | ----------------------------- |
| touchstart    | 手指触摸到一个DOM元素时触发   |
| touchmove     | 手指在一个DOM元素上滑动时触发 |
| touchend      | 手指从一个DOM元素上移开时触发 |

## 2. 触摸事件对象（touchEvent）

touchEvent是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件，这类事件用于描述一个或多个触电，可以检测触点的移动，触点的增加和减少。

触摸事件常见对象列表：

| 触摸列表       |                                            |
| -------------- | ------------------------------------------ |
| touches        | 正在触摸屏幕的所有手指的一个列表           |
| targetTouches  | 正在触摸当前DOM元素上的手指的一个列表      |
| changedTouches | 手指状态发生改变的列表，从无到有，从有到无 |

## 3. classList 属性

classList属性是返回元素的类名，该属性用于元素中添加类，移除类及切换css类。

**添加类：**

`element.classList.add('类名')`；

> div.classList.add('three');   添加一个three的类名

**移除类：**

`element.classList.remove('类名')`;

**切换类：**

`element.classList.toggle('类名')`;   

#  本地存储

  