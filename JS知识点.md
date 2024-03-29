## DOM简介

## 获取元素

## 事件基础

## 操作元素

#### H5自定义属性

只能获取data-开头的

dataset 是一个集合里面存放了所有以data开头的自定义属性

​    console.log(div.dataset);

​    console.log(div.dataset.index);

​    console.log(div.dataset['index']);

######     如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法

​    console.log(div.dataset.listName);

​    console.log(div.dataset['listName']);

## 节点操作

节点含有nodeType（节点类型），nodeName（节点名称），nodeValue（节点值）

- 元素节点nodeType为1

- 属性节点nodeType为2

- 文本节点nodeType为3（含有文字，空格，换行）

  ##### 主要操作元素节点

### 节点层级

1.父级节点

node.parentNode   得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null

2.子节点

- 父元素.childNodes        得到的所有的子节点 包含 元素节点 文本节点等等

​    console.log(ul.childNodes);

​    console.log(ul.childNodes[0].nodeType);

- ##### children 获取所有的<u>子元素节点</u> 也是我们实际开发常用的

​    console.log(ul.children);

- firstChild 第一个子节点 不管是<u>文本节点还是元素节点</u>

  parentNode.firstChild 

  ol.lastChild

- firstElementChild 返回第一个<u>子元素节点</u> ie9才支持

  ol.firstElementChild

  ol.lastElementChild

- ##### 实际开发的写法  既没有兼容性问题又返回第一个子元素

   第一个孩子   console.log(ol.children[0]);

​        最后一个孩子  console.log(ol.children[ol.children.length - 1]);

3.兄弟节点

##### 	nextSibling 下一个兄弟节点 包含<u>元素节点或者文本节点</u>等等

​	node.nextSibling

​	node.previousSibling

##### 	nextElementSibling 得到下一个<u>兄弟元素节点</u>

​	node.nextElementSibling

​	node.previousElementSibling

4.创建节点

​	document.createElement('li')

5.添加节点

* node.appendChild(child)  node 父级  child 是子级 后面追加元素  类似于数组中的push

  ul.appendChild(li);

*  添加节点 node.insertBefore(child, 指定元素);

  ​    var lili = document.createElement('li');

  ​    ul.insertBefore(lili, ul.children[0]);

我们想要页面添加一个新的元素 ： 1. 创建元素 2. 添加元素

6.删除节点

​	node.removeChild(child)

​	ul.removeChild(ul.children[0]);

7.复制节点（克隆节点）

1. node.cloneNode(); 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容

2. node.cloneNode(true); 括号为true 深拷贝 复制标签复制里面的内容

8.三种动态创建元素区别

- document.write()------直接内容写入文档流，但会导致页面重绘（！DOC的都没了）
- element.innerHTML
- document.createElement()

区别：

1. ##### innerHTML将内容写入某个DOM节点，不会导致页面重绘

2. ##### innerHTML创建多个元素效率更高（不直接拼接字符串，而是采用数组拼接）

   ```js
   <script>
       function fn() {
           var d1 = +new Date();
           var array = [];
           for (var i = 0; i < 1000; i++) {
               array.push('<div style="width:100px; height:2px; border:1px solid blue;"></div>');
           }
           document.body.innerHTML = array.join('');
           var d2 = +new Date();
           console.log(d2 - d1);
       }
       fn();
   </script>
   ```

## DOM重点核心

总结：

1. 创建

   1. document.write()
   2. innerHTML
   3. createElement

2. 增加

   1. appendChild
   2. insertBefore

3. 删除

   removeChild

4. 修改

   1. 修改元素属性：src、href、title···
   2. 修改普通元素内容：innerHTML，innerText
   3. 修改表单元素：value、type、disabled···
   4. 修改元素样式：style、className

5. 查找（获取dom元素）

   1. api：getElementById,getElementByTagName

   2. h5:quertSelector,quertSelectorAll()

   3. 节点操作：父（parentNode），子（children），兄（previousElementSibling，

      nextElementSibling）

6. 属性操作（自定义属性）

   1. setAttribute：设置dom属性值
   2. getAttribute：得到dom属性值
   3. removeAttribute：移出属性

7. 事件操作

   - 获取元素，给元素注册事件

   - #### 事件源.事件类型=事件处理程序

## 事件高级

1.注册事件（绑定事件）

传统注册方式：

##### 	事件源.onclick=function(){}

​	特点：注册事件的唯一性，同一元素只能设置一个处理函数，下面的覆盖上面的

方法监听注册方式：

##### 	eventTarget.addEventListen(type,listener,[,useCapture])

​	特点：同一元素可注册多个监听器

- type：事件类型字符串，eg.click，mouseover
- listener：事件处理函数，eg.事件发生时，会调用该监听函数
- useCapture：可选，默认false

2.删除事件（解绑事件）

##### 	eventTarget.removeEventListener(type,listener,[,useCapture])

    ```js
        // 2. removeEventListener 删除事件
        divs[1].addEventListener('click', fn) // 里面的fn 不需要调用加小括号
    
        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn);
        }
    ```

3.DOM事件流

事件流--从页面接收事件的顺序

事件发生会在元素节点间按特定顺序传播，该传播过程为DOM事件流

![image-20220810100407499](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810100407499.png)

DOM事件流分为三阶段：

1. 捕获阶段
2. 当前目标阶段
3. 冒泡阶段

- **事件冒泡：事件开始由最具体元素接收，之后逐级向上传播到DOM最顶层节点的过程**
- **事件捕获：由DOM最顶层节点开始，逐级向下传播到最具体元素接收的过程**

注意：

1. **JS 代码中只能执行捕获或者冒泡其中的一个阶段。**

2. **onclick 和 attachEvent（ie） 只能得到冒泡阶段。**

3. **捕获阶段 如果addEventListener 第三个参数是 true 那么则处于捕获阶段  document -> html -> body -> father -> son**

   ```js
   <div class="father">
       <div class="son">son盒子</div>
   </div>
   
   var son = document.querySelector('.son');
   son.addEventListener('click', function() {
      alert('son');
   }, true);
   var father = document.querySelector('.father');
   father.addEventListener('click', function() {
      alert('father');
   }, true);
   ```

4. **冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 那么则处于冒泡阶段  son -> father ->body -> html -> document**

   ```js
   var son = document.querySelector('.son');
   son.addEventListener('click', function() {
       alert('son');
   }, false);
   var father = document.querySelector('.father');
   father.addEventListener('click', function() {
       alert('father');
   }, false);
   document.addEventListener('click', function() {
       alert('document');
   })
   ```

4.事件对象

event对象代表事件状态，如键盘按键状态，鼠标位置，鼠标按钮状态...

​    1. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看

​    2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数

​    3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键

​    4. 这个事件对象我们可以自己命名 比如 event 、 evt、 e

    5. 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;

   ```js
div.addEventListener('click', function(e) {
    console.log(e);
})
   ```

#### Q. e.target和this的区别？

![image-20220810094900271](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810094900271.png)

**e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）**

**区别 ： e.target <u>点击了那个元素</u>，就返回那个元素 this 那个元素<u>绑定了这个点击事件，那么就返回谁</u>**

阻止默认行为

```js
        // 常见事件对象的属性和方法
        // 1. 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);

        function fn(e) {
            console.log(e.type);

        }
        // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function(e) {
                e.preventDefault(); //  dom 标准写法
            })
            // 3. 传统的注册方式
        a.onclick = function(e) {
            // 普通浏览器 e.preventDefault();  方法
            // e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            // e.returnValue;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            return false;
            alert(11);
        }
```

5.阻止事件冒泡

事件冒泡:开始由**具体元素**接收，**逐级向上传播到dom最顶层节点**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .father {
            overflow: hidden;
            width: 300px;
            height: 300px;
            margin: 100px auto;
            background-color: pink;
            text-align: center;
        }
        
        .son {
            width: 200px;
            height: 200px;
            margin: 50px;
            background-color: purple;
            line-height: 200px;
            color: #fff;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son">son儿子</div>
    </div>
    <script>
        // 常见事件对象的属性和方法
        // 阻止冒泡  dom 推荐的标准 stopPropagation() 
        var son = document.querySelector('.son');
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // stop 停止  Propagation 传播
            e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false);

        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
</body>

</html>
```

**只对当前元素有效，父级元素还需另行添加**

6.**事件委托**（代理，委派）

##### 核心：不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，利用冒泡原理影响设置每个子节点（给父节点添加监听器，利用事件冒泡影响一个子节点）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';


        })
    </script>
</body>

</html>
```

作用：只操作一次DOM，提高程序性能

7.常用的鼠标事件

![image-20220810101506009](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810101506009.png)

```html
<body>
    我是一段不愿意分享的文字
    <script>
        // 1. contextmenu 我们可以禁用右键菜单
        document.addEventListener('contextmenu', function(e) {
                e.preventDefault();
            })
        // 2. 禁止选中文字 selectstart
        document.addEventListener('selectstart', function(e) {
            e.preventDefault();
        })
    </script>
</body>
```

鼠标事件对象MouseEvent

![image-20220810102025094](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810102025094.png)

```html
<body>
    <script>
        // 鼠标事件对象 MouseEvent
        document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.clientX);
            console.log(e.clientY);
            console.log('---------------------');

            // 2. page 鼠标在页面文档的x和y坐标
            console.log(e.pageX);
            console.log(e.pageY);
            console.log('---------------------');

            // 3. screen 鼠标在电脑屏幕的x和y坐标
            console.log(e.screenX);
            console.log(e.screenY);

        })
    </script>
</body>
```

**page 鼠标在页面文档的x和y坐标常用**

8.常用的键盘事件

键盘事件对象KeyBoardEvent

![image-20220810110239342](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810110239342.png)

```html
<body>
    <script>
        // 常用的键盘事件
        //1. keyup 按键弹起的时候触发 
        // document.onkeyup = function() {
        //         console.log('我弹起了');

        //     }
        document.addEventListener('keyup', function() {
            console.log('我弹起了');
        })

        //3. keypress 按键按下的时候触发  不能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keypress', function() {
                console.log('我按下了press');
            })
            //2. keydown 按键按下的时候触发  能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keydown', function() {
                console.log('我按下了down');
            })
            // 4. 三个事件的执行顺序  keydown -- keypress -- keyup
    </script>
</body>
```

![image-20220810111502403](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810111502403.png)

​    // 键盘事件对象中的**keyCode属性可以得到相应键的ASCII码值**

​    // 1. 我们的**keyup 和keydown**事件**不区分字母大小写**  a 和 A 得到的都是65

​    // 2. 我们的**keypress** 事件 **区分字母大小写**  a  97 和 A 得到的是65

常用**keyup 和keydown**

###### keydown和keypress在文本框特点：事件触发时候，文字还未落入文本框中

###### **keyup**：事件触发的时候，文字已落入文本框内

使用场景：

keyup——————文本框输入时使用、

keydown——————一直按下某些键

keypress——————需要区分按键大小写

## BOM

### 1.BOM概述

BOM浏览器对象模型，**独立于内容而与浏览器窗口进行交互的对象** 核心对象：window

![image-20220810114549166](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810114549166.png)

![image-20220810114748557](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220810114748557.png)

##### window对象是浏览器顶级对象

1. JS访问浏览器窗口的一个接口
2. 是一个**全局对象**，定义在全局作用域的变量，函数都会编程window对象的属性和方法
3. 不要声明 var name=10；有window.name这个属性

### 2.window对象常见事件

1.窗口加载事件

```js
window.onload = function() {
    alert(22);
}
//或者
window.addEventListener('load', function () {
    alert(22);
})
```

window.onload是窗口（页面）加载事件，当文档内容（包括图像，脚本文件，CSS文件等）完全加载完成会触发该事件

window.onload传统注册只能写一次，若有多个则以最后一个为准

事件监听方法则无限制

另一种DOMContentLoaded （图片较大时，加载慢使用）

```js
document.addEventListener('DOMContentLoaded', function () {
    alert(33);
})
```

load 等页面内容全部加载完毕，**包含页面dom元素 图片 flash  css 等等**

DOMContentLoaded 是**DOM 加载完毕，不包含图片 falsh css 等**就可以执行 **加载速度比 load更快一些**

2.调整窗口大小事件

window.onsize=function(){}

window.addEventListener('resize', function() {})

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
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
</body>

</html>
```

像素发生变化就会触发

使用情景---响应式布局，window.innerWidth当前屏幕宽度

### 3.定时器

- setTimeout

  window.setTimeout(调用函数, 延时时间);

  ​    1. 这个window在调用的时候可以省略

  ​    2. 这个延时时间单位是毫秒 但是可以省略，如果省略默认的是0

     3. 这个调用函数可以直接写函数 还可以写 函数名 还有一个写法 '函数名()'

     4. 页面中可能有很多的定时器，我们经常给定时器加标识符 （名字) 

        var timer1 = setTimeout(callback, 3000);

  **回调函数：上一件事肝完，再回头掉头该函数**

  ##### 停止定时器：clearTimeout(timer)

  ```js
  <body>
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
  </body>
  ```

- setInterval

     1. 语法规范：  window.setInterval(调用函数, 延时时间);


2. setTimeout  延时时间到了，就去调用这个回调函数，只调用一次 就结束了这个定时器
  3. setInterval  每隔这个延时时间，就去调用这个回调函数，会调用很多次，重复调用这个函数

  ```js
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>动态倒计时</title>
      <style>
          div {
              margin: 200px;
          }
  
          span {
              display: inline-block;
              width: 40px;
              height: 40px;
              background-color: #333;
              font-size: 20px;
              color: #fff;
              text-align: center;
              line-height: 40px;
          }
      </style>
  </head>
  
  <body>
      <div>
          <span class="hour">1</span>
          <span class="minute">2</span>
          <span class="second">3</span>
      </div>
      <script>
          var hour = document.querySelector('.hour');
          var minute = document.querySelector('.minute');
          var second = document.querySelector('.second');
          var inputTime = +new Date('20223-5-1 18:00:00');
          cutDown();
          //开启定时器
          setInterval(cutDown, 1000);
  
          function cutDown() {
              var nowTime = +new Date();
              var times = (inputTime - nowTime) / 1000;
  
              var d = parseInt(times / 60 / 60 / 24);
              d = d < 10 ? '0' + d : d;
              var h = parseInt(times / 60 / 60 % 24);
              h = h < 10 ? '0' + h : h;
              hour.innerHTML = h;
              var m = parseInt(times / 60 % 60);
              m = m < 10 ? '0' + m : m;
              minute.innerHTML = m;
              var s = parseInt(times % 60);
              s = s < 10 ? '0' + s : s;
              second.innerHTML = s;
          }
      </script>
  </body>
  
  </html>
  ```

  **清除定时器：clearInterval(timer);**

  ```js
  <body>
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
  </body>
  ```

- this指向问题

  this指向在函数定义时确定不了，当函数执行时候才可确定this指向，一般this最终指向是调用它的对象

  ```html
  <body>
      <button>点击</button>
      <script>
          // this 指向问题 一般情况下this的最终指向的是那个调用它的对象
  
          // 1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
          console.log(this);
  
          function fn() {
              console.log(this);
  
          }
          window.fn();
          window.setTimeout(function() {
              console.log(this);
  
          }, 1000);
          // 2. 方法调用中谁调用this指向谁
          var o = {
              sayHi: function() {
                  console.log(this); // this指向的是 o 这个对象
  
              }
          }
          o.sayHi();
          var btn = document.querySelector('button');
          // btn.onclick = function() {
          //     console.log(this); // this指向的是btn这个按钮对象
  
          // }
          btn.addEventListener('click', function() {
                  console.log(this); // this指向的是btn这个按钮对象
  
              })
              // 3. 构造函数中this指向构造函数的实例
          function Fun() {
              console.log(this); // this 指向的是fun 实例对象
  
          }
          var fun = new Fun();
      </script>
  </body>
  ```

### 4.JS执行机制

- 同步：前一任务结束后执行后一任务，程序执行顺序与程序排列顺序一致的

  **同步任务都在主线程上执行，形成执行栈**

- 异步：某件事会花费较长时间，执行该事件同时还可以处理别的事情

  **异步任务通过回调函数实现**

  1. 普通事件：click，resize
  2. 资源加载：load，error
  3. 定时器：setInterval，setTimeout

  **异步任务相关回调函数添加到<u>任务队列（消息队列）</u>**

- **区别：这条流水线上各个流程的执行顺序不同**

- 总结

  1. 先执行**执行栈中同步任务**
  2. 异步任务（回调函数）放入任务队列
  3. 当执行栈中的所有同步任务执行完成。系统会按次序读取**任务队列中的异步任务**，被读取的异步任务结束等待状态，进入执行栈，开始执行

  ![image-20220811112544490](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220811112544490.png)

![image-20220811113108579](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220811113108579.png)

### 5.location对象

1. location属性

   window对象提供**location属性获取或设置窗体URL，还可解析URL**，该属性返回一个对象，于是也称location对象

2. URL

   ![image-20220811113450021](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220811113450021.png)

3. location对象的属性

   ![image-20220811113633584](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220811113633584.png)

4. location对象的方法

   ![image-20220811123831174](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220811123831174.png)

```html
<body>
    <button>点击</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // 记录浏览历史，所以可以实现后退功能
            // location.assign('http://www.itcast.cn');
            // 不记录浏览历史，所以不可以实现后退功能
            // location.replace('http://www.itcast.cn');
            location.reload(true);
        })
    </script>
</body>
```

### 6.navigator对象

**navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以返回由客户机发送服务器的user-agent头部的值。**

下面前端代码可以判断用户那个终端打开页面，实现跳转

```js
if( (navigator.userAgent.match( /(phonelpad|pod] iPhoneliPodliosliPad|Android lMobile|BlackBerry|IEMobile |MQQBrowser|JUc| Fennec|wOSBrowser|BrowserNG| webosl symbian |windows Phone)/i) )){
    window . location.href = "";//手机} 
else {
    window . location.href = "";//电脑
```

### 7.history对象

window对象给我们提供了一个history对象，**与浏览器历史记录进行交互**。该对象包含用户（在浏览器窗口中)访问过的URL。

![image-20220811124439206](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220811124439206.png)

## PC端网页特效

1. ### 元素偏移量offset

   1. offset概述

      **动态得到该元素位置（偏移）、大小等**

      - 获得元素距离带定位父元素的位置
      - 获得元素自身大小（宽度高度）
      - 注：返回数值**不带单位**

      ![image-20220813095943335](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220813095943335.png)

   2. offset和style区别

      ![image-20220813101043772](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220813101043772.png)
      
      **页面拖拽原理：鼠标按下（mousedown），鼠标移动（mousemove），鼠标松开（moseup）**
      
      **模态框移动计算核心：鼠标坐标减去鼠标在盒子内坐标**
      
      ![image-20220813203146513](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220813203146513.png)

2. ### 元素可视区client

   1. client概述

      client翻译过来就是客户端，我们使用client系列的相关属性来获取元素可视区的相关信息
      通过client系列的相关属性可以动态的得到该元素的边框大小、元素大小等。

      ![image-20220813232226274](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220813232226274.png)

   2. 立即执行函数

      立即执行函数: **不需要调用，立马能够自己执行的函数**
      
      最大的作用就是 **独立创建了一个作用域, 里面所有的变量都是局部变量 不会有命名冲突的情况**
      
      ```html
      <body>
          <script>
              // 1.立即执行函数: 不需要调用，立马能够自己执行的函数
              function fn() {
                  console.log(1);
      
              }
              fn();
              // 2. 写法 也可以传递参数进来
              // 1.(function() {})()    或者  2. (function(){}());
              (function(a, b) {
                  console.log(a + b);
                  var num = 10;
              })(1, 2); // 第二个小括号可以看做是调用函数
              (function sum(a, b) {
                  console.log(a + b);
                  var num = 10; // 局部变量
              }(2, 3));
          </script>
      </body>
      ```

3. ### 元素滚动scoll

   scroll翻译过来就是滚动的，我们使用scroll系列的相关属性可以**动态的得到该元素的大小、滚动距离等。**

   ![image-20220814231041267](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220814231041267.png)

   ##### 页面被卷去的头部

   如果浏览器的高（或宽）度不足以显示整个页面时，会自动出现滚动条。**当滚动条向下滚动时，页面上面被隐藏掉的高度**，我们就称为页面被卷去的头部。滚动条在滚动时会触发onscroll事件。

   案例：

   1. 需要用到页面滚动事件scroll因为是页面滚动，所以事件源是document
   2. 滚动到某个位置，就是判断页面被卷去的上部值。
   3. **页面被卷去的头部:可以通过window.pageYoffset获得如果是被卷去的左侧window.pageXOffset**
   4. **注意，元素被卷去的头部是element.scrollTop ,如果是页面被卷去的头部则是window.pageYOffset**

4. 总结

   ![image-20220814235713936](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220814235713936.png)

   ![image-20220814235816976](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220814235816976.png)

   1. **offset系列 经常用于获得<u>元素位置</u>offsetLeft offsetTop**
   2. **client 经常用于获取<u>元素大小</u> clientWidth clientHeight**
   3. **scroll 经常用于获取<u>滚动距离</u>scrollTop scrolleft**
   4. **注意页面滚动的距离通过window. pagexoffset获得**

5. **mouseover和mouseenter区别**

   1. 鼠标移到元素上会触发mouseenter事件
   2. **mouseover鼠标经过自身盒子会触发，经过子盒子也会触发。mouseenter只经过自身盒子触发，因为不会冒泡，mouseleave鼠标离开也不会冒泡**

6. ### 动画函数封装

   1.   动画原理

      **核心：通过定时器setInterval不断移动盒子位置**

      1. 获得盒子当前位置

      2. 让盒子在当前位置加上1个移动距离

      3. 利用定时器不断重复这个操作

      4. 加一个结束定时器的条件

      5. 注意此元素需要添加定位， 才能使用element.style.left

   2. 动画函数简单封装

      注：函数需传递2个参数，**动画对象和移动到的距离**

      ```html
          <style>
              div {
                  position: absolute;
                  left: 0;
                  width: 100px;
                  height: 100px;
                  background-color: pink;
              }
              
              span {
                  position: absolute;
                  left: 0;
                  top: 200px;
                  display: block;
                  width: 150px;
                  height: 150px;
                  background-color: purple;
              }
          </style>
      
      <body>
          <div></div>
          <span>夏雨荷</span>
          <script>
              // 简单动画函数封装obj目标对象 target 目标位置
              function animate(obj, target) {
                  var timer = setInterval(function() {
                      if (obj.offsetLeft >= target) {
                          // 停止动画 本质是停止定时器
                          clearInterval(timer);
                      }
                      obj.style.left = obj.offsetLeft + 1 + 'px';
      
                  }, 30);
              }
      
              var div = document.querySelector('div');
              var span = document.querySelector('span');
              // 调用函数
              animate(div, 300);
              animate(span, 200);
          </script>
      </body>
      ```

   3. 动画函数给不同元素记录不同定时器

      给多个元素都是用该动画函数，每次都要var声明定时器，由此可以给不同元素使用不同定时器（自己专门用自己的定时器）

      **核心：js是一种动态语言，很方便给当前对象添加属性**

      ```html
      <body>
          <button>点击夏雨荷才走</button>
          <div></div>
          <span>夏雨荷</span>
          <script>
              // var obj = {};
              // obj.name = 'andy';
              // 简单动画函数封装obj目标对象 target 目标位置
              // 给不同的元素指定了不同的定时器
              function animate(obj, target) {
                  // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
                  // 解决方案就是 让我们元素只有一个定时器执行
                  // 先清除以前的定时器，只保留当前的一个定时器执行
                  clearInterval(obj.timer);
                  obj.timer = setInterval(function() {
                      if (obj.offsetLeft >= target) {
                          // 停止动画 本质是停止定时器
                          clearInterval(obj.timer);
                      }
                      obj.style.left = obj.offsetLeft + 1 + 'px';
      
                  }, 30);
              }
      
              var div = document.querySelector('div');
              var span = document.querySelector('span');
              var btn = document.querySelector('button');
              // 调用函数
              animate(div, 300);
              btn.addEventListener('click', function() {
                  animate(span, 200);
              })
          </script>
      </body>
      ```

   4. 缓动效果原理

      **让元素运动速度有所变化，最常见让速度慢慢停下**

      ​    思路：

      ​    1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。

      ​    2. 核心算法：(目标值 - 现在的位置) / 10 做为每次移动的距离 步长

             3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器
             4. 注意步长值需要调整

      ```html
      <body>
          <button>点击夏雨荷才走</button>
          <span>夏雨荷</span>
          <script>
              // 缓动动画函数封装obj目标对象 target 目标位置
              // 思路：
              // 1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。
              // 2. 核心算法：(目标值 - 现在的位置) / 10 做为每次移动的距离 步长
              // 3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器
              function animate(obj, target) {
                  // 先清除以前的定时器，只保留当前的一个定时器执行
                  clearInterval(obj.timer);
                  obj.timer = setInterval(function () {
                      // 步长值写到定时器的里面
                      var step = (target - obj.offsetLeft) / 10;
                      if (obj.offsetLeft == target) {
                          // 停止动画 本质是停止定时器
                          clearInterval(obj.timer);
                      }
                      // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                      obj.style.left = obj.offsetLeft + step + 'px';
      
                  }, 15);
              }
              var span = document.querySelector('span');
              var btn = document.querySelector('button');
      
              btn.addEventListener('click', function () {
                  // 调用函数
                  animate(span, 500);
              })
              // 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
              // 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
          </script>
      </body>
      ```

   5. 动画函数多个目标值之间移动

      案例：动画函数800移到500

      核心：点击按钮时，判断步长是正值还是负值

      1. 正值，步长往大了取整（ceil）
      2. 负值，步长往小了取整（floor）

      ```html
      <body>
          <button class="btn500">点击夏雨荷到500</button>
          <button class="btn800">点击夏雨荷到800</button>
          <span>夏雨荷</span>
          <script>
              // 缓动动画函数封装obj目标对象 target 目标位置
              // 思路：
              // 1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。
              // 2. 核心算法：(目标值 - 现在的位置) / 10 做为每次移动的距离 步长
              // 3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器
              function animate(obj, target) {
                  // 先清除以前的定时器，只保留当前的一个定时器执行
                  clearInterval(obj.timer);
                  obj.timer = setInterval(function() {
                      // 步长值写到定时器的里面
                      // 把我们步长值改为整数 不要出现小数的问题
                      // var step = Math.ceil((target - obj.offsetLeft) / 10);
                      var step = (target - obj.offsetLeft) / 10;
                      step = step > 0 ? Math.ceil(step) : Math.floor(step);
                      if (obj.offsetLeft == target) {
                          // 停止动画 本质是停止定时器
                          clearInterval(obj.timer);
                      }
                      // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                      obj.style.left = obj.offsetLeft + step + 'px';
      
                  }, 15);
              }
              var span = document.querySelector('span');
              var btn500 = document.querySelector('.btn500');
              var btn800 = document.querySelector('.btn800');
      
              btn500.addEventListener('click', function() {
                  // 调用函数
                  animate(span, 500);
              })
              btn800.addEventListener('click', function() {
                      // 调用函数
                      animate(span, 800);
                  })
                  // 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
                  // 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
          </script>
      </body>
      ```

   6. 动画函数添加回调函数

      **回调函数原理：函数可作为一个参数，将这个函数作为参数传到另一个函数里，当那个函数执行完成后，再执行传进去的这个函数**

      ```html
      <body>
          <button class="btn500">点击夏雨荷到500</button>
          <button class="btn800">点击夏雨荷到800</button>
          <span>夏雨荷</span>
          <script>
              // 缓动动画函数封装obj目标对象 target 目标位置
              // 思路：
              // 1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。
              // 2. 核心算法：(目标值 - 现在的位置) / 10 做为每次移动的距离 步长
              // 3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器
              function animate(obj, target, callback) {
                  // console.log(callback);  callback = function() {}  调用的时候 callback()
      
                  // 先清除以前的定时器，只保留当前的一个定时器执行
                  clearInterval(obj.timer);
                  obj.timer = setInterval(function() {
                      // 步长值写到定时器的里面
                      // 把我们步长值改为整数 不要出现小数的问题
                      // var step = Math.ceil((target - obj.offsetLeft) / 10);
                      var step = (target - obj.offsetLeft) / 10;
                      step = step > 0 ? Math.ceil(step) : Math.floor(step);
                      if (obj.offsetLeft == target) {
                          // 停止动画 本质是停止定时器
                          clearInterval(obj.timer);
                          // 回调函数写到定时器结束里面
                          if (callback) {
                              // 调用函数
                              callback();
                          }
                      }
                      // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                      obj.style.left = obj.offsetLeft + step + 'px';
      
                  }, 15);
              }
              var span = document.querySelector('span');
              var btn500 = document.querySelector('.btn500');
              var btn800 = document.querySelector('.btn800');
      
              btn500.addEventListener('click', function() {
                  // 调用函数
                  animate(span, 500);
              })
              btn800.addEventListener('click', function() {
                      // 调用函数
                      animate(span, 800, function() {
                          // alert('你好吗');
                          span.style.backgroundColor = 'red';
                      });
                  })
                  // 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
                  // 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
          </script>
      </body>
      ```

   7. 动画函数封装到单独js文件

      animate文件

7. ### 常见网页特效案例

   1. 案例：轮播图

   2. **节流阀：当上一个函数动画内容执行完毕，再执行下一个函数动画，让事件无法连续触发**

      **实现核心：利用回调函数，添加一个变量控制，锁住函数和解锁函数**

      eg.开始设置一个变量  var flag=true;

      if(flag){flag=false;do next} 关闭水龙头

      利用回调函数 动画执行完毕 flag=true 打开水龙头

   3. 案例：返回顶部

      滚动窗口至文档中特定位置：window.scroll(x,y)
   
      - 带有动画的返回顶部
      - 1.使用封装的animate动画函数
      - 2.只需把所有left值改成 **页面垂直滚动距离相关**就可以了
      - 3.页面滚动了多少，可以通过window.pageYOffset获得
      - 4.最后是页面滚动，使用window.scroll(x,y)
   
   4. 案例：筋斗云

## 移动端网页特效

1. 触屏事件（touch）

   1. 触摸事件可响应用户手指（或触控笔）对屏幕或触控板的操作

       | 触摸touch事件 | 说明                          |
       | ------------- | ----------------------------- |
       | touchstart    | 手指触摸到一个dom元素时触发   |
       | touchmove     | 手指在一个dom元素上滑动时触发 |
       | touchend      | 手指从一个dom元素上移开时触发 |

   2. 触摸事件对象（TouchEvent）

       | 触摸列表       | 说明                                           |
       | -------------- | ---------------------------------------------- |
       | touches        | 正在触摸屏幕的所有手指的一个列表               |
       | targetTouches  | 正在触摸当前DOM元素上的手指的一个列表          |
       | changedTouches | 手指状态发生改变的列表，从无到有，从有到无变化 |

   3. 移动端拖动元素

   ​    （1） 触摸元素 touchstart：  获取手指初始坐标，同时获得盒子原来的位置

   ​    （2） 移动手指 touchmove：  计算手指的滑动距离，并且移动盒子

   ​    （3） 离开手指 touchend:

   ​	**注：手指移动会触发滚动屏幕，由此需要阻止默认屏幕滚动（e.preventDefault()）**

2. 移动端常见特效

   ##### classList属性

   作用：返回元素类名。该属性用于在元素中添加，移除，切换CSS类

   ```html
   <script>
       	// classList 返回元素的类名
           var div = document.querySelector('div');
           // console.log(div.classList[1]);
           // 1. 添加类名  是在后面追加类名不会覆盖以前的类名 注意前面不需要加.
           div.classList.add('three');
           // 2. 删除类名
           div.classList.remove('one');
           // 3. 切换类
           var btn = document.querySelector('button');
           btn.addEventListener('click', function() {
               document.body.classList.toggle('bg');
           }	
   </script>
   ```

   **click延时解决方案**

   移动端click事件有300ms的延时，原因移动端屏幕双击会缩放（double tap to zoom）页面

   解决方案：

   1. 禁用缩放。浏览器禁用默认的双击缩放行为且去掉300ms的点击延迟。

      ```html
      <meta name="viewport" content="user-scalable=no">
      ```

   2. 利用touch事件自己封装这个事件解决300ms延迟

      原理

      1. 当手指触摸屏幕，记录当前触摸时间
      2. 当手指离开屏幕，用离开时间减去触摸时间
      3. 当时间小于150ms并且没有滑动过屏幕，则定义为点击

   3. 使用插件。fastclick插件解决300ms延迟

3. 移动端常见开发插件

   swiper

   superslide

   zy.media.js---视频插件

4. 移动端常用开发框架

   框架：一套架构，基于自身特点向用户提供一套较为完整的解决方案，其控制权在框架本身，使用者按框架所规定的某种规范进行开发

   插件：一般为解决某个问题存在，功能单一，比较小

   前端框架有：**BootStrap，Vue，Angular，React等**，PC移动端都可

   前端常用移动端插件：**swiper，superslide，iscroll**

## 本地存储

### 本地存储特性

1. 数据存储在用户浏览器中
2. 设置、读取方便，甚至页面刷新不丢失数据
3. 容量较大，sessionStorage约5M，localStorage约20M
4. 只能存字符串，可将对象JSON.stringify()编码后存储

### window.sessionStorage

1. 生命周期为关闭浏览器窗口
2. 在同一个窗口（页面）下数据可以共享
3. 以键值对的形式存储使用

#### 存储数据

```html
sessionStorage.setItem(key,value)
```

#### 获取数据

```html
sessionStorage.getItem(key)
```

#### 删除数据

```html
sessionStorage.removeItem(key)
```

#### 删除所有数据

```html
sessionStorage.clear()
```


### window.localStorage

1. 生命周期永久生效，除非手动删除否则关闭页面也会存在
2. 可多窗口（页面）共享（同一浏览器也可共享）
3. 以键值对形式存储使用

#### 存储数据

```html
localStorage.setItem(key,value)
```

#### 获取数据

```html
localStorage.getItem(key)
```

#### 删除数据

```html
localStorage.removeItem(key)
```

#### 删除所有数据

```html
localStorage.clear()
```
