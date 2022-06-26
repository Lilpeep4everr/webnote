##布局原理
&emsp;&emsp;flex是flexible Box的缩写，意为“弹性布局”,用来为盒装模型提供最大的灵活性，任何一个容器都可以指定为flex布局。
* 当我们为父盒子设定为flex布局以后，子元素的float、clear、和vertical-align属性将失效。
* 伸缩布局=弹性布局=伸缩盒布局=弹性盒布局=flex布局
  
##flex布局父项常见属性
* Flex布局中默认的主轴是row，x轴
* 如果想改变主轴方向可通过设置flex-direction来改变
* flex-direction:column；将主轴改为y轴，纵轴
* flex-direction:row；将主轴改为x轴，横轴
* flex-direction:row-reverse；主轴为x轴，并且翻转
* flex-direction:column-reverse；主轴为y轴，并且翻转
-----
* 通过justify-content能够设置主轴子元素排列形式
* 值为flex-start所有子元素在主轴头部显示
* 值为flex-end所有子元素在主轴尾部显示
* 值为flex-center所有子元素在主轴居中对齐
* 值为space-around所有子元素平分剩余空间
* 值为space-between所有子元素先两边贴边在平分剩余空间
---
* 开启flex布局后默认为不换行
* 如果想要换行效果设置flex-wrap：wrap
* wrap-reverse是换行和换列，但以相反的顺序
---
* 利用align-items能够设置侧轴元素对齐的方式在子项为单项（单行）
* 的时候使用
* align-items的值为flex-start表示从头开始
* align-items的值为flex-end 表示从结尾开始
* align-items的值为center 表示居中显示
* align-items的值为stretch 会将子元素拉伸
---
* Align-content适应于换行（多行）的情况下（单行情况下无效）可以设置上对齐、下对齐、居中、拉伸以及平均分配剩余空间等属性值
* Align-item和align-content的区别单行找 align-items 多行找align-content
---
* Flex-flow就是flex-direction和flex-wrap的合写
  
##flex布局子项常见属性
* Flex用来设置分配剩余空间的比列的
* 剩余空间是指父盒子的宽度减去没有设置flex的盒子的宽度
* 在将剩余空间按占比分配给各个子盒子
* 比列计算：当前子盒子的flex数值/所有flex的总和
* align-self允许单个项目与其他项目不一样的对齐方式
* order可以定义子项排列顺序，数值越小越前（默认是0）
---
* flex-grow定义 flex item 在主轴方向上的放大比例，默认值为 0，即如果存在剩余空间，该 item 也不会放大；flex-shrink定义 flex item 在主轴方向上的缩小比例，默认值为 1，即如果空间不足，该 item 将缩小.
* flex-basis定义了再分配多余空间之前，flex item 占据的主轴大小（main size）
浏览器会根据这个属性，计算主轴是否有多余空间；它的默认值是 auto，即 item 的本来大小；
* flex组合写的顺序是grow、shrink、basis
####&emsp;&emsp;flex特殊写法
|属性|作用|
|:-|:-|
|flex:auto;|flex:1 1 auto|
|flex:none;|flex:0 0 auto|
|flex:0%;|flex:1 1 0%|
|flex:100px;|flex:1 1 100px|
|flex:1;|flex:1 1 0%|