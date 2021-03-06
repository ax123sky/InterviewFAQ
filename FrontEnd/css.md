## IE盒模型和标准盒模型
### 标准盒模型
![](https://mdn.mozillademos.org/files/13647/box-model-standard-small.png)
width和height只包含content。

在IE中使用标准盒模型：
1. 添加文档声明 < !DOCTYPE html >
2. < meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" >

### IE盒模型
![](https://mdn.mozillademos.org/files/13649/box-model-alt-small.png)
width和height包含content、padding和border

在非IE中使用IE盒模型：在CSS中设置box-sizing属性为border-box（默认是content-box）

**最佳实践：**
```css
box-sizing: border-box;
-moz-box-sizing: border-box;
-webkit-box-sizing: border-box;
```
这样可以多浏览器兼容，保持一致。

----------
 
## 元素消失的四种CSS方法
```css
visibility: hidden;
opacity: 0;
position: absolute; left: -1000px;
display: none;
```
~~width: 0; height: 0;~~

~~z-index: -100;~~

----------
 
## 伪类和伪元素

## 长文本如何用CSS实现省略号

## BEM
BEM：**Block**，**Element**，**Modifier**。类似于OOP，BEM是一种用代码和一系列模式来描述现实情况的方法，只考虑程序实体，和程序语言无关。利用BEM原则可以指导网站的构建。遵循统一的原则和规范可以有助于团队协作和沟通。

![](/image/BEM.jpg)

### Block
一个块是一个独立的实体，如积木一般。块可以复合。下图是搜索块：

![](/image/block.jpg)

### Element
元素是块的一部分，具有一定的功能，依赖上下文。下图是搜索块中的输入域和按钮：

![](/image/element.jpg)

块和元素构成了页面内容，并且遵循着一定的顺序。为了描述页面布局，需要为每一个块和元素定义可识别的唯一关键字（一般是名字）。
### 块的独立性
随着项目发展，我们会在页面中添加、移动或者删除某些块，因此每个块必须是独立的，可以放置在页面的任何位置，包括嵌套在其他块中。
### CSS和BEM
从CSS的角度来看：
- 每一个块（或者元素）必须有一个唯一的名字（即CSS类名）。
- HTML元素不能作为CSS选择器，因为这样上下文相关，不独立。
- 尽量少用级联（cascade）选择器。

CSS命名方案（BEM原则）：
1. 块的CSS类名就是块的名字。
2. 一个元素的CSS类名是一个块名和元素名的组合，中间用两个下划线（B__E）。
3. 块名和元素名用连字符分割单词（block-name__element-name）。
### 块修饰符
我们经常需要创建一个和已存在的块相似的块，只是外观和行为有些许改变。为了避免重复开发，引入修饰符（***modifier***）的概念。修饰符作为块/元素的属性，代表块/元素在外观/行为上的改变。一个修饰符有一个名字和一个值。可以同时使用多个修饰符。

![](/image/modifier.jpg)
### 从HTML/CSS角度看修饰符
对于块/元素来说，修饰符就是附加的CSS类。我们用一个下划线来分隔块名（或元素名）和修饰符名，再用另一个下划线来分隔修饰符名和它对应的值。
```html
<ul class="menu menu_size_big menu_type_buttons">
  ...
</ul>
```
```css
.menu_size_big {  }
.menu_type_buttons .menu__item {  }
```
### 块的一致性
复用块不仅要实现相同的CSS，还要复用行为。

----------
 
## CSS3弹性布局
## BFC
## 元素居中
### 水平居中
inline 元素：`text-align: center`

block 元素：`margin: 0 auto`

多个block元素并排：
```html
<main class="inline-block-center">
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
</main>
```
```css
.inline-block-center {
  text-align: center;
}
.inline-block-center div {
  display: inline-block;
}
```
[测试效果](https://jsfiddle.net/w8kte3k9/)

用flexbox：
```css
.flex-center {
  display: flex;
  justify-content: center;
}
```
[测试效果](https://jsfiddle.net/w8kte3k9/2/)
### 垂直居中
#### inline 元素
- 一行元素：`padding-top` = `padding-bottom` or `line-height` = `height`
- 多行元素：
```html
<div class="center-table">
    <p>I'm vertically centered multiple lines of text in a CSS-created table layout.</p>
</div>
```
```css
/* 伪装成table的cell，设置vertical-align */
.center-table {
  display: table;
}
.center-table p {
  display: table-cell;
  vertical-align: middle;
}
```
[测试效果](https://jsfiddle.net/w8kte3k9/3/)

用flexbox：
```css
.flex-center-vertically {
  display: flex;
  justify-content: center;
  flex-direction: column;
}
```
[测试效果](https://jsfiddle.net/w8kte3k9/4/)
#### block 元素
知道需要居中元素的height：
```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  height: 50px;
  margin-top: -25px; /* height/2, account for padding and border if not using box-sizing: border-box */
}
```
[测试效果](https://jsfiddle.net/1vc637z4/1/)

不知道需要居中元素的height：
```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```
[测试效果](https://jsfiddle.net/1vc637z4/2/)

用flexbox：
```css
.parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
```
[测试效果](https://jsfiddle.net/1vc637z4/4/)
### 水平和垂直居中
固定宽度和高度的元素：
```css
.parent {
  position: relative;
}
.child {
  width: 80px;
  height: 40px;
  padding: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -30px 0 0 -50px; /* 原理和之前的相似，一半的宽/高 + padding */
}
```
[测试效果](https://jsfiddle.net/1vc637z4/6/)

未知宽度和高度：
```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```
[测试效果](https://jsfiddle.net/1vc637z4/8/)

用flexbox：
```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```
[测试效果](https://jsfiddle.net/1vc637z4/10/)

----------
