## 表格结构

![image-20220709103937380](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709103937380.png)

**表头单元格th 表头文字会加粗**

**属性：cellpadding---设置单元边和内容空白距离**

​            **cellspacing---设置单元格与单元格之间空白**

**合并单元格**

跨行合并：rowspan="合并单元格个数"

跨列合并：colspan="合并单元格个数"

目标单元格：（绿色对钩为目标）

- 跨行：最上侧单元格为目标

- 跨列：最左侧单元格为目标

  ![image-20220709112741062](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709112741062.png)

**步骤**

1. **确定跨行还是跨列**
2. **找到目标单元格 colspan|rowspan**
3. **删除多余单元格**

## 列表标签

#### 无序列表（排列简单、整齐、无序）

```    html
 <ul>
		<li>1231</li>
        <li>231</li>
        <li>rewq</li>
 </ul>
```

**注意：**

1. **ul只能放li**
2. **li可以放任何标签**

####    自定义列表（围绕小标题说明）

```html
<dl>
    <dt>hhh</dt>
    <dd>why</dd>
    <dd>not</dd>
    <dt>lalla</dt>
    <dd>hurry</dd>
    <dt>la</dt>
    <dd>hunger</dd>
</dl>
```

dl---定义描述列表（只能放dt|dd） 	dt----项目名字 	dd---描述项目

![image-20220709113900398](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709113900398.png)

## 表单标签

#### input标签

name 的主要作用就是用于区别不同的表单。

![image-20220709134024290](C:\Users\22982\AppData\Roaming\Typora\typora-user-images\image-20220709134024290.png)

#### label标签（增大点击区域）

**<label> 标签的for 属性应当与相关元素的id 属性相同。**

label（for属性值）里面嵌入input（id属性值一样）

#### select标签（下拉）

在<option> 中定义selected =“selected " 时，当前项即为默认选中项。

#### textarea文本域

多行输入

------

**(1)表单域form使用场景: 提交区域内表单元素给后台服务器**

**(2)文件域file是input type 属性值使用场景: 上传文件**

**(3)文本域textarea使用场景: 可以输入多行文字, 比如留言板 网站介绍等…**