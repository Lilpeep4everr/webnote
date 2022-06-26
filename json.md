##简介
&emsp;&emsp;在JS语言中，一切都是对象。因此，任何js支持的类型都可以通过JSON来表示，例如字符串、数字、对象、数组等。看看他的要求和语法格式：
·对象表示为键值对
·数据有逗号分割
·花括号保存对象
·方括号保存数组

格式为：
```json
{
    "name": "中国",
    "province": [{
        "name": "黑龙江",
        "cities": {
            "city": ["哈尔滨", "大庆"]
        }
    }, {
        "name": "广东",
        "cities": {
            "city": ["广州", "深圳", "珠海"]
        }
    }, {
        "name": "台湾",
        "cities": {
            "city": ["台北", "高雄"]
        }
    }, {
        "name": "新疆",
        "cities": {
            "city": ["乌鲁木齐"]
        }
    }]
}
```
##JSON 与 JS 对象的关系
&emsp;&emsp;很多人搞不清楚 JSON 和 JS 对象的关系，甚至连谁是谁都不清楚。其实，可以这么理解：**JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。** 如：
```
var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的
1
var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串
```
##JSON 和 JS 对象互转
&emsp;&emsp;要实现从JSON字符串转换为JS对象，使用 JSON.parse() 方法：
```
var obj = JSON.parse('{"a": "Hello", "b": "World"}'); //结果是 {a: 'Hello', b: 'World'}
```
&emsp;&emsp;要实现从JS对象转换为JSON字符串，使用 JSON.stringify() 方法：
```
var json = JSON.stringify({a: 'Hello', b: 'World'}); //结果是 '{"a": "Hello", "b": "World"}'
```
