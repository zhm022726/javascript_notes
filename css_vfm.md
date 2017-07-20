# CSS Box Model盒模型

# Visual Formatting Model

CSS中的visual formatting model(视觉格式化模型)是一种处理文档并把它显示在可视化媒体上的算法。这是CSS中的一个基础概念。visual formatting model把文档的每一个元素转换成0个，1个或多个符合CSS盒模型的盒子，每个盒子的布局内容包括如下部分：

- 盒子尺寸：明确指定受限制或不指定
- 盒子类型：行内，行内级，原子行内级，块盒
- 定位方案：包括正常文档流，float或者绝对定位
- 节点树的其他元素：其子元素或兄弟元素
- viewport（视窗）的尺寸和定位
- 内含图片的固有尺寸
- 其他额外信息

visual formatting model相对于包含块的边界来渲染盒子，通常，一个盒子为它的后代元素建立包含块。然而一个盒子并不受其包含块限制，当一个盒子的内容超出其包含块时，就是我们通常所说的溢出（overflow）。

## 盒子的生成

----
CSS visual formatting model从文档元素生成盒子，生成的盒子有多种类型，其类型会影响visual formatting model的行为。生成盒子的类型取决于元素CSS属性display的值。

### 块级元素和块盒子

当元素的CSS属性display计算值是block，list-item或table的时候，这个元素就是块级元素。一个块级元素会被视觉格式化成一个块（block），按照垂直方向排列。

#### 主要块级盒（principal block-level box）

每个块级盒子都参与Block Formatting Context(块级格式化上下文)。每个块级元素(block-level element)至少生成一个块级盒子，即主要块级盒，大多数元素只生成一个主要块级盒，而有一些元素，如li列表，则会生成多个盒子，包括主要块级盒及描述排版信息或项目符号的其他盒子。

主要块级盒包括包括后代元素生成的盒子及生成的内容，我们可以使用之前谈到的定位方案定位该盒子。

#### 块容器盒（block container box）

块容器盒只包含其他块级盒或生成一个行内格式化上下文，即只包含行内盒。我们必须明白块级盒和块容器盒两个概念不冲突。块级盒描述盒子与它的父级和兄弟元素之间的行为，块容器盒描述它与其后代元素之间如何相互作用。块级盒也可能是一个块容器盒。一些块级盒，比如表格，不是块级容器盒；相反地，一些块级容器盒，比如非置换行内块和非置换表格单元格也不是块级盒。

#### 块盒

块级盒中也是块容器盒的盒子，是块盒（block box）。

#### 匿名块盒

在某些情况下，visual formatting model 需要添加一些辅助性盒子，但是CSS选择器不能选中这些盒子，这些盒子叫做匿名盒子（anonymous box）.

不能使用CSS选择器选择匿名盒子，说明不能给他们定义样式，这意味着所有可继承属性都继承自父元素，所有不可继承属性都是其初始值。

##### 匿名块盒实例

块容器盒只能包含块级盒或行内级盒，但是，通常在一个文档中，包含这两种类型盒子，此时，在行内级盒子前后创建匿名块盒。

```

    <div>我是第一个匿名块盒的内容<p>我是块级盒子的内容</p>我是第二个匿名块盒的内容</div>
```

如上HTML代码，效果如下：

![匿名块盒]()





