# HTML(5)

# CSS(3)

## 选择器

CSS(3)中提供的选择器手册（w3school）：http://www.w3school.com.cn/cssref/css_selectors.asp

### 比较常用的几种选择器：

| 选择器     | 例子                                                         |
| ---------- | ------------------------------------------------------------ |
| 类选择器   | .class                                                       |
| 标签选择器 | element                                                      |
| id选择器   | #id                                                          |
| 后代选择器 | element_1 element_2：选择 element_1 内部的全部 element_2 元素 |
| 子代选择器 | element_1>element_2：选择以 element_1 为父元素的全部 element_2 元素 |
| 群组选择器 | element_1,element_2：选择 element_1 和 element_2 ……          |
| 相邻选择器 | element_1+element_2：选择与 element_1 相邻的，并且元素类型为 element_2 的元素，相邻和E类型，两个条件都要满足，缺一不可 |
| 兄弟选择器 | element_1~element_2：选择element_1的兄弟元素，且元素类型为 element_2 |



### 属性选择器

| 例子        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| [attr]      | 选择存在attr属性的元素，如果想要限制元素类型，则可以写成 E[attr]，下同 |
| [attr=val]  | 选择属性值完全等于val的元素，引号可加可不加                  |
| [attr*=val] | 选择属性值里包含val字符的元素                                |
| [attr^=val] | 选择属性值里以val字符开头的元素                              |
| [attr$=val] | 选择属性值里以val字符结尾的元素                              |



### 伪类选择器

#### 超链接伪类选择器

| 例子      | 说明                      |
| --------- | ------------------------- |
| a:link    | 定义a元素未访问时的样式   |
| a:visited | 定义a元素访问后的样式     |
| a:hover   | 定义鼠标经过a元素时的样式 |
| a:active  | 定义鼠标点击激活时的样式  |

注意：

1. 在定义这四个伪类的时候，要按照 link、visited、hover、active 的顺序进行，即“爱恨原则”——“LoVe HAte”。
2. hover 伪类并不限用于 a 元素，它可以定义任何一个元素在鼠标经过时的样式。



#### 相对于父元素的结构伪类

| 例子                | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| E:first-child       | 查找E这个元素的父元素的第一个子元素E，如果第一个子元素不是E类型，则查找无效 |
| E:last-child        | 查找E这个元素的父元素的最后一个子元素E，如果最后一个子元素不是E类型，则查找无效 |
| E:nth-child(n)      | 查找E这个元素的父元素的第n个子元素E（注意索引是从1开始的，第一个的索引就是1，不要下意识以为第一个的索引是0），如果第n个子元素不是E类型，则查找无效；n也可以是关键字或表达式，见下 |
| E:nth-last-child(n) | 同E:nth-child(n) 相似，只是倒着计算                          |
| E:nth-child(even)   | 此处n就是取关键字even，表示偶数项的元素                      |
| E:nth-child(odd)    | 此处n就是取关键字odd，表示奇数项的元素                       |
| E:empty             | 选中没有任何子节点的E元素，注意，空格也算子元素              |
| E:target            | 结合锚点进行使用，处于当前锚点的元素会被选中                 |


上面的选择器我们可以发现到一个很大的缺点，就是在查找的过程中并没有将元素类型限制成我们想要查找的E类型。因此，一旦查找到的元素不是E类型的元素，则查找无效，这在变化多端的动态数据中是极其容易出现的。因此，CSS3又提供了更为实用的选择器：

| 例子             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| E:first-of-type  | 查找E元素的父元素的第一个E类型的元素，查找的时候只会查找满足E类型的元素，过滤掉其它类型的元素 |
| E:last-of-type   | 查找E元素的父元素的最后一个E类型的元素，查找的时候只会查找满足E类型的元素，过滤掉其它类型的元素 |
| E:nth-of-type(n) | 查找E元素的父元素的第n个E类型的元素，查找的时候只会查找满足E类型的元素，过滤掉其它类型的元素 |

需要重点说明的是关于 nth-child(n) 和 nth-of-type(n) 中的n，它遵循线性变化，取值范围为0~查找元素的长度。但是当 n≤0 时，选取是无效的。如当 n 是一个表达式，nth-of-type(-n+5) 表示查找 nth-of-type(5)、nth-of-type(4)、nth-of-type(3)、nth-of-type(2)、nth-of-type(1)，即查找前五个子元素 。


### 伪元素选择器

| 例子            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| E::before       | 定义在一个元素之前插入 content 属性定义的内容和样式          |
| E::after        | 定义在一个元素之前插入 content 属性定义的内容和样式          |
| E::first-letter | 文本的第一个字母或字(不是词组)                               |
| E::first-line   | 文本第一行；如果设置了::first-letter，那么无法同时设置::first-line的样式 |
| E::selection    | 可改变选中文本的样式；它只能设置显示的样式，而不能设置内容大小 |


E::before、E::after：分别定义在一个元素之前和之后插入 content 属性定义的内容和样式。注意：

1. 是一个行内元素，需要通过以下三种方法转换成块元素：float、display:block、position（常用）；

2. 必须添加 content:""，就算不设置内容；

3. 在CSS2中是伪类——E:before、E:after，在CSS3中是伪元素——E::before、E::after。在新版本下，E:after、E:before会被自动识别为E::after、E::before。但有时为了兼容处理，还是会写成E:after、E:before。



## CSS优先级算法

### 优先级比较

! important > 内联样式 > id > class > 标签 > 通配符 > 继承 > 默认

### 权重计算

我们把特殊性分为5个等级，每个等级代表一类选择器，每个等级的值为其所代表的选择器的个数乘以这一等级的权值，最后把所有等级的值相加得出选择器的特殊值。

5个等级的定义如下：

1. 第一等：代表内联样式，如: style=””，权值为1000。
2. 第二等：代表ID选择器，如：#content，权值为0100。
3. 第三等：代表类，伪类和属性选择器，如.content，权值为0010。
4. 第四等：代表标签选择器和伪元素选择器，如div p，权值为0001。
5. 第五等：通用选择器（*），子选择器（>），相邻同胞选择器（+），权值为0000

来看以下的**例子**：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <style>
		#content #in_block .user_info a{/*权重：100*2+10*1+1*1=211*/
			font-size: 21px;
			color: yellow;
		}
		#users_info #username{/*权重：100*2=200*/
		    font-size: 15px;
		    color: red;
		}
		#username{/*权重：100*1=100*/
		    font-size: 16px;
		    color: green; 
		}
		*{/* 权重为0 */
			font-size: 20px;
			color: blue;
		}
    </style>
    <body>
        <div class="contain" id="content" style="width: 200px;height: 200px;margin: 0 auto;background: #C4E3F3;">
            <div id="in_block" class="left_content">
                <div class="user_info" id="users_info">
                    <a id="username">注意我的字体大小和颜色</a>
                </div>
            </div>
        </div>
    </body>
</html>
```

