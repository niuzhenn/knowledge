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

# 盒模型
盒模型就是把页面上的元素看作一个个的盒子，盒模型分为两种
1. w3c标准盒模型：只包含content部分
2. ie盒模型：包含content，padding，border  
设置width属性，对于两种盒模型表现是不同的
标准盒模型就指content部分的宽度，如果再设置padding属性，则盒子整体宽度会比设置的width要宽
ie盒模型则是指content+padding+border的整体宽度

通过box-sizing可以统一盒模型的展示（content, border-box）
