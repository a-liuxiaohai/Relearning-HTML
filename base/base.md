**1. var/let/const共同点**

 - 在全局作用域中定义的变量，都可以在函数中使用
 - 在函数声明中定义的变量，只能在函数及子函数中使用，涉及到函数的作用域
 - 函数中声明的变量就像声明了私有领地，外面无法访问

**不同点**

- var声明变量没有快级作用域，会存在最近函数或者全局作用域中，也存在window中
- let / const 有快级作用域，变量只会在快级作用域中有效，不会污染的一些变量
- let / const 在同一作用域下，不能重复定义变量名，声明时必须赋值
- const 常量，如果变量是值类型，那么不可以修改，如果是引用类型，是可以修改的



**2.for/in**

> for/in用来遍历对象的所有属性，主要用于遍历对象，不建议用来遍历数组

```js
let info = {
  name:'liuxiaohai',
  age: 26
}

for(let key in info){
  if(info.hasOwnProperty(key)){
    console.log('只要对象自身的属性，不含prototype'，key)
    console.log(info[key],'获取到对象的每一个值')
  }
}
```

**3.for/of**

> 用来遍历Array，String，Maps，Sets等可以迭代的数据结构，for/of遍历获取到的是值

```js
let arr = [1,2,3,4]
for(let value in arr){
  console.log(value,'获取到的是1，2，3，4')
}
```

**4.typeof**

> 用于返回一下的原始类型，number, string,boolean,function,object,undefined

```js
let a = 1  	 console.log(typeof a) //number
let b = '1'  console.log(typeof b) //string
let c      	 console.log(typeof c) //undefined 变量定义未赋值
function run() console.log(typeof run) // function 
let d = [1,2,3] console.log(typeof d)  // object
let e = {name:'liuxiaohai'} console.log(typeof e) //object
```

**5.instanceof**

> instaceof 运算符用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上

可以理解为是否为某个对象的实例，typeof不能区分数组，但是instanceof 可以

```js
let lxh = []   console.log(lxh instanceof Array) // true
let info = {}  console.log(info instanceof Array) // false
let info = {}  console.log(info instanceof Object)// true
```



---

### String的常用方法

**1.截取字符串**

> 使用 slice 、 substr 、 substring 函数都可以截取字符串

- slice 、 substring 第二个参数为截取的结束位置
- substr 第二个参数指定获取字符数量

```js
# slice() 提取某个字符串的一部分，并返回一个新的字符串，且不会改动原字符串。
let str = "liuxiaohai";
console.log(str.slice()); // liuxiaoahi 什么参数都不传，则完全复制一遍
console.log(str.slice(3)); //xiaohai 一个参数，从下标3开始截，直到最后
console.log(str.slice(3, 7)); // xiao从下标3的位置，截取到下标为7的位置

# substring() 效果和slice一样
# substr() 第二个参数指定获取截取字符串的数量
console.log(str.substr(3, 4)); // 从下标3的位置截取，截4个
```

**2.indexOf**

> 查找字符串，从开始获取字符串的位置，检测不到时返回-1

```js
console.log('liuxiaohai'.indexOf('0')) // 1 检测到了所以返回当前下标
console.log('liuxiaohai'.indexOf('0',3)) // 从第3个字符开始向后搜索
```

**3.includes 包含**

> 查找字符串中是否包含指定的子字符串。如果包含返回true，不包含为false

```js
let name = 'liuxiaohai'
name.includes('com') // false 不包含
```

**4.replace 替换字符串**

> replace 用于字符串资环操作

```js
let name = 'liuxiaohai'
let web = name.replace('xiaohai','mao')
console.log(web) //liumao
```

**5.repeat 重复生成**

>字符串repeat方法，可以重复生成一些字符，可以用于电话号吗的脱敏

案例:模糊后四位的电话号码 1897044****

```js
let phone = 18970446252
function formatPhone(phone,len=3){
  String(phone).slice(0,-1*len)+ '*'.repeat(len)
}
formatPhone(phone,4)
```

**6.split分割 join拼接**

> split 分割字符串，分成数组，不改变原字符串
>
> join Array方法，用于对数组的拼接，拼接成字符串

```js
let name = 'lixuiaohai & maoshuang'
console.log(name.split('&')) // ['liuxiaohai','maoshuang']

let arr = [1,2,3]
arr.join('') // 123
```



---

### Number

**1. parseInt 对数字取整**

```js
let num = '99liu'
parseInt(num) //99
```

**2.parseFlot 浮点数**

```js
let str = '18.55'
console.log(parseFlot(str)) // 18.55
```

**3.toFixed舍入操作**

```js
let num = 1.556
console.log(num.toFixed(2))  // 1.55
```

**4.Math.min最小值  Math.max最大值**

```js
console.log(Math.max(1,2,3)) // 3
console.log(Math.min(1,2,3)) // 1
```

**5.Math.ceil向上取整  Math.floor向下取整**

```js
console.log(Math.ceil(1.11))  // 2
console.log(Math.floor(1.55)) // 1
```

**6.Math.round四舍五入  Math.random随机数**

```js
Math.round(1.5) //2
Math.random(0,1) // 包括0但不包括1
```



---

### Date 时间

**1.new Date() 获取当前时间**

```js
let now = new Date() // 当前时间戳
let now = new Date('2028-02-22 03:25:02'); //指定时间
```

**2.封装时间处理函数**

```js
function dateFormat(date,foramt='YYYY-MM-DD HH:mm:ss'){
  // 格式获取的时间
  let config = {
    YYYY:date.getFullYear(),
    MM: date.getMonth()+1,
    DD: date.getDate(),
    HH: date.getHours(),
    mm: date.getMinutes(),
    ss: date.getSeconds()
  }
  // for/in 对格式进行替换，这样外面传递进来什么格式就可以进行获取相应的值
  for(let key in config){
    format = format.replace(key,config[key])
  }
  // 把结果返回出去
  return format
}
let date = newDate()
let formatDate = dateFormat(date,'YYYY-MM-DD')
```

