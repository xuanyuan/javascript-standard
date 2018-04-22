## JS常见注意点，编码规范

### 立即执行函数
```javascript
// 立即执行函IIFE(Immediately Invoked Function Expression)

(function () {
    // code
})();
// 在以下情况会报错
var a = 1
(function () { // Uncaught TypeError: 1 is not a function
    // code
})
// 被理解成为 var a = 1 (function (){})()
// 应该改为
void function() {
}();
```
### 检查变量是否为对象
```javascript
// 首先判断他是否为null
if (someVal !== null && typeof someVal === 'object') {
    // code
}
```
### NaN !== NaN
```javascript
NaN === NaN // false
var a = NaN; a === a // false

isNaN('abc') // true
isNaN('123') // false
isNaN('') // false
isNaN([]) // false
isNaN({}) // true
isNaN(123) // false
```
**永远不要写 someValue === NaN**
### 正确使用 parseInt
使用规则一：请传入第二参数
parseInt的第一个参数为待parse的字符串（如果不是字符串则会首先转换为字符串）;第二个参数为使用的进制数

```javascript
parseInt(0.0000000008) = ?
=>
String(0.0000000008)=>'8e-10'
parseInt('8e-10')=>8
```
使用规则二：永远不要使用parseInt给小数取整
建议数值转换一概使用强制转换函数Number，或+（正号）

除了用于比较null或undefined，永远不要使用非严格相等==
关于非严格相等，记住以下规则：
```javascript
null == null //=> true
null == undefined //=> true
undefined == null //=> true
undefined == undefined //=> true
x == null //=> false(x非null或undefined)
x == undefined //=> false(x非null或undefined)
```
简言之
x == null // 或 x = undefined
是最简单的判断x为null或undefined的方式，相对应的
x != null // 或 x != undefined
是最简单的判断x非null和undefined的方式。这就是==存在的唯一意义

慎用||填充默认值
expr1 || expr2的意思是：如果expr1能转换成true则返回expr1，否则返回expr2
expr1 || expr2 <=> Boolean(expr1) ? expr1 : expr2
哪些值不能转换为true呢？
1. null
2. undefined
3. NaN
4. 0
5. ''(空字符串)

如果用户指定了传入参数的值为0或者是空字符串的配置项，它的值就会被强制替换为默认值，然而实际上只有undefined
应该被认为是用户没有指定其值（语义上可以理解：null表示用户让你给他把这个值空着;而undefined表示用户没发表意见）
所以就应该是这样：
```javascript
config.prop1 = config.prop1 !== undefined ? config.prop1 : 233;
config.prop2 = config.prop2 !== undefined ? config.prop2 : 'balabala';
```

不要使用for_in遍历数组
使用for_in遍历数组的问题：
1. 遍历顺序不固定
2. 会遍历出对象原型链上的值
3. 运行效率低下

不要用JSON.parse(JSON.stringify())深拷贝数组
问题：
1. 会使某些特定值转换为null
NaN,undefined,Infinity对于JSON中不支持的这些值，会在序列化JSON时被转换成null，反序列化回来后也是null
2. 会丢失值为undefined的键值对
JSON序列化时会忽略值为undefined的key,反序列化回来后自然也丢失了
3. 会将Date对象转换为字符串
JSON不支持Date对象类型，会将其转换成ISO8601格式的字符串。然而反序列化并不会把时间格式的字符串转换为Date对象

#### 不要用 arr.find 代替 arr.some
Array.prototype.find 返回第一个符合条件的值，直接拿这个值做 if 判断是否存在，如果这个符合条件的值恰好是 0 怎么办？
arr.find 是找到数组中的值后对其进一步处理，一般用于对象数组的情况；
arr.some 才是检查存在性；两者不可混用。

#### 对数组排序时，永远记得传入比较函数
arr.sort 默认会将数组中所有元素转换成字符串后以字典序排序。例如：
```javascript
[1,2,3,4,5,6,7,8,9,10].sort() // => [1,10,2,3,4,5,6,7,8,9]
```
除非你是给字符串数组排序，否则请给它传入一个比较函数。
```javascript
[1,2,3,4,5,6,7,8,9,10].sort((x, y) => y - x) // => [ 10, 9, 8, 7, 6, 5, 4, 3, 2, 1 ]
[1,2,3,4,5,6,7,8,9,10].sort((x, y) => x - y) // => [ 10, 9, 8, 7, 6, 5, 4, 3, 2, 1 ]
```

补：forEach 与 break
ES6 以前，遍历数组主要就是两种方法：手写循环用下标迭代，使用 Array.prototype.forEach。
前者万能，效率最高，可就是写起来比较繁琐——它不能直接获取到数组中的值。

forEach 接受一个回调函数，你可以提前 return，相当于手写循环中的 continue。
但是你不能 break——因为回调函数中没有循环让你去 break：
```javascript
[1, 2, 3, 4, 5].forEach(x => {
  console.log(x);
  if (x === 3) {
    break;  // SyntaxError: Illegal break statement
  }
});
```
考虑 Array.prototype.some 的特性，当 some 找到一个符合条件的值（回调函数返回 true）时会立即终止循环，利用这样的特性可以模拟 break：
```javascript
[1, 2, 3, 4, 5].some(x => {
  console.log(x);
  if (x === 3) {
    return true; // break
  }
  // return undefined; 相当于 false
});
```
在 ES6 前，使用该法（），ES6 不一样了，我们有了 for...of。
for...of 是真正的循环，可以 break：
```javascript
for (const x of [1, 2, 3, 4, 5]) {
  console.log(x);
  if (x === 3) {
    break;
  }
}
```
但是有个问题，for...of 似乎拿不到循环的下标。
其实 JavaScript 语言制定者想到了这个问题，可以如下解决：
```javascript
for (const [index, value] of [1, 2, 3, 4, 5].entries()) {
  console.log(`arr[${index}] = ${value}`);
}
```
Array.prototype.entries

for...of 和 forEach 的性能测试：
https://jsperf.com/array-fore... Chrome 中 for...of 要快一些