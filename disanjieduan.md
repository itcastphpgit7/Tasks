# html标签

### hmtl自己的语法格式



     <html>   
         <head>
             <title></title>
         </head>
          <body>
          </body>
    </html>
### 文字类标签

文字容器：h1~h6（标题标签）；p（段落标签）
文字修饰：斜体（em，i）黑体（b，strong）细体（small）换行（br）删除线（del）<center></center>(居中)

### 布局类标签

div：块容器 （占一行）（h4)
span：内联容器

### 图像标签<img/>

src:图片来源
alt：用来代替的文本

### 表格标签

<table></table>定义表格
<th></th>      定义表格表头单元格（文字会居中加粗）
<tr></tr>      定义表格中的行
<td></td>      定义表格中的单元

##### 块级元素：占一行；行内元素：一行里不下

# css

css:与html合作，html负责控制网页的结构，css负责控制网页的表现
css选择器：每一条css样式定义由两部分组成，形式如下：【code】选择器{样式}【/code】，简而言之，就是使用css对html进行一对一，一对多的控制
修改方式（属性：值；）：例如；<style>选择器{      color：颜色；}
                                                                 </style>

### 字体样式属性

字号大小：font- size
字体：font -family

### 盒子模型

盒子边框（border）：border-width   border-style   border-color，其中border-style包括了solid（实线）dashed（虚线）dotted（点线）double（双实线）

# outline

| [outline](https://www.runoob.com/cssref/pr-outline.html)     | 在一个声明中设置所有的轮廓属性 | *outline-color outline-style outline-width *inherit          | 2    |
| ------------------------------------------------------------ | ------------------------------ | ------------------------------------------------------------ | ---- |
| [outline-color](https://www.runoob.com/cssref/pr-outline-color.html) | 设置轮廓的颜色                 | *color-name hex-number rgb-number *invert inherit            | 2    |
| [outline-style](https://www.runoob.com/cssref/pr-outline-style.html) | 设置轮廓的样式                 | none dotted dashed solid double groove ridge inset outset inherit | 2    |
| [outline-width](https://www.runoob.com/cssref/pr-outline-width.html) | 设置轮廓的宽度                 | thin<br/>medium<br/>thick<br/>*length<br/>*inherit           | 2    |

## margin 

可以单独改变元素的上，下，左，右边距，也可以一次改变所有的属性。

| 值       | 说明                                        |
| :------- | :------------------------------------------ |
| auto     | 设置浏览器边距。 这样做的结果会依赖于浏览器 |
| *length* | 定义一个固定的margin（使用像素，pt，em等）  |
| *%*      | 定义一个使用百分比的边距                    |

![Remark](https://www.runoob.com/images/lamp.gif) Margin可以使用负值，重叠的内容。

## padding（内边距）

| 值       | 说明                                |
| :------- | :---------------------------------- |
| *length* | 定义一个固定的填充(像素, pt, em,等) |
| *%*      | 使用百分比值定义一个填充            |

在CSS中，它可以指定不同的侧面不同的填充

### javascript

JavaScript 是一个脚本语言。它是一个轻量级，但功能强大的编程语言。

1,在HTML中必须在<script> 与 </script> 标签之间。

也可以在<boby>和<head>

### 变量：

- 变量必须以字母开头

- 变量也能以 $ 和 _ 符号开头（不过我们不推荐这么做）

- 变量名称对大小写敏感（y 和 Y 是不同的变量）

  当您声明新变量时，可以使用关键词 "new" 来声明其类型：

  var carname=new String;
  var x=   new Number;
  var y=   new Boolean;
  var cars=  new Array;
  var person= new Object;

#### 对象

对象是变量的容器

对象的方法定义了一个函数，并作为对象的属性存储。

对象方法通过添加 () 调用 (作为一个函数)。

该实例访问了 person 对象的 fullName() 方法:

#### 数据类型

基本数据类型：undefined,null,boolean,number,string
复杂数据类型：object

#### 运算符的应用

可以参考 c语言





## 




​       



