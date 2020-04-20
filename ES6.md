# ECMAScript 6

目标：学习完 ES6 可以掌握方便后续的开发，未来工作中大量使用 ES6 开发

1. ECMAScript 6 介绍
2. ECMAScript 6 新增语法
3. 内置对象的扩展
4. ECMAScript 6 降级处理（学习完node再讲）

## 1. ECMAScript 6 介绍

<!--01-介绍-ES6简介-->

ES -- ECMAScript

ECMA -- 欧洲计算机制造商协会

ECMA262标准 -- 第一版JS的标准

我们之前学习的是 ES5.1

2015年发布了ES6，并且更名为ES2015。决定以年号为版本号，并且每年发布一个新版本。

- ES2015
- ES2016
- ...

网上所说的ES7、ES8等等，只是人们推算的，因为官方从未承认什么ES7，ES8。网上所提到的ES7，正式名称应该是ES2016。

- 每一年，所有人可以给JS提议，提出JS需要哪些改进，并给出解决办法。
- 如果提议被采纳，进入草案阶段
- 第二年发布的新版，就会包括前一年的草案

### 1.1 为什么要学习ES6 ###

- 提供了更加方便的新语法，**弥补** JS 语言本身的**缺陷**，新增了便捷的语法
- 给内置对象（Array、String、....）增加了更多的方法。
- ES6 让 JS 可以开发复杂的大型项目，成为企业级开发语言
- 新的前端项目中大量使用 ES6 的新语法（今天学完，后面就大量使用了）

### 1.2 ECMAScript 6 是什么

- ECMAScript 6 又叫 ES2015，简称 ES6
- ES6 是继 ES4、ES5 之后的 JS 语言规范
- ES6 中增加了一些新的特性
- ES6 的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言
- 2015年6月发布

### 1.3 小结

- ES6 是新的 JS 的代码规范，提供了一些新特性，使我们可以开发大型应用
- ES6 弥补了 JS 语言本身的缺陷，增加了新语法，扩展了内置对象
- ES6用起来非常爽。因为语法非常人性化。

## 2. ECMAScript 6 新增语法

- let和const关键字
- 箭头函数
- 函数参数默认值
- 函数剩余参数
- Array对象扩展
- String对象扩展
- 新增对象Set
- 定义对象的简洁方式



- Promise（最后一天）

### 2.1 let 和 const

<!--02.1-语法-let-->

- let -- 用于声明变量
  - let 定义变量，变量不可以再次定义，但可以改变其值

  - 具有块级作用域

  - 没有变量提升，必须先定义再使用

  - let声明的变量不会压到window对象中，是独立的

  - 代码演示

    ```js
    // 1. let 定义变量，变量不可以再次定义，但可以改变其值
    let name = 'zhangsan';
    name = 'lisi';
    console.log(name); // lisi
    let name = 'wangwu'; // 再次定义，报错：Identifier 'name' has already been declared
    ```

    ```js
    // 2. 具有块级作用域，块就是大括号
    {
        let age = 18;
        console.log(age); // 18
    }
    console.log(age); // 报错，此作用域中没有age的定义
    
    for (let i = 0; i < 10; i++) {
        // i 只能在此范围内使用，因为有块级作用域
    }
    console.log(i);  // 报错，此作用域中没有age的定义
    ```

    ```js
    // 3. 没有变量提升，必须先定义再使用
    console.log(gender); // 报错，此时还没有定义gender
    let gender = '男'; 
    ```

    ```js
    // 4. let声明的变量不会压到window对象中，是独立的
    let hobby = '吃饭';
    console.log(window.hobby); // undefined
    ```

> 如果使用var声明了变量，也不能再次用let声明了，反之也是不行的。
>
> 原因也是这个变量已经被声明过了。
>
> 不过这只是一种特殊情况了，实际开发要么全部使用var，要么全部使用let。

- const -- 用于声明常量（值不能改变）

  - 使用const关键字定义常量

  - 常量是不可变的，一旦定义，则不能修改其值

  - 初始化常量时，必须给初始值

  - 具有块级作用域

  - 没有变量提升，必须先定义再使用

  - 常量也是独立的，定义后不会压入到window对象中

  - 代码演示

    ```js
    // 1. 使用const关键字定义常量，常量名一般大写
    const PI = 3.1415926;
    ```

    ```js
    // 2. 常量是不可变的，一旦定义，则不能修改其值
    const PI = 3.1415926；
    PI = 3.14; // 报错，常用一旦被初始化，则不能被修改
    ```

    ```js
    // 3. 初始化常量时，必须给初始值
    const PI; // 报错，Missing initializer in const declaration
    ```

    ```js
    // 4. 具有块级作用域
    // 5. 没有变量提升，必须先定义再使用
    // 6. 常量也是独立的，定义后不会压入到window对象中
    // 这三条和let变量一样，不再写代码
    ```

- 小结

  | 关键字 | 变量提升 | 块级作用域 | 初始值 | 更改值 | 通过window调用 |
  | :----: | :------: | :--------: | :----: | :----: | :------------: |
  |  let   |    ×     |     √      |   -    |  Yes   |       No       |
  | const  |    ×     |     √      |  Yes   |   No   |       No       |
  |  var   |    √     |     ×      |   -    |  Yes   |      Yes       |

### 2.2 解构赋值  

1. 数组的解构 
2. 对象的解构 

ES 6 允许按照一定**==模式==**，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

#### 2.2.1 数组的解构

方便获取数组中的某些项

```js
// 情况1，变量和值一一对应
let arr = [5, 9, 10];
let [a, b, c] = arr;
console.log(a, b, c); // 输出 5 9 10
```

```js
// 情况2，变量多，值少
let arr = [5, 9, 10];
let [a, b, c, d] = arr;
console.log(a, b, c, d); // 输出 5 9 10 undefined
```

```js
// 情况3，变量少，值多
let arr = [5, 9, 10, 8, 3, 2];
let [a, b] = arr;
console.log(a, b); // 5, 9
```

```js
// 情况4，按需取值
let arr = [5, 9, 10, 8, 3, 2];
let [, , a, , b] = arr; // 不需要用变量接收的值，用空位占位
console.log(a, b); // 10, 3 
```

```js
// 情况5，剩余值
let arr = [5, 9, 10, 8, 3, 2];
let [a, b, ...c] = arr; // ...c 接收剩余的其他值，得到的c是一个数组
console.log(a, b, c); 
// 结果：
// a = 5, 
// b = 9, 
// c = [10, 8, 3, 2]
```

```js
// 情况6，复杂的情况，只要符合模式，即可解构
let arr = ['zhangsan', 18, ['175cm', '65kg']];
let [, , [a, b]] = arr;
console.log(a, b); // 175cm 65kg
```

实际应用：

```js
function sum ([a, b, c]) {
    // 形参 = 实参
    // [a, b, c] = [1, 2, 3, 4, 5]
    console.log(a + b + c);
}
sum([3, 4, 5, 6, 7]);  // 3+4+5 = 12
```



#### 2.2.2 对象的解构

- 方便解析对象中的某些属性的值

```js
// 情况1，默认要求变量名和属性名一样
let { foo, bar } = {foo: 'aaa', bar: 'bbb'};
console.log(foo, bar); // aaa, bbb

let {a, c} = {a: 'hello', b: 'world'};
console.log(a, c); // hello, undefined
```

```js
// 情况2，可以通过:为变量改名
let {a, b:c} = {a: 'hello', b: 'world'};
console.log(a, c); // hello, world
```

```js
// 情况3，变量名和属性名一致即可获取到值，不一定要一一对应
let {b} = {a: 'hello', b: 'world'};
console.log(b); // world
// 此时，没有定义变量a，所以使用a会报错
```

```js
// 情况4，剩余值
let obj = {name:'zs', age:20, gender:'男'};
let {name, ...a} = obj;
console.log(name, a);
// 结果：
// name = zs
// a = {age: 20, gender: "男"};
```

```js
// 情况5，复杂的情况，只要符合模式，即可解构
let obj = {
    name: 'zhangsan',
    age: 22,
    dog: {
        name: '毛毛',
        age: 3
    }
};
let {dog: {name, age}} = obj;
console.log(name, age); // 毛毛 3
```

```js
let person = {
            pname: '小明',
            page: 20,
            dog: {
                name: '小黑',
                age: 4,
                child: {
                    name: '小白',
                    age: 1
                }
            }
        }

        let {
            pname, 
            page, 
            dog: {
                name: dname, 
                age: dage, 
                child: {
                    name, age
                }
            }
        } = person;

        console.log(pname, dname, name);
/*
解构的时候，模式和对象的 结构 是一样的
如果变量名冲突，可以使用  原变量: 新变量 的语法处理
*/
```



#### 2.2.3 实际应用

```js
// 假设从服务器上获取的数据如下
let response = {
    data: ['a', 'b', 'c'],
    meta: {
        code: 200,
        msg: '获取数据成功'
    }
}
// 如何获取到 code 和 msg
let { meta: { code, msg } } = response;
console.log(code, msg); // 200, 获取数据成功
```

### 2.3 函数

#### 2.3.1 箭头函数

<!--02.3.1-语法-箭头函数-->

ES6 中允许使用箭头定义函数 (=>  goes to)，目的是**简化函数的定义**并且里面的this也比较特殊。

- 箭头函数的基本定义

  ```js
  // 非箭头函数
  let fn = function (x) {
      return x * 2;
  }
  // 箭头函数，等同于上面的函数
  let fn = (x) => {
      return x * 2;
  }
  ```

- 箭头函数的特点

    - 形参只有一个，可以省略小括号

        ```js
        let fn = (x) => {
            return x * 2;
        }
        // 等同于
        let fn = x => {
            return x * 2;
        }
        ```

    - 函数体只有一句话，可以省略大括号，并且表示返回函数体的内容

        ```js
        let fn = (x, y) => {
            return x + y;
        }
        // 等同于
        let fn = (x, y) => x + y;
        ```

    - 箭头函数内部没有 arguments

        ```js
        let fn = () => {
            console.log(arguments); // 报错，arguments is not defined
        };
        fn(1, 2);
        ```

    - 箭头函数内部的 `this` 指向外部作用域中的 `this` ，或者可以认为箭头函数没有自己的 `this`

      MDN解释：箭头函数不会创建自己的`this`,它只会从自己的作用域链的上一层继承`this`
    
      ```js
      var name = 'lisi'; // 测试时，这里必须用var，因为用let声明的变量不能使用window调用
      let obj = {
          name: 'zhangsan',
          fn : () => {
              console.log(this); // window对象
              console.log(this.name); // lisi
          }
      };
  obj.fn();
    ```

    - 箭头函数不能作为构造函数
    
        ```js
        let Person = () => {
        	
        };
        let obj = new Person(); // 报错，Person is not a constructor
        // 换个角度理解，箭头函数中都没有自己的this，怎么处理成员，所以不能当构造函数
        ```

#### 2.3.2 参数的默认值

ES6 之前函数不能设置参数的默认值

```js
// ES5 中给参数设置默认值的变通做法
function fn(x, y) {
    y = y || 'world';
    console.log(x, y);
}
fn(1)
// ES6 中给函数设置默认值
function fn(x, y = 'world') {
    console.log(x, y);
}
fn(2)
fn(2,3)
```

#### 2.3.3 rest 参数

rest 参数：剩余参数，以 … 修饰最后一个参数，把多余的参数都放到一个**数组**中。可以替代 arguments 的使用

```js
// 参数很多，不确定多少个，可以使用剩余参数
function fn(...values) {
    console.log(values); // [6, 1, 100, 9, 10]
}
// 调用
fn(6, 1, 100, 9, 10);
```

```js
function fn(a, b, ...values) {
    console.log(a); // 6
    console.log(b); // 1
    console.log(values); // [100, 9, 10]
}
// 调用
console.log(fn(6, 1, 100, 9, 10));
```

> **注意：rest 参数只能是最后一个参数**

## 3. 内置对象的扩展

1. Array 的扩展
2. String 的扩展
3. Number 的扩展
4. Set

### 3.1 Array 的扩展

<!--03.1-语法-Array扩展-->

- 扩展运算符

  - 可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造字面量对象时, 将对象表达式按key-value的方式展开

  ```js
  // 合并两个数组
  let arr1 = [1, 2];
  let arr2 = [3, 4];
  let arr3 = [...arr1, ...arr2];
  console.log(arr3); // [1, 2, 3, 4]
  
  // 把数组展开作为参数，可以替代 apply
  // 求数组的最大值
  let arr = [6, 99, 10, 1];
  let max = Math.max(...arr); // 等同于 Math.max(6, 99, 10, 1);
  ```

- Array.from()

  - 把伪数组转换成数组
  - 伪数组必须有length属性，没有length将得到一个空数组
  - 转换后的数组长度，是根据伪数组的length决定的

  ```js
  let fakeArr = {
    0: 'a',
    1: 'b',
    2: 'c',
    length: 3
  };
  
  let arr = Array.from(fakeArr);
  console.log(arr); // ['a', 'b', 'c']
  
  // 转数组的对象必须有length值，因为得到的数组的成员个数是length指定的个数
  // 上例中，如果length为2，则得到的数组为 ['a', 'b']
  ```

- forEach遍历数组

  - 要为forEach传递一个函数进来

  - 为forEach传递的函数有三个形参，分别表示数组的值、下标、当前的数组

      ```js
      // [xxx,xxx].forEach(function (value, index, arr) {
          // value 表示数组的值
          // index 表示数组的下标、索引
          // arr 表示当前的数组
      // });
      
      [3, 8, 4, 9].forEach(function (v, i, a) {
          console.log(v); // 表示数组的值 ，输出的结果是 3,8,4,9
          // console.log(i); // 表示数组的下标
          // console.log(a); // 表示数组
      });
      
      // 如果不需要下标和当前的数组，只使用value即可
      // 函数可以使用箭头函数
      [3, 8, 4, 9].forEach((item) => {
          console.log(item);
      });
      
      // 下面的意思是循环，在循环数组的时候，输出数组的每个值
      [3, 8, 4, 9].forEach(item => console.log(item));
      ```

      

- 数组实例的 find() 和 findIndex()  类似语法的方法还有：forEach 、some、every、filter、map、reduce

  - find和findIndex方法，会遍历传递进来的数组
  - 回调函数有三个参数，分别表示数组的值、索引及整个数组

  - 回调函数中return的是一个条件，find和findIndex方法的返回值就是满足这个条件的第一个元素或索引

  - **find** 找到数组中第一个满足条件的成员并**返回该成员**，如果找不到返回**undefined**。

  - **findIndex** 找到数组中第一个满足条件的成员并**返回该成员的索引**，如果找不到返回 **-1**。

  ```js
  // 语法结构
  let arr = [1, 2, 4, 0, -4, 3, -2, 9];
  arr.find(function (item, index, self) {
      console.log(item); // 数组中的每个值
      console.log(index); // 数组中的每个索引/下标
      console.log(self); // 当前的数组
  });
  ```

  ```js
  // 用法：找数组中第一个小于0的数字
  let arr = [1, 2, 4, 0, -4, 3, -2, 9];
  let result = arr.find(function (item) {
      return item < 0; //遍历过程中，根据这个条件去查找
  });
  console.log(result); // -4
  ```

  > findIndex 的使用和 find 类似，只不过它查找的不是值，而是下标

- 数组实例的 includes()

  - 判断数组是否包含某个值，返回 true / false
  - 参数1，必须，表示查找的内容
  - 参数2，可选，表示开始查找的位置，0表示开头的位置

  ```js
  let arr = [1, 4, 3, 9];
  console.log(arr.includes(4)); // true
  console.log(arr.includes(4, 2)); // false， 从2的位置开始查，所以没有找到4
  console.log(arr.includes(5)); // false
  ```

### 3.2 String的扩展

<!--03.2-语法-String扩展-->

- 模板字符串

  - 模板字符串解决了字符串拼接不便的问题

  - 模板字符串使用反引号 **`** 括起来内容
  - 模板字符串中的内容可以换行
  - 变量在模板字符串中使用 `${name}` 来表示，不用加 + 符号

  ```js
  let name = 'zs';
  let age = 18;
  // 拼接多个变量，在模板字符串中使用占位的方式，更易懂
  let str = `我是${name}，今年${age}`;
  
  
  ```

  ```js
  // 内容过多可以直接换行
  let obj = {name: 'zhangsan', age: 20};
  let arr = ['175cm', '60kg'];
  let html = `
  	<div>
  		<ul>
  			<li>${obj.name}</li>
  			<li>${obj.age + 2}</li>
  			<li>${arr[0]}</li>
  			<li>${arr[1]}</li>
  		</ul>
  	</div>
  `;
  ```

  

- includes(), startsWith(), endsWith()

  - `includes(str, [position])`		返回布尔值，表示是否找到了参数字符串
  - `startsWidth(str, [position])`         返回布尔值，表示参数字符串是否在原字符串的头部或指定位置
  - `endsWith(str, [length])`            返回布尔值，表示参数字符串是否在原字符串的尾部或指定位置。

  ```js
  console.log('hello world'.includes('e', 2)); // false 从位置2开始查找e，没有找到
  console.log('hello world'.includes('e')); // true
  
  console.log('hello world'.startsWith('h')); // 未指定位置，看开头是否是h，返回true
  console.log('hello world'.startsWith('l', 2)); // 指定位置的字符是l，返回true
  
  console.log('hello world'.endsWith('d')); // 未指定位置，结尾是d，返回true
  console.log('hello world'.endsWith('r', 9)); // 先截取9个字符，然后看这9个字符串的结尾是不是r。返回true
  ```

- repeat()

  `repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

  ```js
  let html = '<li>itheima</li>';
  html = html.repeat(10);
  ```

- trim()

    `trim()` 方法可以去掉字符串两边的空白

    ```js
    console.log('    hello        '.trim()); // hello
    console.log('    hello        '); //
    ```

    

### 3.3 Number的扩展

ES6 将全局方法`parseInt()`和`parseFloat()`，移植到`Number`对象上面，功能完全保持不变。

- Number.parseInt()

- Number.parseFloat()

    ```js
    console.log(parseInt('123abc'));
    // ES6中，将parseInt移植到了Number对象上
    console.log(Number.parseInt('123abc'));
    ```

    

### 3.4 Set

<!--03.4-语法-新增Set对象-->

ES6 提供了新的数据结构 Set。它类似于数组，但是==成员的值都是唯一的==，没有重复的值。

`Set`本身是一个构造函数，用来生成 Set 数据结构。

Set的特点就是该对象里面的成员不会有重复。

```js
// 1. 基本使用
let s = new Set();
// 得到一个空的Set对象
// 调用add方法，向s中添加几个值
s.add(3);
s.add(7);
s.add(9);
s.add(7); // Set对象中的成员都是唯一的，前面添加过7了，所以这里添加无效

console.log(s.size);
console.log(s); // {3, 7, 9}
```

- Set 的成员
  - `size`：属性，获取 `set` 中成员的个数，相当于数组中的 `length`
  - `add(value)`：添加某个值，返回 Set 结构本身。
  - `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
  - `has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
  - `clear()`：清除所有成员，没有返回值。

```js
// 将一些重复的值加入到Set对象中，看看效果
const s = new Set();
// 使用forEach遍历前面的数组，然后将数组中的每个值都通过Set对象的add方法添加到Set对象中
[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));
// s = {2, 3, 5, 4}
// 遍历Set对象，发现重复的值只有一份
// for...in  循环中的 i 表示数组的下标，或对象的属性名
// for...of  循环中的 i 表示数组的值，或对象的值
for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

另外初始化Set的时候，也可以为其传入数组或字符串，得到的Set对象中的成员不会有重复。

根据这个特点可以完成数组或字符串去重。

```js
// Set 可以通过一个数组初始化
let set = new Set([1, 2, 1, 5, 1, 6]);
console.log(set); //Set(4) {1, 2, 5, 6}
// 数组去重
let arr = [...set]; // 方式一
console.log(Array.from(set)); // from是将伪数组变为数组;方式二
console.log(arr); // [1, 2, 5, 6]

// 完成字符串去重
let str = [...new Set('ababbc')].join('');
console.log(str); // abc
```



## 4. 定义对象的简洁方式

<!--04-语法-简洁的定义对象的方式-->

```js
let id = 1;
let name = 'zs';
let age = 20;

// 之前定义对象的方案
// let obj = {
//     // 属性: 值
//     id: id,
//     name: name,
//     age: age,
//     fn: function () {
//         console.log(this.age);
//     }
// };

// obj.fn();


// ES6的新方案
let obj = {
    id,  // 属性名id和前面的变量id名字相同，则可以省略 :id
    name,
    nianling: age,
    // 下面的函数是上面函数的简化写法，可以省略 :function  。但是注意这里仅仅是上面函数的简化，不是箭头函数
    fn () {
        console.log(this.name);
    }
};
obj.fn();
```

## 5. ECMAScript 6 降级处理 (保留)

### 5.1 ES 6 的兼容性问题 ###

- ES6 虽好，但是有兼容性问题，IE7-IE11 基本不支持 ES6

  [ES6 兼容性列表](http://kangax.github.io/compat-table/es6/)

- 在最新的现代浏览器、移动端、Node.js 中都支持 ES6

- 后续我们会讲解如何处理 ES6 的兼容性

### 5.2 ES 6 降级处理 ###

因为 ES 6 有浏览器兼容性问题，可以使用一些工具进行降级处理，例如：**babel**

- 降级处理 babel 的使用步骤

   1. 安装 Node.js

   2. 命令行中安装 babel

   3. 配置文件 `.babelrc`

   4. 运行


- 安装 Node.js

     [官网](https://nodejs.org/en/)

- 项目初始化(项目文件夹不能有中文)

     ```bash
     npm init -y
     ```
- 在命令行中，安装 babel [babel官网](https://babeljs.io)

   ```bash
   npm install  @babel/core @babel/cli @babel/preset-env
   ```

- 配置文件 `.babelrc` (手工创建这个文件)

  babel 的降级处理配置

  ```json
  {
    "presets": ["@babel/preset-env"]
  }
  ```

- 在命令行中，运行

  ```bash
  # 把转换的结果输出到指定的文件
  npx babel index.js -o test.js
  # 把转换的结果输出到指定的目录
  npx babel 包含有js的原目录 -d 转换后的新目录
  ```

**参考：**[babel官网](https://www.babeljs.cn/)

## 6. 扩展阅读

[ES 6 扩展阅读](http://es6.ruanyifeng.com/)