## Front_End JavaScript Code Standard ##

### 1. 基本格式化
#### 1.1. 缩进层级
设置Tab键为插入四个空格
#### 1.2. 语句结尾
不要省略分号
#### 1.3. 行的长度
源码单行长度不超过80个字符，文档中代码单行长度不超过70个字符
#### 1.4. 换行
通常我们会在运算符后换行，下一行会增加两个层级的缩进。
```javascript
// 好的做法
callAFunction(document, element, window, "some string value", true, 123,
        navigator);
// 对于语句来说，同样也可以应用下面这种换行规则
if (isLeapYear && isFebruary && day == 29 && itsYourBirthday &&
        noPlans) {
    // 主体部分依然是一个缩进 
    waitAnotherFourYears();
    }
```
注：当给变量赋值时，第二行的位置应当和赋值运算符的位置保持对齐。
```javascript
var result = something + anotherThing + yetAnotherThing + somethingElse +
             anotherSomethingElse;
```
#### 1.5. 空行 ####
在每个流控制语句之前(if, for)添加空行。
以下四种情况添加空行：

 1） 在方法之间
 
 2） 在方法中的局部变量和第一条语句之间
```javascript
function func() {
    var var;
    // 空行
    // 你的代码
}
```
 3） 在多行或单行注释之前
```javascript
function doSomething() {
    
    // 注释
    code...

    /*
     *...
     */
    code...  
}
```
 4）在方法内的逻辑片段之前插入空行，提高可读性

#### 1.6. 命名
 (小)驼峰式大小写:小写字母开始，后续每个单词首字母都大写
##### 1.6.1. 变量和函数
 变量名总是遵守驼峰大小写命名法，命名前缀应当是名词。
 
 以名词作为前缀可以让变量和函数区分开来，因为函数名前缀应当是动词。

 命名长度应该尽可能短，尽量在变量名中体现出值的数据类型。
 
 数字：count,length和size
 
 字符串： name,title,message
 
 单个字符命名的变量诸如i,j,k通常在循环中使用

 函数和方法命名来说，第一个单词应该是动词
 can,has,is 返回一个布尔值
 get        返回一个非布尔值
 set        保存一个值

##### 1.6.2常量
 大写字母和下划线来命名，下划线用以分隔单词
```javascript
const MAX_COUNT
const PI
```

##### 1.6.3构造函数
 大驼峰命名法，常常是名词
#### 1.7直接量
```javascript
// 多行字符串
var longString = "hello here's the story of a man " +
                 "named Brady.";
```
##### 1.7.2数字
整数和浮点数——都存储为相同的数据类型
```javascript
// 整数
var count = 10;

// 十六进制写法
var num = 0xA2;

// 小数
var price = 10.0;
var price = 10.00;

// 科学计数法
var num = 1e23;
```

##### 1.7.3 null

**应使用null场景**

1）用来初始化一个变量，这个变量可能赋值为一个对象。

2）用来和一个已经初始化的变量比较，这个变量可以是也可以不是一个对象

3）当函数的参数期望是对象时，用作参数传入

4）当函数的返回值期望是对象时，用作返回值传出

**不应当使用null**

1）不要使用null来检测是否传入了某个参数

2）不要用null来检测一个未初始化的变量
```javascript
// 好的做法,初始化一个变量
var person = null;
// 好的做法，用来和一个已经初始化的变量比较
var person = getPerson();
if (person !== null) {
    doSomething();
}
// 好的做法，用作返回值传出
function getPerson() {
    if (condition) {
        return new Person('Nich');
    }
    else {
        return null;
    }
}
```
**null最好的方式是将它当做对象的占位符**

##### 1.7.4 undefined
```javascript
// foo 未被声明
var person;
console.log(typeof person); // "undefined" === typeof person // true
console.log(typeof foo);    // "undefined" === typeof foo    // true 
// 不管值是undefined的变量还是未声明的变量
typeof undefined === "undefined" // true
typeof null === "object"         // true
'a' === "a" // true 
```
##### 1.7.5 对象直接量
创建对象最流行的一种做法是使用对象直接量，在直接量中直接写出所有属性。
```javascript
// 好的做法
var book = {
    title: "JavaScript",
    author: "Nichalas"
};

/*
 *当定义对象直接量时，常常在第一行包含左花括号，
 *每一个属性的键值对都独占一行，并保持一个缩进，
 *最后右花括号也独占一行
 */
```
##### 1.7.6 数组直接量
不赞成显式地使用Array构造函数创建数组
```javascript
// 好的做法
var colors = ["red", "green", "blue"];
var numbers = [1, 2, 3, 4];
```

### 2 注释
#### 2.1单行注释
使用方法：

1）独占一行的注释，用来解释下一行代码。这行注释之前总是有一个空行，且缩进层级和下一行代码保持一致

2）在代码行的尾部的注释。代码结束到注释之间至少有一个缩进。注释(包括之前的代码部分)不应当超过单行最大最大字符数限制，如果超过了，就将这条注释放置于当前代码行的上方。

3）被注释掉的大段代码

单行注释不应当以连续多行注释的形式出现，除非你注释掉一大段代码。只有当需要注释一段很长的文本时才使用多行注释。
```javascript
// 好的做法
if (condition) {
    
    // 如果代码执行到这里，则表明通过了所有检查
    allowed();
}

// 好的做法
// if (condition) {
//     doSomething();
//     thenDoSomethingElse();
// }
```
#### 2.2多行注释
```javascript
/*
 *另一段注释
 *这段注释包含两行文本
 */
```
java风格的注释：第一行是/*
第二行是以*开始且和上一行的*保持左对齐
最后一行是*/

多行注释总是会出现在将要描述的代码段之前，注释和代码之间没有空行间隔。和单行注释一样，多行注释之前应当有一个空行,且缩进层级和其描述的代码保存一致。
```javascript
if (condition) {
    
    /*
     * 如果...
     * 说明...
     */
    allowed();
}
```
#### 2.3 使用注释
添加注释的一般原则是，在需要让代码变得更清晰时添加注释

### 3 语句和表达式
```javascript
// 好的做法
if (condition) {
    doSomething();
}
``` 
所有的块语句都应当使用花括号，包括
if、for、 while、 do...while、 try...catch...finally

#### 3.1 花括号的对齐方式
推荐：将左花括号放置在块语句中第一句代码的末尾。
```javascript
if (condition) {
    doSomething();
}
else {
    doSomethingElse();
}
```
#### 3.2 块语句间隔
块语句首行附近的空白行同样需要注意：
在左圆括号之前和右圆括号之后各添加一个空格
```javascript
if (condition) {
    doSomething();
}
```
#### 3.3 switch
switch语句中可以使用任意类型值，任何表达式都可合法地用于case从句
##### 3.3.1 缩进
```javascript
switch (condition) {
    case 'first':
        // 代码
        break;

    case "second":
        // 代码
        break;

    default:
        // 代码 

}
```
1）每条case语句相对于switch关键字都缩进一个层级
2）从第二条case语句开始，每条case语句前后各有一个空行

#### 3.6 for-in循环
不仅遍历对象的实例属性，还遍历从原型继承来的属性;
最好使用hasOwnProperty()方法来为for-in循环过滤出实例属性
var prop;

for (prop in Object) {
    
    if (Object.hasOwnProperty(prop)) {
        console.log(prop);
        console.log(Object[prop]);
    }
}

*Crockford的编程规范要求所有的for-in循环都必须用hasOwnProperty()。
*for-in循环是用来对实例对象和原型链中的键(key)做遍历的，而不是用来遍历包含数字索引的数组的，因此for-in循环不应当用于数组

### 4 变量、函数和运算符
#### 4.1变量声明
JS中允许多次使用var语句，此外var语句几乎可以用在JS脚本中的任意地方。所有的var语句都提前到包含这段逻辑的函数的顶部执行。
*建议总是将局部变量的定义作为函数内第一条语句
```javascript
function doSomethingWithItems(items) {
    var value= 10,
        result = value + 10,
        i,
        len;

    for (i = 0, len = items.length; i < len; i++) {
        doSomething(items[i]);
    }
}
```
将所有的var语句合并为一个语句，每个变量的初始化独占一行，赋值运算符应当对齐。
对于那些没有初始值的变量来说，他们应当出现在var语句尾部
为了保持成本最低，推荐合并var语句，代码更短，下载更快

#### 4.2 函数声明
推荐先声明JS函数然后使用函数
```javascript
function doSomethingWithItems(items) {
    // 区别与块语句参数右圆括号之后仅有一个空格，左圆括号之前没有空格
}
```
函数声明不应当出现在语句块之内。
```javascript
// 以下为语句块的几种类型
{...}

if (condition) {

}

for () {

}
```

#### 4.3 函数调用间隔
一般情况下，对于函数调用写法推荐的风格是，在函数名和左括号之间没有空格，这样做是为了将她和块语句区分开来
```javascript
doSomething(items);

while (items) {
    // 代码逻辑
}
```
#### 4.4 立即调用的函数
javascript中允许声明匿名函数，并将匿名函数赋值给变量或属性
```javascript
var doSomething = function() {
    // 函数体
}
```
这种匿名函数 同样可以通过在最后加上一对圆括号来立即执行并返回一个值，然后将这个值赋值给变量
```javascript
var value = (function() {
    
    // 函数体
    return {
        message: 'Hi';
    }
}());
```
将函数用一对圆括号包裹起来
在第一行有一个标识符(左圆括号),表明这是一个立即执行的函数。

#### 4.5 严格模式
最好不要在全局作用域中使用"use strict"
```javascript
function doSomething() {
    "use strict";
    // code
}
```
#### 4.6 相等
1）如果将数字和字符串进行比较，字符串会首先转换为数字，然后执行比较
```javascript
5 == '5'     //true
25 == '0x19' //true
```

2）如果一个布尔值和数字比较，布尔值会首先转换为数字，进行比较
false->0, true->1

3）如果其中一个值是对象而另一个不是，则会首先调用对象的valueOf()方法，得到原始类型值再进行比较。如果没有定义valueOf(),则调用toString()。
之后的比较操作就和上文提到的多类型值比较的情形一样了。
```javascript
null == undefined; // true
```
由于强制类型转换的缘故，我们推荐不要使用\==和!=,而是应当使用=\==和!==。如果两个值的类型不同，则它们不相等。

##### 4.6.2 原始包装类型
JS中有个3种包装类型：String,Boolean和Number。每种类型都代表全局作用域中的一个构造函数，并分别表示各自对应的原始值的对象。
*强烈建议避免使用包装类型
