# BFC
BFC的全称是Block Formatting Context，块级格式化上下文，是一个独立的渲染区域。
BFC会有以下特性：
1. 同属一个BFC的上下相邻元素，会发生margin重叠，即两个元素之间的距离由较大的margin决定
2. 计算bfc的高度，浮动元素也参与计算
3. bfc区域不会与浮动元素重叠
4. 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

如何生成BFC元素
1. 根元素
2. position属性为absolute, fixed
3. float属性不为none
4. overflow不为visible,
5. display为inline-block, table-cell, table-caption, flex, inline-flex

# 上下左右居中
1. 使用绝对定位
```
position: absolute;
left: 50%;
top: 50%;
transform: translate(-50%, -50%);
```
2. flex
```
display: flex;
align-items: center;
justify-content: center;
```

# flex布局
```
display: flex;
```
容器属性
```
flex-direction: row|column|row-reverse|column-reverse
flex-wrap: no-wrap|wrap|wrap-reverse
flex-flow: flex-direction和flex-wrap简写集合
justify-content: flex-start|flex-end|space-between|space-round|space-evenly|center
align-items: stretch|center|flex-start|flex-end|baseline
align-content: flex-start|flex-end|center|space-between|space-around|space-evenly|stretch
```
项目属性
```
order:
flex-grow: 默认0|项目在有剩余空间的情况下是否放大
flex-shrink: 默认1|项目在空间不足时是否缩小
flex-basis: 项目宽度
flex: 默认0 1 auto|flex-grow，flex-shrink与flex-basis集合
align-self: auto(默认)|flex-start|flex-end|center|baseline|stretch
```

# 重绘，重排
1. 元素的宽高，位置，隐藏等会引起页面布局发生变化的属性变动时，浏览器需要重新计算元素的位置，就会发生重绘
2. 元素的颜色，透明度等不会导致页面布局发生变化，则浏览器会进行重绘

如何优化重排
1. 通过变更class的方式批量修改样式
2. 循环添加子元素的时候，先让父元素隐藏，批量添加完成后再显示
3. 同时创建多个节点，通过documentFargment一次添加
4. 一个元素不可避免的会引起多次重排，先让其脱离文档流
5. 使用布局信息，先将其缓存起来，避免多次访问dom

# 盒模型
盒模型就是把页面上的元素看作一个个的盒子，盒模型分为两种
1. w3c标准盒模型：只包含content部分
2. ie盒模型：包含content，padding，border  
设置width属性，对于两种盒模型表现是不同的
标准盒模型就指content部分的宽度，如果再设置padding属性，则盒子整体宽度会比设置的width要宽
ie盒模型则是指content+padding+border的整体宽度

通过box-sizing可以统一盒模型的展示（content, border-box）

# 选择器权重
内联样式：1000
id选择器：0100
类选择器，伪类选择器，属性选择器：0010
标签选择器，伪元素选择器：0001
子选择器，相邻选择器：0000
继承：无

!important：最优先

权重的计算方式：
每个选择器叠加计算，最终对权重进行比较，且1,0,0,0 > 0,99,99,99

例如：
```
/* 权重0,1,0,0 */
#demo {
}
/* 权重0,0,1,2 */
.class div a {
}
/* 权重0,1,0,1 */
#demo tag {
}
```

## position
1. static: 元素在文档流中的当前位置不变
2. fixed：元素相对于屏幕定位，不给元素预留位置
3. relative： 给元素预留位置，元素相对于自身进行偏移，偏移后在原位置会留下空白
4. absolute：不给元素预留位置，相对于最近的position的值为fixed,relative,absolute,sticky的祖先元素定位
5. sticky：
