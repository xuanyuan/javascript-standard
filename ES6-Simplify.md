### 1.对象属性简写
```javascript 1.6
// 属性名和key名相同
const obj = {x:x, y:y}
// 简写为
const obj = {x, y}
```
### 2.箭头函数
```javascript 1.6
function sayHello(name) {
    console.log('hello', name);
}
setTimeout(function() {
    console.log('Loaded')
}, 2000);
list.forEach(function (item) {
    console.log(item);
})
// 简写
sayHello = name => console.log('hello', name);
setTimeout(() => console.log('loaded'), 2000);
list.forEach(item => console.log(item));
```
### 3.隐式返回值简写
```javascript 1.6
function calcCircumference(diameter) {
    return Math.PI * diameter;
}
var func = function func() {
  return {foo: 1};
};
// 简写为
calcCircumference = diameter => (
    Math.PI* diameter;
)
var func = () => ({foo: 1});
```
### 4.默认参数值
```javascript
volume = (1, w = 3, h = 4) => (1 * w * h);
volume(2) // output:24
```
### 5.解构赋值简写方法
```javascript
const observable = require('mobx/observable');
const action = require('mobx/action');
const runInAction = require('mobx/runInAction');

const store = this.props.store;
const form = this.props.form;
const loading = this.props.loading;
const errors = this.props.errors;
const entity = this.props.entity;
// 简写为
import { observable, action, runInAction } from 'mobx';
const { store, form, loading, errors, entity } = this.props;
// 也可以分配变量名
const { store, form, loading, errors, entity: contact } = this.props;
```
### 6.扩展运算符简写
```javascript
// joining arrays
const odd = [1, 3, 5];
const nums = [2, 4, 6].concat(odd);

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = arr.slice();

// 简写：
// joining arrays
const odd = [1, 3, 5];
const nums = [2, 4, 6, ...odd];

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```
**使用扩展运算符解构:**
```javascript
const { a, b, ...z } = {a: 1, b: 2, c: 3, d: 4 };
console.log(a) // 1
console.log(b) // 2
console.log(z) // { c: 3, d: 4}
```

# 箭头函数括号问题，闭包

