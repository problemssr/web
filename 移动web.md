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

在firework里面把精灵图等比例缩放为原来的一半

之后根据大小测量坐标

注意代码里面background-size也要写：精灵图原来宽度的一半