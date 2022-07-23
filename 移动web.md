# 移动端基础

### 视口

视口（viewport）就是浏览器显示页面内容的屏幕区域。视口可以分为布局视口、视觉视口和理想视口

#### 布局视口layout viewport

一般移动设备的浏览器都默认设置了一个布局视口，用于解决早期的PC端页面在手机上显示的问题。
iOS, Android基本都将这个视口分辨率设置为980px，所以PC上的网页大多都能在手机上呈现，只不过元素看上去很小，一般默认可以通过手动缩放网页。

#### 视觉视口visual viewport

字面意思，它是用户正在看到的网站的区域。注意：是网站的区域。

我们可以通过缩放去操作视觉视口，但不会影响布局视口，布局视口仍保持原来的宽度。

#### 理想视口ideal viewport

为了使网站在移动端有最理想的浏览和阅读宽度而设定

理想视口，对设备来讲，是最理想的视口尺寸

需要手动添写meta视口标签通知浏览器操作

meta视口标签的主要目的：布局视口的宽度应该与理想视口的宽度一致，简单理解就是设备有多宽，我们布局的视口就多宽

总结

视口就是浏览器显示页面内容的屏幕区域

视口分为布局视口、视觉视口和理想视口

我们移动端布局想要的是理想视口就是手机屏幕有多宽，我们的布局视口就有多宽

想要理想视口，我们需要给我们的移动端页面添加meta视口标签

### meta视口标签

```css
<meta name="viewport" content="width=device-width, user-scalable=no,initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

![image-20220720110344466](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220720110344466.png)

#### 标准的viewport设置

视口宽度和设备保持一致

视口的默认缩放比例1.0

不允许用户自行缩放

最大允许的缩放比例1.0

最小允许的缩放比例1.0

### 二倍图

#### 物理像素&物理像素比

物理像素点指的是屏幕显示的最小颗粒，是物理真实存在的。这是厂商在出厂时就设置好了,比如苹果6\7\8 是 750* 1334

我们开发时候的1px 不是一定等于1个物理像素的

PC端页面，1个px 等于1个物理像素的，但是移动端就不尽相同

一个px的能显示的物理像素点的个数，称为物理像素比或屏幕像素比

### 多倍图

对于一张50px * 50px 的图片,在手机Retina 屏中打开，按照刚才的物理像素比会放大倍数，这样会造成图片模糊

在标准的viewport设置中，使用倍图来提高图片质量，解决在高清设备中的模糊问题

通常使用二倍图，因为iPhone 6\7\8 的影响,但是现在还存在3倍图4倍图的情况，这个看实际开发公司需求

背景图片注意缩放问题

```css
/*在iphone8下面*/
img{
    /*原始图片100*100px*/
    width: 50px;
    height: 50px;
}
.box{
    /*原始图片100*100px*/
    background-size: 50px 50px;
}
```

### 背景缩放background-size

background-size 属性规定背景图像的尺寸

```css
background-size:背景图片宽度 背景图片高度;
```

单位：长度|百分比|cover|contain;

cover把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。

contain把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域

## 移动端开发选择

### 移动端主流方案

#### 单独移动端页面（主流）

通常情况下，网址域名前面加m(mobile)可以打开移动端。通过判断设备，如果是移动设备打开，则跳到移动端页面。

#### 响应式兼容PC移动端

三星电子官网：www.samsung.com/cn/ ，通过判断屏幕宽度来改变样式，以适应不同终端。

缺点：制作麻烦，需要花很大精力去调兼容性问题

## 移动端技术解决方案

### 移动端浏览器

移动端浏览器基本以 webkit 内核为主，因此我们就考虑webkit兼容性问题。我们可以放心使用H5 标签和CSS3 样式。

同时我们浏览器的私有前缀我们只需要考虑添加 webkit 即可

![image-20220720111641410](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220720111641410.png)

### CSS初始化normalize.css

移动端CSS 初始化推荐使用 normalize.css

Normalize.css：保护了有价值的默认值

Normalize.css：修复了浏览器的bug

Normalize.css：是模块化的

Normalize.css：拥有详细的文档

### CSS3 盒子模型box-sizing

传统模式宽度计算：盒子的宽度 = CSS中设置的width + border + padding

CSS3盒子模型：盒子的宽度 = CSS中设置的宽度width 里面包含了 border 和 padding也就是说，我们的CSS3中的盒子模型，padding 和 border 不会撑大盒子了

```css
/*CSS3盒子模型*/
box-sizing: border-box;
/*传统盒子模型*/
box-sizing: content-box;
```

**传统/CSS3盒子模型？**

移动端可以全部CSS3 盒子模型

PC端如果完全需要兼容，我们就用传统模式，如果不考虑兼容性，我们就选择 CSS3 盒子模型

### 特殊样式

```css
/*CSS3盒子模型*/
box-sizing: border-box;
-webkit-box-sizing: border-box;
/*点击高亮我们需要清除清除设置为transparent完成透明*/
-webkit-tap-highlight-color: transparent;
/*移动端浏览器默认外观在iOS上加上这个属性才能给按钮和输入框自定样式*/
-webkit-appearance: none;
/*禁用长按页面时的弹出菜单*/
img,a { -webkit-touch-callout: none; }
```

### 移动端常见布局

#### 移动端技术选型

1. 单独制作移动端页面（主流）

   流式布局（百分比布局）

   flex 弹性布局（强烈推荐）

   less+rem+媒体查询布局

   混合布局

2. 响应式页面兼容移动端（其次）

   媒体查询

   bootstarp

#### 流式布局（百分比布局）

流式布局，就是百分比布局，也称非固定像素布局。

通过盒子的宽度设置成百分比来根据屏幕的宽度来进行伸缩，不受固定像素的限制，内容向两侧填充。

流式布局方式是移动web开发使用的比较常见的布局方式

max-width最大宽度（max-height 最大高度）

min-width最小宽度（min-height 最小高度）

**二倍精灵图做法**

在firework里面把<u>精灵图等比例缩放为原来的一半</u>

之后根据<u>大小测量坐标</u>

注意代码里面<u>background-size也要写：**精灵图原来宽度的一半**</u>

------

# flex布局

flex 弹性布局

操作方便，布局极为简单，移动端应用很广泛

PC 端浏览器支持情况较差

IE 11或更低版本，不支持或仅部分支持

布局原理

flex 是flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为flex 布局。

当我们为父盒子设为flex 布局以后，子元素的float、clear和vertical-align属性将失效。

伸缩布局=弹性布局=伸缩盒布局=弹性盒布局=flex布局

### 总结

#### flex布局原理：就是通过给父盒子添加flex属性，来控制子盒子的位置和排列方式

### flex布局父项常见属性

#### flex-direction设置主轴的方向

##### 1.主轴与侧轴

在flex布局中，是分为主轴和侧轴两个方向，同样的叫法有：行和列、x轴和y轴

默认主轴方向就是x轴方向，水平向右

默认侧轴方向就是y轴方向，水平向下

![image-20220721170740012](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721170740012.png)

flex-direction属性决定主轴的方向（即项目的排列方向）

注意：主轴和侧轴是会变化的，就看flex-direction设置谁为主轴，剩下的就是侧轴。而我们的子元素是跟着主轴来排列的

![image-20220721170801940](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721170801940.png)

####  justify-content设置主轴上的子元素排列方式

justify-content 属性定义了项目在主轴上的对齐方式

**注意：使用这个属性之前一定要确定好主轴是哪个**

![image-20220721170912605](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721170912605.png)

#### flex-wrap设置子元素是否换行

默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，flex布局中默认是不换行的。

![image-20220721170933413](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721170933413.png)

#### align-items设置侧轴上的子元素排列方式（单行）

该属性是控制子项在侧轴（默认是y轴）上的排列方式 在子项为单项（单行）的时候使用

![image-20220721171002829](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721171002829.png)

#### align-content 设置侧轴上的子元素的排列方式（多行）

设置子项在侧轴上的排列方式并且只能用于子项出现换行的情况（多行），在单行下是没有效果的。

![image-20220721171031413](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721171031413.png)

#### align-content和align-items 区别

align-items 适用于单行情况下，只有上对齐、下对齐、居中和拉伸

align-content 适应于换行（多行）的情况下（单行情况下无效），可以设置上对齐、下对齐、居中、拉伸以及平均分配剩余空间等属性值。

总结就是单行找align-items 多行找align-content

![image-20220721171107853](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220721171107853.png)

#### flex-flow

flex-flow 属性是flex-direction 和flex-wrap 属性的复合属性

```css
flex-flow:row wrap;
```

flex-direction：设置主轴的方向

justify-content：设置主轴上的子元素排列方式

flex-wrap：设置子元素是否换行

align-content：设置侧轴上的子元素的排列方式（多行）

align-items：设置侧轴上的子元素排列方式（单行）

flex-flow：复合属性，相当于同时设置了flex-direction 和 flex-wrap

## flex布局子项常见属性

#### flex 属性

flex 属性定义子项目分配剩余空间，用flex来表示占多少份数。

```css
.item {
	flex: <number>; /* default 0 */
}
```

####  align-self控制子项自己在侧轴上的排列方式

align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```css
span:nth-child(2) {
    /*设置自己在侧轴上的排列方式*/
	align-self: flex-end;
}
```

#### order属性定义项目的排列顺序

数值越小，排列越靠前，默认为0。

注意：和 z-index 不一样。

```css
.item {
	order: <number>;
}
```

------

### 属性选择器改图片

```css
/* 属性选择器改图片 */
.local-nav li [class^="local-nav-icon"]{
    width: 32px;
    height: 32px;
    background: url(../images/localnav_bg.png) no-repeat 0 0;
    background-size: 32px auto;
}
.local-nav li .local-nav-icon-icon2{
    background: url(../images/localnav_bg.png) no-repeat 0 -32px;
    background-size: 32px auto;
}
.local-nav li .local-nav-icon-icon3{
    background: url(../images/localnav_bg.png) no-repeat 0 -64px;
    background-size: 32px auto;
}
.local-nav li .local-nav-icon-icon4{
    background: url(../images/localnav_bg.png) no-repeat 0 -96px;
    background-size: 32px auto;
}
.local-nav li .local-nav-icon-icon5{
    background: url(../images/localnav_bg.png) no-repeat 0 -128px;
    background-size: 32px auto;
}
```

```html
<ul class="local-nav">
    <li>
        <a href="#" title="景点·玩乐">
            <span class="local-nav-icon-icon1"></span>
            <span>景点·玩乐</span>
        </a>
    </li>
    <li>
        <a href="#" title="景点·玩乐">
            <span class="local-nav-icon-icon2"></span>
            <span>景点·玩乐</span>
        </a>
    </li>
    <li>
        <a href="#" title="景点·玩乐">
            <span class="local-nav-icon-icon3"></span>
            <span>景点·玩乐</span>
        </a>
    </li>
    <li>
        <a href="#" title="景点·玩乐">
            <span class="local-nav-icon-icon4"></span>
            <span>景点·玩乐</span>
        </a>
    </li>
    <li>
        <a href="#" title="景点·玩乐">
            <span class="local-nav-icon-icon5"></span>
            <span>景点·玩乐</span>
        </a>
    </li>
</ul>
```

### 背景线性渐变

![image-20220723122057841](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220723122057841.png)

```css
background: linear-gradient(起始方向,颜色1,颜色2,...);
background: -webkit-linear-gradient(left, red,blue);
background: -webkit-linear-gradient(left,top,red,blue);
```

背景渐变必须添加浏览器私有前缀

起始方向可以是：方位名词 或者度数，如果省略默认就是top

------

# rem适配布局

### rem 基础

#### 1.rem 单位

rem (root em)是一个相对单位，类似于em，em是父元素字体大小。

不同的是**rem**的基准是相对于**html元素的字体大小**。

比如，根元素（html）设置font-size=12px; 非根元素设置width:2rem;则换成px表示就是24px。

rem的优势：父元素文字大小可能不一致，但是整个页面只有一个html，可以很好来控制整个页面的元素大小

```css
/*根html为12px */
html {
	font-size: 12px;
}
/*此时div的字体大小就是24px */
div {
	font-size: 2rem;
}
```

#### 2.媒体查询

媒体查询（Media Query）是CSS3新语法。

使用@media 查询，可以针对不同的媒体类型定义不同的样式

**@media 可以针对不同的屏幕尺寸设置不同的样式**

当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面

目前针对很多苹果手机、Android手机，平板等设备都用得到多媒体查询

```css
#在屏幕（mediatype=screen）上 并且（and） 最大宽度8px（(max-width:8px)）
@media mediatype and|not|only (media feature) {
	CSS-Code;
}
```

用@media 开头注意@符号

mediatype 媒体类型

关键字and not only

media feature媒体特性必须有小括号包含

1. mediatype 查询类型

   将不同的终端设备划分成不同的类型，称为媒体类型

![image-20220723150241836](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220723150241836.png)

2. 关键字

   关键字将媒体类型或多个媒体特性连接到一起做为媒体查询的条件。

   and：可以将多个媒体特性连接到一起，相当于“且”的意思。

   not：排除某个媒体类型，相当于“非”的意思，可以省略。

   only：指定某个特定的媒体类型，可以省略。

3. 媒体特性

   每种媒体类型都具体各自不同的性，根据不同媒体类型的媒体特性设置不同的展示风格。我们暂且了解三个。注意他们要加小括号包含

![image-20220723150625282](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220723150625282.png)

#### <u>注意：为了防止混乱，媒体查询我们要按照从小到大或者从大到小的顺序来写,但是我们最喜欢的还是从小到大来写，这样代码更简洁</u>

##### <u>媒体查询+rem实现元素</u>动态大小变化

rem单位是跟着html来走的，有了rem页面元素可以设置不同大小尺寸

媒体查询可以根据不同设备宽度来修改样式

媒体查询+rem 就可以实现不同设备宽度，实现页面元素大小的动态变化

###### 引入资源（理解）

当样式比较繁多的时候，我们可以针对不同的媒体使用不同 stylesheets（样式表）。

原理，就是直接在link中判断设备的尺寸，然后引用不同的css文件。

```css
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
eg.
<link rel="stylesheet" href="styleA.css" media="screen and (min-width: 400px)">
```

### 3.Less 基础

##### Less是一门 CSS 预处理语言，它扩展了CSS的动态特性。

![image-20220723151559278](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220723151559278.png)

####  Less 变量

变量是指没有固定的值，可以改变的。因为我们CSS中的一些颜色和数值等经常使用。

```css
@变量名:值;
eg.
@color: pink;
```

1. 变量命名规范

   必须有@为前缀

   不能包含特殊字符

   不能以数字开头

   大小写敏感

2. 变量使用规范

   ```css
   //直接使用
   body{
   	color:@color;
   }
   a:hover{
   	color:@color;
   }
   ```

#### Less 编译

本质上，Less包含一套自定义的语法及一个解析器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的CSS 文件。

所以，我们需要把我们的less文件，编译生成为css文件，这样我们的html页面才能使用。

##### Less 嵌套

我们经常用到选择器的嵌套

```css
#header .logo {
	width: 300px;
}
/* Less 嵌套写法 */
#header {
	.logo {
		width: 300px;
	}
}
```

如果遇见（交集|伪类|伪元素选择器）

内层选择器的前面没有 & 符号，则它被解析为父选择器的后代；

如果有 & 符号，它就被解析为父元素自身或父元素的伪类。

##### Less 嵌套写法

```css
a:hover{
	color:red;
}
a{
	&:hover{
		color:red;
	}
}
```

####  Less 运算

任何数字、颜色或者变量都可以参与运算。就是Less提供了加（+）、减（-）、乘（*）、除（/）算术运算。

```css
/*Less里面写*/
@witdh: 10px + 5;
div {
	border: @witdh solid red;
}
/*生成的css*/
div {
	border: 15px solid red;
}
/*Less甚至还可以这样*/
width: (@width + 5) * 2;
```

注意：

乘号（*****）和除号（**/**）的写法

**运算符中间左右有个空格隔开1px + 5**

对于两个不同的单位的值之间的运算，运算结果的值取第一个值的单位

如果两个值之间只有一个值有单位，则运算结果就取该单位

------

### rem 适配方案

1.让一些不能等比自适应的元素，达到当设备尺寸发生改变的时候，等比例适配当前设备。

2.使用媒体查询根据不同设备按比例设置html的字体大小，然后页面元素使用rem做尺寸单位，当html字体大小变化元素尺寸也会发生变化，从而达到等比缩放的适配。

- ①按照设计稿与设备宽度的比例，动态计算并设置 html 根标签的 font-size 大小；（媒体查询）
- ②CSS 中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为 rem 为单位的值；

#### rem 适配方案技术使用（市场主流）

技术方案1

​	less

​	媒体查询

​	rem

技术方案2（推荐）

​	flexible.js

​	rem