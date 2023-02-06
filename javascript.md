[TOC]

# JS基础

## 引入方式

1. 页头引入(head标签内)    内嵌式: <script>todo···</script>

2. 页中引入(body标签内)    内嵌式

3. 元素事件中引入(标签属性中引入)    行内式
   
   ```html
   <input type="button" value="唐伯虎" onclick="alert('?')">
   ```

4. 引入外部js文件
   
   ```javascript
   <script src="js文件名.js"></script>    //中间不可以写代码
   ```

<br/>

## JS组成

- DOM：浏览器对象模型(API)
- BOM：页面文档对象模型(API)
- ECMAScript：JavaScript语法

浏览器分为两部分：

- 渲染引擎：解析HTML和CSS
- JS引擎：读取网页中JS代码(逐行解析)

<br/>

## JS数据类型

- 值类型(基本类型)：字符串（String）、数字(Number)、布尔(Boolean)、空（Null）、未定义（Undefined）、Symbol(ES6新增，代表独一无二的值)
- 引用数据类型（对象类型）：对象(Object)、数组(Array)、函数(Function)，还有两个特殊的对象：正则（RegExp）和日期（Date）。

**弱类型**语言

### 可以使用**typeof**查看变量数据类型

```
typeof 3.14;  //返回
```

### 转义字符

\n, \', \"    其他需要的查

### if语句判断

false, "", NaN, 0, null, undefined都会转换为**false**

### let命令

let声明的变量只在let命令**所在的块级作用域**内有效。

### const命令

**只读常量**

声明时**必须赋值**

只在声明**所在的块级作用域**内有效

### 模板字符串

模板字符串（template string）是增强版的字符串，用**反引号（`）标识**。它可以当作普通字符串使用，也可以用来**定义多行字符串**，或者在**字符串中嵌入变量**。

```javascript
// 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串
`In JavaScript this is
 not legal.`

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量,需要将变量名写在${}之中。
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

## 常用方法

### isNaN()方法

用来判断非数字，非数字返回true，反之返回false

### 字符串转数值型parseInt()

- Number.parseInt(): 字符串转整型
- Number.parseFloat(): 字符串转浮点型

### typeof运算符

用于返回它的操作数当前所容纳的数据的类型

```javascript
var num=10;
console.log(typeof num);        //number
```

### includes()寻找指定字符串

返回布尔值，表示是否找到了参数字符串

```
let s = 'ab';
s.includes('a') //true
s.includes('c') //false
```

## 声明提升

函数和变量声明都将被提升到作用域的最顶部

严格模式中不允许使用**未声明的变量**

```
console.log(num);
var num = 10;
//先var num;然后按作用域顺序执行，故结果为undefined
```

<br/>

## JS执行机制

JS特点：单线程

### 同步任务

同步任务都在主线程上执行，形成一个执行栈

前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。

### 异步任务

异步任务相关回调函数添加到任务队列中(消息队列)

你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。

### JS执行机制(事件循环)

![361c905af7153b1fe1ad9a882ac150e0](https://user-images.githubusercontent.com/112193327/203088229-38e96694-91c3-40f8-8b2b-f79cc8f2f7c4.png)
![94522dfb7cd2feed50a754941aff882f](https://user-images.githubusercontent.com/112193327/203088311-1dfe6d4e-440b-46ad-825b-d947f0baf01d.png)

# 数组

## 创建

1. 字面量
   
   ```
   var phone = ["Xiaomi","Iphone"]
   ```

2. 常规
   
   ```javascript
   var phone = new Array();
   phone[0] = "Xiaomi";
   phone[1] = "Iphone";
   或者
   var phone = new Array("Xiaomi","Iphone");
   ```

<br/>

## 访问

```javascript
var phone = new Array("Xiaomi","Iphone");
console.log(phone[0]); //Xiaomivar phone = new Array("Xiaomi","Iphone");
console.log(phone[0]); //Xiaomi
```

<br/>

## 常用方法

### 添加删除元素

- array.push(elem): 添加至数组尾部
- array.unshift(elem): 添加至数组头部
- array.pop(elem): 删除数组尾部
- array.shift(elem): 添加数组头部
- array1.concat(array2): 合并两个数组并返回一个新数组，1的元素在前

#### 

### 返回数组元素索引
数组名.indexOf(数组元素); //只满足第一个数组元素，找不到返回-1
```javascript
var phone = new Array("Xiaomi","Iphone");
console.log(phone.indexOf("Xiaomi")); //0
console.log(phone.indexOf("HuaWei")); //-1 未找到
```

### 数组转换字符串

- array.toString()

- array.join(分隔符)    //无参数时默认用","分割
  
  ```javascript
  var phone = new Array("Xiaomi","Iphone");
  console.log(phone.join("/"));  //'Xiaomi/Iphone' 
  ```


### 数组拷贝

```javascript
const itemsCopy = [...items];
```

### 数组遍历

#### forEach

```javascript
//参数: 数组当前项的值，数组当前项的索引，调用了该函数的数组本身;返回值为空
//array.forEach(function(currentValue, index, arr)){}    
{
  let a = [1,2,3,4]
  a.forEach(ele => console.log(ele)) //1 2 3 4
}
```

#### 筛选filter(返回新数组)

```javascript
 //参数：数组当前项的值,数组当前项的索引,调用了该函数的数组本身
 array.filter(function(currentValue, index, arr)){}    
 var arr = array.filter(currentValue, index)){
      return value >= 20;   //返回value大于等于20的数组项组成的数组
 }
 var arr = array.filter(value => value >= 20)
```

#### 筛选every(全部满足条件返回true)

```javascript
var arr = [10, 30, 4];
var flag = arr.every(function(value){
  return  value > 11;
});
console.log(flag); // false
```

#### 筛选some(找到一个满足条件的就返回True, or false)找唯一值Id等()

在some里面**return true可以终止迭代，效率更高**

```javascript
array.some(function(currentValue, index, arr)){}    //数组当前项的值，数组当前项的索引，调用了该函数的数组本身； 返回值为布尔，找到第一个就终止循环
var arr = array.filter(currentValue, index)){
      return value >= 20;   //返回value满足条件的值,有则返回true并终止循环
} 
```

### 回调函数处理数组(增强数据,返回新数组)map

```
array.map(function(element, index, array){}  //数组当前项的值，数组当前项的索引，调用了该函数的数组本身；
var a = [30,40,50];
function f(value) {
  return value*2;    
}
var a1=a.map(f);    //返回一个新数组，其中每个元素均为关联的原始数组元素的回调函数（f）返回值
console.log(a1);  //60,80,100
```

<br/>

<br/>

# 函数

## 定义

```javascript
//function 函数名(参数){}

var f = new Function('a','b','console.log(a+b)');    //了解
f(1,2); //3
```

![b338a5391bf096bc832c154dd2c078cd.png](C:\Users\Ly199\Desktop\b338a5391bf096bc832c154dd2c078cd.png)



函数都是有返回值的，没有return返回undefined

<br/>

## 构造函数

用于初始化对象，可将对象中公共属性抽取出来封装进去

```
function 构造函数名(形参,形参···){
    this.属性 = 形参;
    ···
}
var 对象名 = new 构造函数名(实参,实参···);
```

JavaScript的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的this 上添加。通过这两种方式添加的成员，就分别称为静态成员和实例成员。

静态成员:在**构造函数本身上**添加的成员称为静态成员，只能由**构造函数本身**来访问

实例成员:在**构造函数内部创建**的对象成员称为实例成员，只能由**实例化的对象**来访问

```javascript
function foo(){
    this.show = function(){ //实例成员
        return this;
    }
}

foo.test = 123; //静态属性，静态成员

foo.say = function(){ //静态成员
    return this;
}
foo.say();

var fn = new foo(); //实例化的新的对象，this指向这个新的对象，不能访问类的静态方法
fn.say(); //Noname1.html:45 Uncaught TypeError: fn.say is not a function
console.log(foo.say() == fn.say());
```

<br/>

## 原型

### 构造函数原型

构造函数通过原型分配的函数是所有对象所共享的。

JavaScript 规定，每一个构造函数都有一个prototype属性，指向另一个对象。注意这个prototype就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。

我们可以把那些不变的方法，直接定义在prototype对象上，这样所有对象的实例就可以共享这些方法。

```javascript
构造函数名.prototype.方法名 = function(){} //把方法放到原型对象上 实现了对象之间方法的共享
```

### 对象原型

对象都会有一个属性\__proto__指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 proto 原型的存在。

- \__proto__对象原型和原型对象 prototype 是等价的
- \__proto__对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个**非标准属性**，因此实际开发中，**不可以使用**这个属性，它只是内部指向原型对象 prototype

<img src="5e4dc1a1df02ad16f5e9a9a1ee3d08a7.png" alt="截图" style="zoom:75%;" />

对象原型（ proto）和 构造函数（prototype）原型对象里面都有一个属性 constructor 属性 ，constructor 我们称为构造函数，因为它指回构造函数本身。

constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。

一般情况下，对象的方法都在构造函数的原型对象中设置。如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor 就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。

```javascript
构造函数.prototype = {
    constructor:构造函数名
    方法名:function(){},
    方法名:function(){}···
}
//这个时候原型没有constructor属性,需要在第一行重新赋值
```

### 原型链
JavaScript 中的原型链是一种实现对象继承的机制

#### 原型链的工作方式
1. 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性
2. 如果没有就查找它的原型（也就是 \__proto__指向的 prototype 原型对象）
3. 如果还没有就查找原型对象的原型（Object的原型对象）
4. 依此类推一直找到 Object 为止（null）

### JS的链式编程

链式编程实际是将多个方法（函数）通过某种方式链接在一起，使多个逻辑块能按流程逐步执行（或跳过执行），从而实现解耦。

```javascript
/* 链式 */
console.log(
    [1,2,3,4]
        .concat(5)
        .filter((item)=>(item<3))
        .concat(6)
        .join("")
);  // 输出 126

/* 非链式 */
const arr = [1,2,3,4];
const arr1 = arr.concat(5);
const arr2 = arr1.filter((item)=>(item<3));
const arr3 = arr2.concat(6);
console.log(arr3.join(""));
```

实现链式反应的本质为：每次该对象（Object-A）调用其方法（Method-1）时，**返回值仍为本对象**（Object-A），从而后面使用链式的方式再调用另外一个方法（Method-2）时，得到的this仍为原对象（Object-A），然后返回值同样（Object-A），从而仍可通过链式的方式再调用该对象上的别的方法（Method-3），以此类推。

在js上常见的链式编程有以下几种具体应用：

- 对象方法**return this**的链式操作
  
  - ```
    var myObj = {
        name: '',
        setName: function(newName) {
            this.name = newName;
            // 要实现在调用setName方法后仍能链式调用myObj的其他方法就必须返回this，即返回myObj
            return this;
        },
        addStr: function(str) {
            this.name += str;
            return this;
        },
        consoleName: function() {
            console.log(this.name);
            return this;
        }
    };
    
    myObj
        .setName('帅哥')
        .addStr('就是我')
        .consoleName();     // 输出'帅哥就是我'
    ```

- Promise

- 责任链（Chain of responsibility）

<br/>

## 闭包

有权访问**另一个函数作用域中变量**的函数，**变量所在的函数**就是闭包

```javascript
function fn(){
  var num = 10;

  return function fun(){
    console.log(num);
  }
}
var f = fn(); //fun()
f();
//closure: fn
```

作用：延伸了变量的作用范围

<br/>

## 参数默认值

参数可以省略，省略的参数应该放到最后一个参数

```javascript
{
    let a = (x,y=1) => console.log(x+y);
    a(1);    //2
    a(3,2)    //5
}
```

<br/>

## 立即执行函数

不需要调用，立马能够自己执行的函数

独立创建了一个作用域，函数带不带名字都可以

作用：创建独立作用域

```javascript
//1
(function(形参){
...
})(实参);
//2
(function(形参){
...
}(实参));
//3
((形参) => {
  console.log('Welcome to the Internet.');
})(实参);
```

<br/>

## 箭头函数

```javascript
var f = v => v;

// 等同于
var f = function (v) {
  return v;
};

//如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分。
var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```

箭头函数没有自己的this对象，内部的this就是**定义时上层作用域中的this**。也就是说，箭头函数内部的this指向是固定的，相比之下，普通函数的this指向是可变的。

### 不适用场景

#### 定义对象的方法，且该方法内部包括this

```javascript
//调用cat.jumps()时，如果是普通函数，该方法内部的this指向cat；
//如果写成箭头函数，使得this指向全局对象，因此不会得到预期结果。
//这是因为对象不构成单独的作用域，导致jumps箭头函数定义时的作用域就是全局作用域。
const cat = {
  lives: 9,
  jumps: () => {
    this.lives--;
  }
}
```

#### 需要动态this的时候

```javascript
var button = document.getElementById('press');
button.addEventListener('click', () => {
  this.classList.toggle('on');
});
```

button的监听函数是一个箭头函数，导致里面的this就是全局对象。如果改成普通函数，this就会**动态指向被点击的按钮对象**。

<br/>

## 严格模式

### 定义

作用域最开始添加’use strict‘，该作用域就是严格模式

### 规范

正常模式下变量可以不声明直接赋值，默认变量为**全局变量**
严格模式必须**先声明后使用**
严禁删除**已经声明过的变量**
严格模式下全局作用域中函数**this指向undefined** 
严格模式下构造函数不加new调用，**this会报错**函数中不能有重名的参数

<br/>

## 应用

### 可以指定某一个参数不得省略，如果省略就抛出一个错误

```
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
// Error: Missing parameter
```

<br/>

<br/>

# This

## 指向

1. 单独使用: 拥有者是全局对象，this指的是全局对象
2. 方法中的this: 
   1. 在对象方法中，this指的是此方法的拥有者，代表对象本身
   2. 在事件方法中，this指的是绑定该事件的元素
3. 函数中的this:
   1. 普通函数，定时器函数，立即执行函数，回调函数的this指的是全局对象
   2. 在构造函数中，this指向实例对象
   3. 箭头函数没有自己的this值，箭头函数中所使用的this都是来自函数作用域链

<br/>

## 改变函数内部指向

### call方法

调用函数，改变函数内部指向实现继承

```
函数名.call(对象,实参,实参...)
```

### apply方法

和call基本一致，参数用数组传递

```javascript
fn.call(obj, 1, 2);
fn.apply(obj, [1, 2]); //第一个参数为this指向，第二个参数是数组
```

### bind方法(重要)

改变函数内部指向，不调用函数，返回一个新函数

```javascript
函数名.bind(对象,实参,实参···)

var o = {name : 'ly'};
function fn(){
    console.log(this); //指向window
}
var f = fn.bind(o);
f(); //指向o

//用法
function(···){···}.bind(this)
```

<br/>

<br/>

# 解构赋值

```javascript
let [a, b, c] = [1, 2, 3];
```

如果解构不成功，变量的值就等于undefined。

<br/>

## 对象解构

```
//后台内部类
Wrapper a = new Wrapper();
a.Name = 'ly';
a.Age = 18;

//js对象解构
let {Name,Age} = a;
console.log(Name + '-' + Age);
```

<br/>

## 用途

### 交换变量值

```javascript
let x = 1;
let y = 2;
[x, y] = [y, x];
```

### 提取JSON数据

```javascript
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);
// 42, "OK", [867, 5309]
```

### 遍历Map结构

```javascript
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```

<br/>

<br/>

# Web API

BOM(浏览器功能),DOM(页面元素)

DOM(文档对象模型):处理HTML或XML的API(网页)，改变网页的内容、结构、样式

DOM树:文档-元素（元素就是标签）-节点(可以把他们都看成对象),一个页面就是一个文档

DOM：操作元素

<br/>

## DOM

### 节点

在js中**页面由节点组成**，一个节点就是一个**对象**

- 节点类型
  
  1. 元素节点（div等）nodeType=1
  2. 属性节点（div class=""）nodeType=2
  3. 文本节点    nodeType=3
  4. 其他查文档

- 节点名称 只读
  
  - 节点名称就是DOM节点的名字，不同类型的节点对应不同的节点名称

- 节点值
  
  - 对于文本节点，节点值为文本内容；对于属性节点，节点值为属性的值。
    
    节点值对于文档节点和元素节点是不可用的。

换行和空格都是文本节点

#### 节点层级

![b120725efea9e7984bcf5766a508ca14.png](C:\Users\Ly199\Desktop\b120725efea9e7984bcf5766a508ca14.png)



- 父节点
  
  - ```javascript
    var son = document.querySelector('.类名');
    var father = son.parentNode; //得到的是最近的父亲 找不到返回null
    ```

- 子节点
  
  - ```javascript
    parentNode.childNodes //包含元素节点，文本节点
    parentNode.children //获取所有的子元素节点
    parentNode.firstChild
    parentNode.lastChild
    ```

- 同级节点
  
  - ```javascript
    node.previousSibling  //上一个哥哥节点，找不到返回null
    node.nextSidling  //下一个弟弟节点，找不到返回undefined
    ```

#### 节点操作

```javascript
var li = document.createElement('li'); //创建节点
var ul = document.querySelector('ul');
ul.appendChild(li); //添加节点
ul.removeChild(ul.children[0]); //删除节点
ul.cloneNode(); //复制节点 如果括号参数为空 or false, 浅拷贝(只复制节点本身，不复制子节点)； true为深拷贝
```

### 常用方法

#### 获取元素

```javascript
var ele = document.getElementById('id');  //根据id获取元素
var ele = document.getElementByTagName('td');  //根据标签名获取元素
var ele = document.getElementByClassName('className');  //根据类名获取元素
var ele = document.querySelector('.id');  //根据选择器获取元素  #id名，标签名
var eles = document.querySelector('.id');  //根据选择器获取元素，返回nodeList
```

#### 操作元素内容

```
var div = document.querySelector('div');

div.innerText = '<strong>a</strong>'; //输出："strong>a</strong>"

div.innerHTML = '<strong>a</strong>'; //输出："a"(粗体)
```

#### 操作元素属性

element.style

element.className    //将样式写进类中修改类名属性

#### 给元素设置自定义属性

```
<div data-index="1"></div>
element.setAttribute('data-index',2)
```

### PC端网页特效

#### 元素偏移量offset

offset系列属性作用element.offsetParent返回作为该元素带有定位的父级元素如果父级都没有定位则返回bodyelement.offsetTop返回元素相对带有定位父元素上方的偏移element.offsetLeft返回元素相对带有定位父元素左边框的偏移element.offsetWidth返回自身包括padding、边框、内容区的宽度，返回数值不带单位element.offsetHeight返回自身包括padding、边框、内容区的高度，返回数值不带单位### offset和style区别
![截图](6e3b45a9f5391b7fa644c6e8d67347ee.png)

#### 元素可视区client

不包含边框

client系列属性作用element.clientTop返回元素上边框的大小element.clientLeft返回元素左边框的大小element.clientWidth返回自身包括padding、内容区的宽度，不含边框，返回数值不带单位element.clientHeight返回自身包括padding、内容区的高度，不含边框，返回数值不带单位

#### 元素滚动scroll

scroll滚动事件，内容实际高度宽度

scroll系列属性作用element.scrollTop返回被卷去的上侧距离，返回数值不带单位element.scrollLeft返回被卷去的左侧距离，返回数值不带单位element.scrollWidth返回自身实际的宽度，不含边框，返回数值不带单位element.scrollHeight返回自身实际的高度，不含边框，返回数值不带单位

#### 用法

offset系列经常用于获得元素位置： offsetLeft offsetTop client经常用于获取元素大小： clientWidth clientHeight scroll经常用于获取滚动距离： scrollTop scrollLeft 注意页面滚动的距离通过window.pagexoffset 获得

<br/>

## BOM

浏览器对象模型，把浏览器当作一个对象，浏览器大小，跳转，页面条滚动等

### window对象

顶级对象是window，js访问浏览器窗口的接口

所有定义在全局作用域中的变量、函数都会变成window对象的属性和方法，在调用的

时候可以省略window

```
window.open(url) === open(url)  //打开窗口
window.close() === close()  //关闭窗口
window.event === event  //获取事件
window.document === document  //获取文档
```

var命令和function命令声明的全局变量，依旧是顶层对象的属性

let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。

#### 常用属性

##### name

window下的一个特殊属性window.name，默认值为空

##### 浏览器距离屏幕距离

window.screenX,window.screenY

#### 常用方法

| 方法            | 描述          |
| ------------- | ----------- |
| alert()       | 警告框         |
| prompt()      | 输入框         |
| confirm()     | 确认框         |
| focus()       | 键盘焦点给予一个窗口  |
| blur()        | 键盘焦点从顶层窗口移开 |
| setTimeout()  | 定时器         |
| setInterval() | 间隔执行定时器     |

#### 常用事件

##### 页面加载事件(两种)

当文档内容完全加载完成会触发该事件

```javascript
window.onload = function(){};
window.addEventListener('load',function(){});
window.addEventListener('DOMContentLoaded',function(){});
```

注意：有了window.onload就可以把js代码写在页面元素上方，因为onload是等页面内容全部加载完毕，再去执行处理函数

- DomContentLoaded 事件的触发**(快)**
  
  - DOMContentLoaded 事件在 html文档加载完毕，并且 html 所引用的内联 js、以及外链 js 的同步代码都执行完毕后触发。

- load 事件的触发**(慢)**
  
  - 当页面 DOM 结构中的 js、css、图片，以及 js 异步加载的 js、**css 、图片都加载完成之后**，才会触发 load 事件。

##### 调整窗口大小事件

```javascript
window.onresize = function(){};
window.addEventListener('resize',function(){});
```

### navigator对象

#### 常用属性

userAgent: 返回浏览器内核(如果出现**Mobile**说明用户使用的是移动端)

### location对象

#### 常用属性

| location对象属性      | 返回值                   |
| ----------------- |:--------------------- |
| location.href     | 获取或者设置整个url           |
| location.host     | 返回主机域名(www.baidu.com) |
| location.port     | 返回端口号    未写返回空字符串''   |
| location.pathname | 返回路径                  |
| location.search   | 返回参数(url问号?后的部分)      |
| location.hash     | 返回片段 #后面内容 常见于链接，锚点   |

#### 常用方法

| location对象方法       | 返回值    |
| ------------------ | ------ |
| location.assign()  | 跳转页面   |
| location.replace() | 替换当前页面 |
| location.reload()  | 重新加载页面 |

### history对象

#### 常用方法

| history对象方法 | 作用                  |
| ----------- | ------------------- |
| back()      | 后退                  |
| forward()   | 前进                  |
| go(参数)      | 参数=1前进1个页面，-1后退1个页面 |





# 事件

事件三要素

- 事件源：事件被触发的对象(eg. 按钮) 
- 事件类型：如何触发 什么事件(eg. 鼠标点击(onclick))
- 事件处理程序：通过一个函数赋值的方式完成

执行事件的顺序：

1. 获取事件源
2. 注册事件
3. 添加事件处理程序

<br/>

## 传统事件注册

同一个元素同一个事件只能设置一个处理函数，最后处理的处理函数将会覆盖前面注册的处理函数

```
<button id="btn">唐伯虎</button>    //事件源
<script>
    var btn = document.getElementById('btn');    //获取事件源
    btn.onclick = function(){    //注册事件，添加事件处理程序
        alert('点秋香')
         btn.onclick = null //解绑事件
    }
</script>
```

<br/>

## 方法监听注册事件

addEventListener(type, listener[, useCapture])

第三个参数为**true**，则为捕获阶段 **document->body->父节点->子节点**

**false为冒泡阶段 子节点~~~~document**

```
var btn = document.querySelectorAll('button');
btn[0].addEventListener('click',function(){
    alert('事件被触发');
})
btn[0].removeEventListener('click',函数名); //解绑事件
```

<br/>

## DOM事件流

![482fddfd04f915aac40753718e6a533b.png](C:\Users\Ly199\Desktop\482fddfd04f915aac40753718e6a533b.png)



DOM事件流分为3个阶段：

1. 捕获阶段
2. 当前目标阶段
3. 冒泡阶段

### 注意

1. JS代码中只能执行捕获或者冒泡其中一个阶段
2. onclick 和 attachEvent 只能得到冒泡阶段
3. 如果 addEventListener 第三个参数是true处于捕获阶段，false或省略处于冒泡阶段
4. 实际开发中我们更关注事件冒泡
5. 有些事件是没有冒泡的，比如 onblur, onfocus, onmouseenter, onmouseleave

### 捕获阶段

如果 addEventListener 第三个参数是true，则处于捕获阶段。

捕获阶段：document -> html -> body -> father -> son

### 冒泡阶段

如果 addEventListener 第三个参数是false或省略，则处于冒泡阶段。

冒泡阶段：son -> father -> body -> html -> document

### 事件委托(通过冒泡)

原理：不给每个子节点单独设置监听器，而是**设置在父结点上**，然后利用**冒泡原理影响设置每个子节点**

作用：只操作一次DOM，提高了程序的性能

使用e.target获得子节点

<br/>

## 事件对象

注册事件时，事件对象自动创建

### 常用方法

```
event.target  //返回触发事件的对象
event.type  //返回事件类型(eg. click, mouseover)不带on
event.preventDefault()  //组织默认事件(eg. 不让链接跳转，不让表单提交)
event.stopPropagation() //阻止冒泡
```

<br/>

## 防抖

用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完后，才执行查询的请求，这样可以有效减少请求次数，节约请求资源

```
var timer = null    //防抖动的timer
//定义防抖的函数
function debounceSearch(keywords){
    timer = setTimeout(function(){
        后台方法(keywords)                
    }, 500)
}

var input = document.querySelector('input');
//触发keyup的时候清空timer
input.addEventListener('keyup', function(){
    //清除计时器后重新计时
    clearTimeout(timer);  
    debounceSearch(keywords);
})
```

## 节流

减少事件触发频率

```
//定义节流阀
var timer = null
//注册绑定事件
item.addEventListener('事件名', function(){
  //判断节流阀是否为空
  if(timer) { return }
  timer = setTimeout(function(){
    ··· //省略代码
    timer = null  //清空节流阀
  }, 16)  //事件触发频率,一帧动画16.7ms
})
```

<br/>

## 防抖和节流区别

防抖：如果事件被频繁触发，防抖能保证只有最有一次触发生效！前面N多次的触发都会被忽略

节流：如果事件被频繁触发，节流能够减少事件触发的频率，因此，节流是有选择性地执行部分事件！

# Promise对象

## 用法

- 对象状态不受外界影响。只有**异步操作的结果可以决定当前状态**。三种状态: **pending(进行中), fulfilled(已成功), rejected(已失败)**
- 状态改变后就**不会再变**。pending =>fulfilled or pending => rejected。当状态改变后，可以通过调用回调函数返回结果
- 构造函数接收一个函数作为参数，该函数的两个参数分别是resolve和reject（两个函数）
- resolve函数的作用：将Promise对象的状态从从 pending 变为 resolved，在异步操作成功时调用，并将异步操作的结果，作为参数传递出去
- reject函数的作用是，将Promise对象的状态从pending 变为 rejected，在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

<br/>

## then方法

Promise实例生成以后，可以用**then方法**分别指定resolved状态和rejected状态的回调函数。

then方法可以接受**两个回调函数**作为参数。

第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。

```javascript
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

实例

```javascript
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```
