##注释
```
//这种注释在编译后不会出现在css文件上
/* 这种注释就会被保留在css文件上 */
```
##Less变量
通过@进行宏定义标签
```
@width: 10px;
@height: @width + 10px;

#header {
  width: @width;
  height: @height;
}
```
举例：id选择器和类选择器的使用（url地址和属性变量同理）
```
@mySelector: #wrap;
@wrap: wrap;
@{mySelector}{
    color:aliceblue;
    width: 55px;
}
.@{wrap}{
    color:aliceblue;
    width: 55px;
}
#@{wrap}{
    color:aliceblue;
    width: 55px;
}
————————————————————————————————————
#wrap {
  color: aliceblue;
  width: 55px;
}
.wrap {
  color: aliceblue;
  width: 55px;
}
#wrap {
  color: aliceblue;
  width: 55px;
}

```
声明变量写法
```
@background:{background:red};
#main{
    @background();
}
#wrap{
    @Rules();
}
_________________
#main {
  background: red;
}
#wrap {
  width: 12px;
  height: 12px;
  border: 1px solid red;
}
```
变量运算进行运算时有一个值带单位就行，连接运算时记得添加空格。
变量作用域遵循**就近原则**
```

@var:@a;
@a:100%;
#wrap {
    width:@var;
    @a:9%;
}
_________________
#wrap {
  width: 9%;
}

```

##嵌套
```
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
____________________
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```
媒体查询
```
.component {
  width: 300px;
  @media (min-width: 768px) {
    width: 600px;
    @media  (min-resolution: 192dpi) {
      background-image: url(/img/retina2x.png);
    }
  }
  @media (min-width: 1280px) {
    width: 800px;
  }
}
__________________________________
.component {
  width: 300px;
}
@media (min-width: 768px) {
  .component {
    width: 600px;
  }
}
@media (min-width: 768px) and (min-resolution: 192dpi) {
  .component {
    background-image: url(/img/retina2x.png);
  }
}
@media (min-width: 1280px) {
  .component {
    width: 800px;
  }
}

```

##混合方法
无参数方法
```
.card(){
    background-color: aliceblue;
}

.dt{
    .card();
}
______________________________________
.dt {
  background-color: aliceblue;
}
//.与#皆可作为方法前缀，方法后写不写（）看个人习惯，建议写上来区分方法和选择器。
```
默认参数方法
```
.border(@a:10px,@b:20px,@c:30px,@color: #fff){
    border:solid 1px @color;
    /* @arguments指代传进来的全部参数 */
    box-shadow:@arguments;
}
.test{
    .border();
}
___________________________________________
.test {
  border: solid 1px #fff;
  /* @arguments指代传进来的全部参数 */
  box-shadow: 10px 20px 30px #fff;
}
```
方法的匹配模式
```
.tag(lr,@width:20px,@color:#000){
    border-color: transparent @color;
}
.tag(tp,@width:20px,@color:#000){
    border-color: @color transparent;
}
.tag(@_,@width:20px,@color:#000){
    border-style: solid;
    border:@width;
}
#main{
    .tag(lr,50px,#999);
}
______________________________________
#main {
  border-color: transparent #999;
  border-style: solid;
  border: 50px;
}
```

方法的命名空间
（存疑
方法条件筛选
```
#card {
    /* when */
    .border(@width,@color,@style) when(@width>100px) and (@color = #999){
        border:@style @color @width;
    }
    /* whennot */
    .margin(@width) when not (@width >= 222px){
        margin: @width;
    }
    /* 逗号分隔符方法 代表|| */
    .font(@size:20px) when (@size<50px),(@size>100px){
        font-size: @size;
    }
}

#main {
    #card > .border(200px,#999,solid);
    #card > .margin(111px);
    #card > .margin(333px);
    #card > .font(70px);
    #card > .font(70px);
    #card > .font(20px);
    
}
_______________________________________________
#main {
  border: solid #999 200px;
  margin: 111px;
  font-size: 20px;
}
//参数量不确定同样可以使用（...）来定义，并用@arguments来获取既可
方法使用同样可以使用！important

```
循环方法
```
.generate-columns(4);
.generate-columns(@n,@i:1) when(@i<=@n){
    .column-@{i}{
        width: (@i*100%/@n);
    }
    .generate-columns(@n,(@i+1));
}
________________________________________
.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}

```
属性拼接方法,+:会添加逗号，+_:会添加空格
```
.boxShadow2(){
    box-shadow+: inset 0 0 10px #555;
}
#main{
    .boxShadow2();
    box-shadow+: inset 0 0 10px #555;
}
_______________________________________
#main {
  box-shadow: inset 0 0 10px #555, inset 0 0 10px #555;
}

```

##继承
extend继承使用
```
.animation{
    transition: all .3s ease-out;
    .hide{
        transform: scale(0);
    }
}

#main {
    &:extend(.animation);
}
____________________________
.animation,
#main {
  transition: all 0.3s ease-out;
}
.animation .hide {
  transform: scale(0);
}

```
all全局搜索替换
```

#main{
    &:after{
        content:'less is good'
    }
}

#wrap:extend(#main all ){

}
________________________________
#main:after,
#wrap:after {
  content: 'less is good';
}

```

##导入
```
@import "nav.less"
```
想要引入但不编译
```
@import(reference)"nav.less"
```
@import的默认行为 相同文件只会被导入一次，随后的导入文件的重复代码都不会解析
```
@import(once)"nav.less"
```
```
@import(multiple) 同名文件多次导入

```
##检测函数
类型检测函数
*   iscolor
*   isnumber
*   isstring
*   iskeyword
*   isurl
单位检测函数
*   ispixel
*   ispercentage
*   isnumber
*   isem
*   isunit 

