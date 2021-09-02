# BFC

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
