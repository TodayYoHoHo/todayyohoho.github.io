+++
date = '2026-05-15T00:00:00+08:00'
draft = false
title = 'JavaScript'
author = "todayyohoho"
tags = ['web', 'javascript']
+++
# JS

# 变量

```js
在js中定义变量需要用关键字声明
1. var name='111'
2. let name_1='222'
# var 和 let 的区别
var作用于全局
let局部定义局部生效
```

### 常量

```js
const pi = 3.14
```

### 命名规范

```js
1. 变量名只能是数字，字母，下划线，$
2. 变量名命名规范
	js推荐驼峰式命名
	userName
	dataOfDb
	python推荐使用下划线
3.不能用关键字做变量名
```

### 代码书写位置

浏览器console界面或单独文件

# 数据类型

js是一门面向对象的编程语言，一切接对象

js拥有动态类型，一个变量名可以指向任意数据类型

## 数值类型

```js
var a = 11.11;
typeof a;
‘number’

// 特殊的NaN：数值类型 表示不是一个数字

转类型
parseInt()
parseFloat()
```

## 字符类型

```js
var s = '111'
var s = "222"
不支持三引号

模版字符串
var s = `
12
23
`
除了可以定义多行文本之外，还可以实现格式化字符串的操作
书写${}会动去前找括号的变量名对应的值,如果没有定义直接报错
var name = '123'
var age = 18
var s = `
my name is ${name} my age is ${age}
`

// 字符串的拼接
python 中推荐用join做拼接
js中直接用+
name+age
```

### 字符串操作

|JavaScript 方法|功能说明|Python 对应方法 / 操作|
| :----------------| :-----------------------------------------------| :-----------------------|
|​`.length`|返回字符串长度|​`len()`|
|​`.trim()`|移除字符串两端空白字符（空格、换行、制表符等）|​`.strip()`|
|​`.trimLeft()`|移除字符串左侧空白字符|​`.lstrip()`|
|​`.trimRight()`|移除字符串右侧空白字符|​`.rstrip()`|
|​`.charAt(n)`|返回索引为`n`的字符|​`[]`​索引取值（如`s[n]`）|
|​`.concat(value, ...)`|拼接多个字符串（自动转换成相同数据类型）|​`.join()`​/`+`运算符|
|​`.indexOf(substring, start)`|查找子串的索引位置，找不到返回`-1`|​`.find()`​/`str.index()`|
|​`.substring(from, to)`|根据索引截取子串（不包含`to`位置）|切片操作`s[from:to]`|
|​`.slice(start, end)`|切片，截取子串，支持负数索引|切片操作`s[start:end]`|
|​`.toLowerCase()`|将字符串转为小写|​`.lower()`|
|​`.toUpperCase()`|将字符串转为大写|​`.upper()`|
|​`.split(delimiter, limit)`|按指定分隔符分割字符串，返回数组|​`.split()`|

## 布尔值

在js中布尔值是全小写的true，false

false：空字符串，0，null，undefined，NaN

### null与undefined

```js
null
表示值为空，一般都是 指定 或者 清空 一的变量时使用
undefined
表示声明一个变量但是没有做初始化操作
函数没有指明返回值时返回undefined
```

# 运算符

```js
算数运算符
x++
++x

比较运算符
1 == ‘1’ 弱等于，做数据类型的转换
1 === ‘1’ 强等于，判断数据类型
1 ！= ‘1’ false
1 ！== ‘1’ true

逻辑运算符
python：and or not
js: && || !

5 && '5'
5 是真值，继续求值；
'5' 是真值，所有值都为真，返回最后一个操作数 '5'。

!5 && '5'
!5：5 是真值，取反后为 false；
遇到第一个假值，直接返回 false

0 || 1
0 是假值，继续求值；
1 是真值，遇到第一个真值，直接返回 1。

赋值运算符
=，+= -=，，，，
```

# 对象

- ## 数组（类似于python中的列表）  [ ]

|JavaScript 数组方法|功能说明|Python 列表对应操作 / 方法|
| :--------------------| :---------------------------------------------| :---------------------------|
|​`.length`|获取数组的大小（长度）|​`len()`|
|​`.push(ele)`|在数组尾部追加元素|​`.append(ele)`|
|​`.pop()`|获取并移除数组尾部的元素|​`.pop()`|
|​`.unshift(ele)`|在数组头部插入元素|​`.insert(0, ele)`|
|​`.shift()`|移除并返回数组头部的元素|​`.pop(0)`​/`.pop(index=0)`|
|​`.slice(start, end)`|切片，截取数组片段（不修改原数组）|切片操作`list[start:end]`|
|​`.reverse()`|反转数组（修改原数组）|​`.reverse()`|
|​`.join(seq)`|将数组元素连接成字符串|​`''.join(list)`|
|​`.concat(val, ...)`|连接多个数组，返回新数组|​`+`​运算符 /`.extend()`|
|​`.sort()`|对数组元素进行排序（修改原数组）|​`.sort()`​/`sorted()`|
|​`.forEach(callback)`|遍历数组，每个元素传递给回调函数|​`for`循环遍历|
|​`.splice(start, deleteCount, ...items)`|删除元素，并可向数组添加新元素（修改原数组）|​`del list[start:end]`​/`.insert()`​+`.pop()`|
|​`.map(callback)`|返回每个元素调用函数处理后的值的新数组|​`map()`/ 列表推导式|

|功能|JS 方法|Python 对应方式|
| :-----------------| :--------| :-------------------|
|映射处理每个元素|​`.map(callback)`|​`map(func, iterable)`​/ 列表推导式`[x*2 for x in lst]`|
|过滤元素|​`.filter(callback)`|​`filter(func, iterable)`​/ 列表推导式`[x for x in lst if x>2]`|
|归约计算|​`.reduce(callback)`|​`functools.reduce(func, iterable)`|

```js
python
from functools import reduce
lst = [1, 2, 3, 4]

# map: 映射：每个元素平方
list(map(lambda x: x**2, lst))  # [1, 4, 9, 16]

# filter: 筛选：筛选偶数
list(filter(lambda x: x % 2 == 0, lst))  # [2, 4]

# reduce: 求和
reduce(lambda a, b: a + b, lst)  # 10
```

遍历.forEach

```js
// JS
let ll = [1, 2, 3];
ll.forEach(function(value, index) {
    console.log(value, index);
});
ll.forEach((value, index) => console.log(value, index));

# 元素+元素索引+元素的数据来源
ll.forEach(function(value, index, arr) {
    console.log(value, index, arr);
}, ll);
```

splice

```js
array.splice(startIndex, deleteCount, item1, item2, ...)
startIndex：操作的起始索引
deleteCount：要删除的元素个数
item1, item2...：可选，要插入到数组中的新元素
```

map

```js
数组.map(function(当前值, 索引, 原数组) {
    return 处理后的值
})
value：当前正在遍历的元素
index：当前元素索引
arr：原数组本身

ll.map(v => v * 2)
```

## 自定义对象（类似于python中的字典） { }

```js
创建自定义对象，第一种方式
var d = {'name':'today','age'=18}
第二种方式，使用关键字new
var d2 = new Object()
添加键值对：d2.name = 'today'

typeof d
"object"
取值
d.name
d.age

for(let i in d){
	console.log(i,d[i])
}
支持for循环取值，暴露给外界可以直接获取的也是键
```

## 内置对象

### Date对象

```js
let d3 = new Date()
拿到结构化时间
d3.toLocalString()
转化成便于读的格式

# 也支持自己手动输入时间
let d4 = new Date('2200/11/11 11:11:11')
d4.toLocaleString()

let d5 = new Date(1111,11,11,11,11,11)
d5.toLocaleString()  # 月份从0开始0-11月
"1111/12/11 上午11:11:11"

# 时间对象具体方法
let d6 = new Date();
d6.getDate()         // 获取日
d6.getDay()          // 获取星期
d6.getMonth()       // 获取月份(0-11)
d6.getFullYear()    // 获取完整的年份
d6.getHours()       // 获取小时
d6.getMinutes()     // 获取分钟
d6.getSeconds()     // 获取秒
d6.getMilliseconds()// 获取毫秒
d6.getTime()         // 时间戳
```

### JSON对象

```js
在python中序列化和反序列化
	dumps	序列化
	loads	反序列化

js中序列化和反序列化
	JSON.stringify()
	JSON.parse()

let d7 = {'name':'today','age':18}
let res = JSON.stringify(d7)
JSON.parse(res)
```

### RegExp对象

```js
在python中使用正则需要借用于re模块
在js中需要创建正则对象

# 第一种
let reg1 = new RegExp('^[a-zA-Z][a-zA-Z0-9]{5,11}')

# 第二种 推荐
let reg2 = /^[a-zA-Z][a-zA-Z0-9]{5,11}/

匹配内容
reg1.test('abcsss')
reg2.test('abcsss')

# 题目 获取字符串里面所有的字母s
let sss = 'egondsb dsb dsb'
sss.match(/s/)   # 拿到一个就停止了
sss.match(/s/g)  # 全局匹配  g就表示全局模式

全局模式槽点
1.全局模式有lastIndex属性，指针停留在结尾
2.什么都不传默认传递undefined
```

### Math对象

```js
abs(x)        返回数的绝对值。
exp(x)        返回 e 的指数。
floor(x)      对数进行下舍入。
log(x)        返回数的自然对数（底为e）。
max(x,y)      返回 x 和 y 中的最高值。
min(x,y)      返回 x 和 y 中的最低值。
pow(x,y)      返回 x 的 y 次幂。
random()      返回 0 ~ 1 之间的随机数。
round(x)      把数四舍五入为最接近的整数。
sin(x)        返回数的正弦。
sqrt(x)       返回数的平方根。
tan(x)        返回角的正切。
```

# 流程控制

## if

```js
if (条件){
成立代码
}else if(条件){
代码
}else{
代码
}
js中代码没有缩进
```

## switch

```js
var num = 2;

switch(num){
    case 0:
        console.log('喝酒');

    case 1:
        console.log('唱歌');
        break;
    case 2:
        console.log('洗脚');
        break;
	default:
		console.log('111')
}
```

## for

```js
for(条件){代码块}
for(let i=0;i<10;i++){
	console.log(i)
}
```

## while

```js
// while循环
var i = 0;
while (i < 100) {
    console.log(i);
    i++;
}
```

## 三元运算符

```js
python：res = 1 if 1>2 else 3
js:
var res = 1<2? 1:3
```

# 函数

```js
关键字function

格式
function(形参1，形参2，，，){体代码}

function func1(a,b){
	console.log("123")
}
参数值在传的时候传多传少都不会报错
function func2(a, b) {
    if (arguments.length < 2) {
        console.log('传少了');
    } else if (arguments.length > 2) {
        console.log('传多了');
    } else {
        console.log('正常执行');
    }
}

返回值 使用的是return
return多个只取最后一个，多个东西需要用数组的形式

匿名函数
// 写法1：直接声明匿名函数（会报错）
function() {
    console.log('哈哈哈哈')
}

// 写法2：将匿名函数赋值给变量（正确）
var res = function() {
    console.log('哈哈哈哈')
}

箭头函数
var func1 = v => v;  """箭头左边的是形参 右边的是返回值"""
等价于
var func1 = function(v){
    return v
}

var func2 = (arg1,arg2) => arg1+arg2
等价于
var func1 = function(arg1,arg2){
    return arg1+arg2
}
```

函数的全局变量和局部变量  
和python中的一致  
闭包

# BOM与DOM操作

- BOM（Browser Object Model）：浏览器对象模型，js代码操作浏览器
- DOM（Document Object Model）：文档对象模型，js代码操作标签

## BOM操作

```js
1.window对象
window对象指代的就是浏览器窗口

window.innerHeight   浏览器窗口的高度
900
window.innerWidth    浏览器窗口的宽度
1680

window.open('https://www.baidu.com/','','height=400px,width=400px,top=400px,left=400px')
# 新建窗口打开页面 第二个参数写空即可 第三个参数写新建的窗口的大小和位置
# 扩展父子页面通信window.opener() 了解

window.close()   关闭当前页面
```

### window子对象

如果是window子对象，那么window可以省略不写

#### navigator对象

```js
window.navigator.appName
"Netscape"

window.navigator.appVersion
"5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36"

window.navigator.userAgent    掌握  # 用来表示当前是否是一个浏览器
"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36"


"""
扩展:防爬措施
  1.最简单最常用的一个就是校验当前请求的发起者是否是一个浏览器
     userAgent
     user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6)
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36
     如何破解该措施
     在你的代码中加上上面的user-agent配置即可
"""

window.navigator.platform
```

#### history对象

```js
window.history.back()	后退
window.history.forward()	前进
```

#### location对象

```js
window.location.href       # 获取当前页面的url
window.location.href = url # 跳转到指定的url
window.location.reload()   # 刷新页面
```

### 弹出框

- 警告框

  ​`alert('！！！')`
- 确认框

  ​`confirm('...')`

  可以获取用户点击确定还是取消
- 提示框

  ​`prompt('提示内容', '默认内容')`

  获取用户输入内容

### 计时器相关

```js
function func1() {
    alert(123)
}
let t = setTimeout(func1, 3000);  // 毫秒为单位 3秒之后自动执行func1函数
clearTimeout(t)                   // 取消定时任务 如果你想要清除定时任务 需要用变量指代定时任务


function func2() {
    alert(123)
}

function show(){
    let t = setInterval(func2, 3000);  // 每隔3秒执行一次
    function inner(){
        clearInterval(t)              // 清除定时器
    }
    setTimeout(inner, 9000)            // 9秒之后触发
}
show()
```

## DOM操作

```js
"""
DOM树的概念

所有的标签都可以称之为是节点

JavaScript 可以通过DOM创建动态的 HTML：

JavaScript 能够改变页面中的所有 HTML 元素
JavaScript 能够改变页面中的所有 HTML 属性
JavaScript 能够改变页面中的所有 CSS 样式
JavaScript 能够对页面中的所有事件做出反应


DOM操作操作的是标签 而一个html页面上的标签有很多
  1.先学如何查找标签
  2.再学DOM操作标签

DOM操作需要用关键字document起手
"""
```

### 查找标签

- 直接查找

  ```js
  """
  id查找
  类查找
  标签查找
  """

  # 注意三个方法的返回值是不一样的
  区分拿到的是对象还是数组，对象可以直接.xxx使用对象方法，数组需要先取对象再使用方法
  document.getElementById('d1')
  <div id="d1">...</div>

  document.getElementsByClassName('c1')
  HTMLCollection [p.c1]0: p.c1length: 1__proto__: HTMLCollection

  document.getElementsByTagName('div')
  HTMLCollection(3) [div#d1, div, div, d1: div#d1]

  let divEle = document.getElementsByTagName('div')[1]
  divEle
  <div>div>div</div>

  """
  用变量名指代标签对象的时候 一般情况下都推荐书写成
  xxxEle
      divEle
      aEle
      pEle
  """
  ```

- 间接查找

  ```js
  let pEle = document.getElementsByClassName('c1')[0]  # 注意是否需要索引取值

  pEle.parentElement  # 拿父节点
  <div id="d1">"div
      "<div>div>div</div><p class="c1">...
  </p><p>div>p</p></div>

  pEle.parentElement.parentElement
  <body>...</body>

  pEle.parentElement.parentElement.parentElement
  <html lang="en"><head>...</head><body>...</body></html>

  pEle.parentElement.parentElement.parentElement.parentElement
  null


  let divEle = document.getElementById('d1')
  divEle.children  # 获取所有的子标签
  divEle.children[0]
  <div>div>div</div>

  divEle.firstElementChild
  <div>div>div</div>

  divEle.lastElementChild
  <p>div>p</p>

  divEle.nextElementSibling  # 同级别下面第一个
  <div>div下面div</div>

  divEle.previousElementSibling  # 同级别上面第一个
  <div>div上面的div</div>
  ```

### 节点操作

```js
"""
通过DOM操作动态的创建img标签
并且给标签加属性
最后将标签添加到文本中
"""

let imgEle = document.createElement('img')  # 创建标签

imgEle.src = '111.png'  # 给标签设置默认的属性
"111.png"
imgEle

imgEle.username = 'jason'  # 自定义的属性“没办法”点的方式直接设置
"jason"
imgEle
<img src="111.png">

imgEle.setAttribute('username','jason')  # 既可以设置自定义的属性也可以设置默认的属性
undefined
imgEle
<img src="111.png" username="jason">

imgEle.setAttribute('title','一张图片')
imgEle
<img src="111.png" username="jason" title="一张图片">


let divEle = document.getElementById('d1')
undefined

divEle.appendChild(imgEle)  # 标签内部添加元素(尾部追加)
<img src="111.png" username="jason" title="一张图片">

"""
创建a标签
设置属性
设置文本
添加到标签内部
	添加到指定的标签的上面
"""
let aEle = document.createElement('a')

aEle
<a></a>

aEle.href = 'https://www.baidu.com/'
aEle
<a href="https://www.baidu.com/"></a>

aEle.innerText = '点我'  # 给标签设置文本内容
aEle
<a href="https://www.baidu.com/">点我</a>

let divEle = document.getElementById('d1')

let pEle = document.getElementById('d2')

divEle.insertBefore(aEle, pEle)  # 添加标签内容指定位置添加
<a href="https://www.baidu.com/">点我</a>

"""
额外补充
appendChild()
    removeChild()
    replaceChild()

setAttribute()    设置属性
    getAttribute()    获取属性
    removeAttribute()    移除属性
"""

# innerText与innerHTML
divEle.innerText  # 获取标签内部所有的文本
divEle.innerHTML  # 内部文本和标签都拿到
"div
    <a href="https://www.baidu.com/">点我</a><p id="d2">div&gt;p</p>
    <span>div&gt;span</span>
"

divEle.innerText = 'heiheihei'
"heiheihei"

divEle.innerHTML = 'hahahaha'
"hahahaha"

divEle.innerText = '<h1>heiheihei</h1>'  # 不识别html标签
"<h1>heiheihei</h1>"

divEle.innerHTML = '<h1>hahahaha</h1>'  # 识别html标签
"<h1>hahahaha</h1>"
```

### 获取值操作

```js
# 获取用户数据标签内部的数据
let seEle = document.getElementById('d2')
seEle.value
"111"

let inputEle = document.getElementById('d1')
inputEle.value

# 如何获取用户上传的文件数据
let fileEle = document.getElementById('d3')
fileEle.value  # 无法获取到文件数据
"C:\fakepath\02_测试路由.png"

fileEle.files
FileList {0: File, length: 1}0: File {name: "02_测试路由.png", lastModified: 1557043082000, lastModifiedDate: Sun May 05 2019 15:58:02 GMT+0800 (中国标准时间), webkitRelativePath: "", size: 29580, ...}length: 1__proto__: FileList

fileEle.files[0]  # 获取文件数据
File {name: "02_测试路由.png", lastModified: 1557043082000, lastModifiedDate: Sun May 05 2019 15:58:02 GMT+0800 (中国标准时间), webkitRelativePath: "", size: 29580, ...}
```

### class,css操作

```js
let divEle = document.getElementById('d1')

divEle.classList  # 获取标签所有的类属性
DOMTokenList(3) ["c1", "bg_red", "bg_green", value: "c1 bg_red bg_green"]

divEle.classList.remove('bg_red')  # 移除某个类属性

divEle.classList.add('bg_red')    # 添加类属性

divEle.classList.contains('c1')   # 验证是否包含某个类属性
true
divEle.classList.contains('c2')
false

divEle.classList.toggle('bg_red') # 有则删除无则添加
false
divEle.classList.toggle('bg_red')
true

css操作
# DOM操作操作标签样式 统一先用style起手
let pEle = document.getElementsByTagName('p')[0]
undefined

pEle.style.color = 'red'
"red"

pEle.style.fontSize = '28px'
"28px"

pEle.style.backgroundColor = 'yellow'
"yellow"

pEle.style.border = '3px solid red'
"3px solid red"
```

## 事件

达到某个实现设定的条件，自动触发的动作

```js
# 绑定事件的两种方式
<button onclick="func1()">点我</button>
<button id="d1">点我</button>

<script>
    // 第一种绑定事件的方式
    function func1() {
        alert(111)
    }

    // 第二种
    let btnEle = document.getElementById('d1');
    btnEle.onclick = function () {
        alert(222)
    }
</script>

js代码一般放在body内最底部

onload等待...完毕
xxx.onload
```

### 原生js事件绑定

- #### 开关灯

  ```html
  <style>
  /* 需要先写样式类，toggle才会变色 */
  .bg_red { background: red; width:100px;height:100px; }
  .bg_green { background: green; }
  </style>

  <div id="d1" class="cl bg_red bg_green"></div>
  <button id="d2">变色</button>

  <script>
  // 获取按钮、div元素
  let btnEle = document.getElementById('d2')
  let divEle = document.getElementById('d1')

  // 按钮点击事件
  btnEle.onclick = function () {
      // classList.toggle：有这个类就删掉，没有就加上
      divEle.classList.toggle('bg_red')
  }
  </script>
  ```

- #### input框获取焦点和失去焦点

  ```html
  <input type="text" value="老板 去吗?" id="d1">

  <script>
  // 获取输入框元素
  let iEle = document.getElementById('d1')

  // onfocus：输入框【获得焦点】(点击输入框)触发
  iEle.onfocus = function () {
      // 清空输入框内容
      iEle.value = ''
  }

  // onblur：输入框【失去焦点】(点击页面别处)触发
  iEle.onblur = function () {
      // 给输入框重新赋值
      iEle.value = '没钱 不去!'
  }
  </script>
  ```

- #### 展示当前时间

  ```html
  <input type="text" id="d1" style="display:block;height:50px;width:200px">
  <button id="d2">开始</button>
  <button id="d3">结束</button>

  <script>
  // 全局变量，用来保存定时器标识
  let t = null
  // 获取元素
  let inputEle = document.getElementById('d1')
  let startBtnEle = document.getElementById('d2')
  let endBtnEle = document.getElementById('d3')

  // 获取本地时间、赋值给输入框
  function showTime() {
    let currentTime = new Date();
    inputEle.value = currentTime.toLocaleString()
  }

  // 开始按钮点击
  startBtnEle.onclick = function () {
    // !t ：只有定时器为空时才新建，防止多次点击开启多个定时器
    if(!t){
      t = setInterval(showTime,1000) // 每隔1秒执行showTime
    }
  }

  // 结束按钮点击
  endBtnEle.onclick = function () {
    clearInterval(t) // 关闭定时器
    t = null // 重置变量，允许再次点击开启
  }
  </script>
  ```

- #### 省市联动

  ```html
  <!-- 两个下拉框：省份、市区 -->
  <select name="" id="d1">
    <option value="" selected disabled>--请选择--</option>
  </select>
  <select name="" id="d2"></select>

  <script>
  // 获取两个下拉元素
  let proEle = document.getElementById('d1')
  let cityEle = document.getElementById('d2')

  // 省市对应数据源
  let data = {
    "河北": ["廊坊", "邯郸", "唐山"],
    "北京": ["朝阳区", "海淀区", "昌平区"],
    "山东": ["威海市", "烟台市", "临沂市"],
    "上海": ["浦东新区", "静安区", "黄浦区"],
    "深圳": ["南山区", "宝安区", "福田区"]
  }

  // 1. 页面初始化：循环把【省份】渲染进第一个下拉框
  for(let key in data){
    // 创建option标签
    let opEle = document.createElement('option')
    opEle.innerText = key    // 下拉显示文字
    opEle.value = key        // option的值
    proEle.appendChild(opEle)// 添加到省份下拉
  }

  // 2. 省份切换事件：选省份，自动渲染对应市区
  proEle.onchange = function(){
    // 获取当前选中的省份名
    let selectPro = this.value
    // 拿到该省份对应的市区数组
    let currentCityList = data[selectPro]

    // 切换省份前：清空旧的市区选项
    cityEle.innerHTML = ''

    // 循环市区数组，生成option放入第二个下拉
    for (let i=0;i<currentCityList.length;i++){
      let currentCity = currentCityList[i]
      let opEle = document.createElement('option')
      opEle.innerText = currentCity
      opEle.value = currentCity
      cityEle.appendChild(opEle)
    }
  }
  </script>
  ```

# jQuery

```html
jQuery内部封装了原生的js代码(还额外添加了很多的功能)
能够让你通过书写更少的代码 完成js操作
类似于python里面的模块  在前端模块不叫模块  叫 “类库”

兼容多个浏览器的 你在使用jquery的时候就不需要考虑浏览器兼容问题

jQuery的宗旨
  write less do more
  让你用更少的代码完成更多的事情

复习
  python导入模块发生了哪些事？
    导入模块其实需要消耗资源
  jQuery在使用的时候也需要导入
    但是它的文件非常的小(几十KB) 基本不影响网络速度

选择器
筛选器
样式操作
文本操作
属性操作
文档处理
事件
动画效果
插件
each、data、Ajax(重点 django部分学)

版本介绍

jQuery文件下载
  压缩      容量更小
  未压缩
```

导入问题

```html
下载后导入
<script src=jQuery-3.71.js></script>

引入CDN服务（基于网络直接请求加载）
CDN：内容分发网络
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
```

## 基本语法

```html
# jQuery基本语法

jQuery(选择器).action()

秉持着jQuery的宗旨 jQuery简写 $
jQuery() === $()

# jQuery与js代码对比

eg:将p标签内部的文本颜色改为红色
// 原生js代码操作标签
let pEle = document.getElementById('d1')
pEle.style.color = 'red'

// jQuery操作标签
$('p').css('color','blue')
```

## 选择器

### 基本选择器

```html
// id选择器
$('#d1')
// 控制台输出：w.fn.init [div#d1]0: div#d1length: 1__proto__: Object(0)

// class选择器
$('.c1')
// 控制台输出：w.fn.init [p.c1, prevObject: w.fn.init(1)]0: p.c1length: 1prevObject: w.fn.init [document]__proto__: Object(0)

// 标签选择器
$('span')
// 控制台输出：w.fn.init(3) [span, span, span, prevObject: w.fn.init(1)]

"""一定要区分开(重点)"""
// jQuery对象如何变成标签(DOM)对象
$('#d1')[0]
// 结果等价于
document.getElementById('d1')

// 标签(DOM)对象如何转jQuery对象
$(document.getElementById('d1'))
```

### 组合选择器/分组与嵌套

```js
$('div')
// w.fn.init(2) [div#d1, div.c1, prevObject: w.fn.init(1)]

$('div.c1')
// w.fn.init [div.c1, prevObject: w.fn.init(1)]0: div.c1length:
// 1prevObject: w.fn.init [document]__proto__: Object(0)

$('div#d1')
// w.fn.init [div#d1, prevObject: w.fn.init(1)]

$('*')
// w.fn.init(19) [html, head, meta, title, meta, link, script, script,
// body, span, span, div#d1, span, p#d2, span, span, div.c1, span, span,
// prevObject: w.fn.init(1)]


$('#d1,.c1,p') // 并列+混用
// w.fn.init(3) [div#d1, p#d2, div.c1, prevObject: w.fn.init(1)]

$('div span') // 所有后代
// w.fn.init(3) [span, span, span, prevObject: w.fn.init(1)]

$('div>span') // 儿子
// w.fn.init(2) [span, span, prevObject: w.fn.init(1)]

$('div+span') // 比邻
// w.fn.init [span, prevObject: w.fn.init(1)]

$('div~span') // 弟弟
// w.fn.init(2) [span, span, prevObject: w.fn.init(1)]
```

### 基本筛选器

```js
$('ul li:first')   // 大儿子：匹配ul下**第一个li元素**
$('ul li:last')    // 小儿子：匹配ul下**最后一个li元素**
$('ul li:eq(2)')   // 放索引：匹配ul下**下标=2的li（索引从0开始计数，第三个li）
// 1. :eq(索引) 精准匹配单个元素，索引从0开始
$('ul li:eq(2)')    // 选取 ul 下索引为2的li（第3个li）

// 2. :even 偶数索引（0、2、4...，索引0算偶数）
$('ul li:even')     // 匹配下标 0/2/4…… 的所有li

// 3. :odd 奇数索引（1、3、5……）
$('ul li:odd')      // 匹配下标 1/3/5…… 的所有li

// 4. :gt(n) greater than，选取索引 > n 的元素
$('ul li:gt(2)')    // 匹配下标大于2：3、4、5...全部li

// 5. :lt(n) less than，选取索引 < n 的元素
$('ul li:lt(2)')    // 匹配下标小于2：0、1 两个li

$('ul li:not("#d1")')  // 排除id=d1的标签，选取ul下**除id为d1之外**所有li元素

$('div')
// 选中页面所有div，控制台显示length=2，一共2个div标签

$('div:has("p")')  // 筛选【内部包含p子标签】的div元素
```

### 属性选择器

```js
// 1. [属性名]：选中**拥有该属性**的所有标签
$('[username]')
// 匹配页面所有带 username 属性的元素：2个input + 1个p，共3个

// 2. [属性="值"]：精准匹配 属性=指定值 的元素
$('[username="111"]')
// 选中 username="111" 的input标签

// 3. 标签名[属性="值"]：限定标签+属性精准匹配
$('p[username="222"]')
// 只找<p>标签里 username="222" 的元素

注意外层单引号，内层双引号

// 1. [属性名]：匹配**所有带有type属性**的元素
$('[type]')
// 结果length=2，选中2个拥有type属性的input标签

// 2. [属性="值"]：精准匹配 type="text" 的元素
$('[type="text"]')
// 筛选出type属性值为text的input，同样匹配到2个元素
```

### 表单筛选器

```js
// 写法1：标签+属性精准选择
$('input[type="text"]')       // 选中type=text的输入框
$('input[type="password"]')   // 选中type=password的密码框

// 写法2：jQuery表单伪类简写（等价上面代码）
$(':text')     // 简写，等效 input[type="text"]
$(':password') // 简写，等效 input[type="password"]

:text
:password
:file
:radio
:checkbox
:submit
:reset
:button
...

表单对象属性
:enabled
:disabled
:checked
:selected

$(':checked')  # 它会将checked和selected都拿到

$(':selected')  # 它不会 只拿selected

$('input:checked')  # 自己加一个限制条件
```

### 筛选器方法

```js
$('#d1').next()    # 同级别下一个
$('#d1').nextAll()
$('#d1').nextUntil('.c1') # 不包括最后一个

$('.c1').prev()       # 上一个同级元素
$('.c1').prevAll()
$('.c1').prevUntil('#d2')

$('#d3').parent()     # 第一级父标签
$('#d3').parent().parent()
$('#d3').parents()
$('#d3').parentsUntil('body')

$('#d2').children()    # 后代（直接子元素）
$('#d2').siblings()    # 同级别上下所有兄弟元素

$('div p')
$('div').find('p')  // find从某个区域内筛选出想要的标签

$('div span:first')
$('div span').first()

$('div span:last')
$('div span').last()

$('div span:not("#d3")')
$('div span').not('#d3')

.has()
.eq()
```

## 操作标签

### 操作类

|功能|原生 JS (classList)|jQuery 方法|
| ----------------------------| ---------------------| -------------|
|添加类名|​`classList.add()`|​`addClass()`|
|移除类名|​`classList.remove()`|​`removeClass()`|
|判断是否存在类名|​`classList.contains()`|​`hasClass()`|
|切换类名（有则删、无则加）|​`classList.toggle()`|​`toggleClass()`|

### css操作

```js
# 链式操作
<p>111</p>
<p>222</p>
"""一行代码将第一个p标签变成红色第二个p标签变成绿色"""
$('p').first().css('color','red').next().css('color','green')
# jQuery的链式操作 使用jQuery可以做到一行代码操作很多标签
# jQuery对象调用jQuery方法之后返回的还是当前jQuery对象 也就可以继续调用其他方法

class MyClass(object):
    def func1(self):
        print('func1')
        return self

    def func2(self):
        print('func2')
        return self

obj = MyClass()
obj.func1().func2()
```

### 位置操作

```js
// 位置操作
offset()     // 相对于浏览器窗口位置
position()   // 相对于父标签的位置
scrollTop()  // 需要了解
$(window).scrollTop()   // 无参：获取页面垂直滚动距离
$(window).scrollTop(0)  // 传参：设置页面滚动到指定垂直位置
$(window).scrollTop(500)
scrollLeft()
```

### 尺寸

```js
$('p').height()      // 文本内容高
$('p').width()

$('p').innerHeight() // 内容+padding
$('p').innerWidth()

$('p').outerHeight() // 内容+padding+border
$('p').outerWidth()
```

### 文本

```js
"""
操作标签内部文本
js                jQuery
innerText         text()  括号内不加参数就是获取，加了就是设置
innerHTML         html()

$('div').text()
"111"

$('div').html()
"<p>111</p>"

$('div').text('1')
$('div').html('1')
$('div').text('<h1>1</h1>')
$('div').html('<h1>1</h1>')
"""
```

### 取值

```js

js            jQuery
.value        .val()

$('#d1').val()
"sasdasdsadsadad"

$('#d1').val('555') // 括号内不加参数就是获取，加了就是设置

$('#d2').val()
"C:\\fakepath\\01_测试路由.png"
$('#d2')[0].files[0] // jQuery对象转原生DOM对象，获取上传文件File对象
```

### 属性操作

```js
# 属性操作

js中                     jQuery
setAttribute()        attr(name,value)  // 设置属性
getAttribute()        attr(name)        // 获取属性
removeAttribute()     removeAttr(name)  // 删除属性

在用变量存储对象的时候 js中推荐使用
    XXXEle      标签对象
jQuery中推荐使用
    $XXXEle     jQuery对象

let $pEle = $('p')

$pEle.attr('id')            // 获取id属性 → "d1"
$pEle.attr('class')         // 获取class属性 → undefined
$pEle.attr('class','c1')    // 设置class="c1"
$pEle.attr('id','id666')    // 修改id为id666
$pEle.attr('password','jason123') // 新增自定义password属性
$pEle.removeAttr('password')// 删除password属性


对于标签上能看到的原生属性和自定义属性用attr
对于返回布尔值，比如checkbox、radio、option是否被选中用prop

$('#d2').prop('checked')
$('#d2').prop('checked')
$('#d3').prop('checked',true)
$('#d3').prop('checked',false)
```

### 文档处理

```js

js                     jQuery
createElement('p')     $('<p>')
appendChild()          append()


let $pEle = $('<p>')
$pEle.text('111')
$pEle.attr('id','d1')
$('#d1').append($pEle)      // 尾部内部做添加
$pEle.appendTo($('#d1'))

$('#d1').prepend($pEle)     // 内部头部追加
$pEle.prependTo($('#d1'))

$('#d2').after($pEle)       // 放在某个标签后面（同级）
$pEle.insertAfter($('#d1'))

$('#d1').before($pEle)      // 放在某个标签后面（同级）
$pEle.insertBefore($('#d2'))

$('#d1').remove()           // 将标签从DOM树中删除
$('#d1').empty()            // 清空标签内部所有的内容
```

## 事件

### jQuery绑定事件的方式

```js
第一种 绑定点击事件
$('#d1').click(function () {
    alert('1111')
});

第二种(功能更加强大 还支持事件委托)
$('#d2').on('click',function () {
    alert('111')
})
```

- ### 克隆事件

  ```js
  <button id="d1">1</button>

  <script>
  $('#d1').on('click',function () {
    // console.log(this)  // this指代是当前被操作的原生DOM标签对象
    // $(this).clone().insertAfter($('body')) // clone默认只克隆标签结构、样式，不克隆绑定的事件
    $(this).clone(true).insertAfter($('body')) // 参数true：连带绑定的事件一起克隆
  })
  </script>
  ```

- ### 左侧菜单显示隐藏

  ```js
  <script>
  $('.title').click(function () {
      // 先给所有的items加hide（全部隐藏）
      $('.items').addClass('hide')
      // 然后将被点击标签内部的hide移除（当前点击项展开）
      $(this).children().removeClass('hide')
  })
  </script>
  ```

- ### 自定义模态框

  给标签添加或移除hide属性
- ### 返回顶部

  ```js
  <script>
  $(window).scroll(function () {
      if($(window).scrollTop() > 300){
          $('#d1').removeClass('hide')
      }else{
          $('#d1').addClass('hide')
      }
  })
  </script>
  ```

- ### 自定义登录校验

  ```js
  在获取用户的用户名和密码的时候 用户如果没有填写 应该提示用户

  <p>username:
      <input type="text" id="username">
      <span style="color: red"></span>
  </p>
  <p>password:
      <input type="text" id="password">
      <span style="color: red"></span>
  </p>
  <button id="d1">提交</button>

  <script>
  let $userName = $('#username')
  let $passWord = $('#password')
  $('#d1').click(function () {
      // 获取用户输入的用户名和密码 做校验
      let userName = $userName.val()
      let passWord = $passWord.val()
      if (!userName) {
          $userName.next().text("用户名不能为空")
      }
      if (!passWord) {
          $passWord.next().text('密码不能为空')
      }
  })
  $('input').focus(function () {
      $(this).next().text('')
  })
  </script>
  ```

- ### input实时监控

  ```js
  <input type="text" id="d1">

  <script>
  $('#d1').on('input',function () {
      console.log(this.value)
  })
  </script>
  ```

- ### hover事件

  ```js
  <script>
  // 单参数：悬浮、离开都会触发同一个函数
  // $("#d1").hover(function () {
  //     alert(123)
  // })

  // 双参数：第一个→移入，第二个→移出
  $('#d1').hover(
      function () {
          alert('我来了')  // 鼠标悬浮移入
      },
      function () {
          alert('我溜了')  // 鼠标移出
      }
  )
  </script>
  ```

- ### 键盘按键

  ```js
  <script>
  $(window).keydown(function (event) {
      console.log(event.keyCode)
      if (event.keyCode === 16){
          alert('你按了shift键')
      }
  })
  </script>
  ```

‍
