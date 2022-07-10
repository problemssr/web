## 基础选择器

#### 标签选择器(按标签名称分类，为页面中某一类标签指定统一的CSS 样式。)

```css
标签名{
	属性1:属性值1;
	属性2:属性值2;
    属性3:属性值3;
}
```

#### 类选择器(差异化选择不同的标签，单独选一个或者某几个标签，可以使用类选择器.)

```css
.类名{
	属性1:属性值1;
	属性2:属性值2;
    属性3:属性值3;
}
<div class=‘red’>变红色</div>
```

## **样式点定义，结构类调用。一个或多个，开发最常用。**

**多类名**

(1)在标签class 属性中写多个类名

(2)多个类名中间必须用空格分开

(3)这个标签就可以分别具有这些类名的样式

```css
    <div class="red big"></div>
```

#### id 选择器(标有特定id 的HTML 元素指定特定的样式。)

```css
#nav
{
color:red;
}
    <div id="hhh">hhhh</div>
```

## 样式#定义,结构id调用, 只能调用一次, 别人切勿使用

#### 通配符选择器

通配符选择器使用“*”定义，它表示选取页面中所有元素（标签）。

```css
*{
  color:red;  
}

//清除所有的元素标签的内外边距
*{
	margin: 0;
	padding: 0;
}
```

![image-20220709152116488](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709152116488.png)

## 字体属性

font-family 属性定义文本的字体系列。

font-size 属性定义字体大小。

font-weight属性设置文本字体的粗细。

font-style属性设置文本的风格。**(很少给文字加斜体，反而要给斜体标签（em，i）改为不倾斜字体。)**

```css
p { font-family:"微软雅黑";}
p { font-size:20px;}
p { font-weight: bold;}
p { font-style: normal;}
```

**字体复合属性(保留font-size 和font-family 属性，否则font 属性将不起作用)**

```css
p { font: font-style font-weight font-size/line-height font-family;}
```

## 文本属性

**文本颜色**

color属性用于定义文本的颜色。

**对齐文本**

text-align 属性用于设置元素内文本内容的水平对齐方式。

**装饰文本**

text-decoration 属性规定添加到文本的修饰。可以给文本添加下划线、删除线、上划线等。

**文本缩进**

text-indent 属性用来指定文本的第一行的缩进，通常是将段落的首行缩进。

**行间距**

line-height 属性用于设置行间的距离（行高）。可以控制文字行与行之间的距离.

```css
p {
    color: red;
    text-align: center;
    text-decoration：underline;(下划线)
    text-indent: 10px;
	line-height: 26px;
}
```



![image-20220709153625174](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709153625174.png)

## 引入方式

*1.内部样式表（嵌入式）*

```css
<style>
	div{
	color: red;
	font-size: 12px;
	}
</style>
```

方便控制当前整个页面中的元素样式设置

代码结构清晰，但是并没有实现结构与样式完全分离

使用内部样式表设定CSS，通常也被称为嵌入式引入，这种方式是我们练习时常用的方式

*2.行内样式表（行内式）*

```css
<div style="color: red; font-size: 12px;">
青春不常在，
抓紧谈恋爱
</div>
```

行内样式表（内联样式表）是在元素标签内部的style 属性中设定CSS 样式。适合于修改简单样式.

不推荐大量使用，只有对当前元素添加简单样式的时候，可以考虑使用

*3.外部样式表（链接式）*

```css
<link rel="stylesheet" href="css文件路径">
```

实际开发都是外部样式表. 适合于样式比较多的情况. 核心是:样式单独写到CSS 文件中，之后把CSS文件引入到HTML 页面中使用.

1. 新建一个后缀名为.css 的样式文件，把所有CSS 代码都放入此文件中
2. 在HTML 页面中，使用<link> 标签引入这个文件。

![image-20220709162050053](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709162050053.png)

# 注意：想让img居中需要对其父元素设置align