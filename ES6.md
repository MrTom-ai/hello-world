#ES6

##Symbol
 ###Symbol的定义
- `Symbol`新增数据类型，表示**独一无二的值**
- `Symbol`**的值通过Symbol函数生成。**
- `Symbol`函数前不能使用new命令，否则会报错。因为生成的Symbol是一个原始数据类型的值，不是对象。也就是说，由于 Symbol 值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。
```js
let s = Symbol()
```
 ###Symbol()参数
- 字符串： Symbol函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分
```js
let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```
- 对象：参数是一个对象，就会调用该对象的toString方法，将其转为字符串，然后才生成一个 Symbol 值。
```js
const obj = {
    toString() {
        return 'abc';
    }
};
const sym = Symbol(obj);
sym // Symbol(abc)
```
>注意，Symbol()函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的Symbol函数的返回值是不相等的。

 ###Symbol运算
  >Symbol 值不能与其他类型的值进行运算，会报错。
```js
let sym = Symbol('My symbol');

"your symbol is " + sym
// TypeError: can't convert symbol to string
`your symbol is ${sym}`
// TypeError: can't convert symbol to string
```
 ###Symbol类型转换
 - Symbol 值可以显式转为字符串。
```js
 let sym = Symbol('My symbol');

String(sym) // 'Symbol(My symbol)'
sym.toString() // 'Symbol(My symbol)'
```
###Symbol操作

- 在创建 Symbol 的时候，参数是为 Symbol 数据的描述。
  - `Symbol.prototype.description`返回 Symbol 的描述。
- 作为属性名的 Symbol
```js
let mySymbol = Symbol();

// 第一种写法
let a = {};
a[mySymbol] = 'Hello!';

// 第二种写法
let a = {
[mySymbol]: 'Hello!'
};

// 第三种写法
let a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

// 以上写法都得到同样结果
a[mySymbol] // "Hello!"
```
>Symbol 值作为对象属性名时，不能用点运算符。

  - Symbol 作为属性名，遍历对象的时候，该属性不会出现在for...in、for...of循环中，也不会被Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回。 但是，它也不是私有属性，有一个Object.getOwnPropertySymbols()方法，可以获取指定对象的所有 Symbol 属性名。该方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。
```js
const obj = {};
let a = Symbol('a');
let b = Symbol('b');

obj[a] = 'Hello';
obj[b] = 'World';

const objectSymbols = Object.getOwnPropertySymbols(obj);

objectSymbols
// [Symbol(a), Symbol(b)]
```
##解构

Es6允许按照一定模式，从**数组和对象**中提取值，对变量进行赋值，这被称为解构
```js
/****数组解构****/ 
let [a, b, c] = [1, 2, 3];
a // 1
b // 2
c // 3
let [, , third] = ["foo", "bar", "baz"];
third // "baz"
//  如果解构不成功，变量的值就等于undefined。
let [foo] = [];
let [bar, too] = [1];
foo //undefined
too //undefined

/****对象解构****/ 
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"
```

###解构默认值
```js
// 对象默认值
let { x = 3 } = {};
x // 3
let { x, y = 5 } = { x: 1 };
x // 1
y // 5
// 数组默认值
let [foo = true] = [];
foo // true
let [x, y = 'b'] = ['a']; // x='a', y='b'
```
##let/const
###let
关键字，用来声明变量。它的用法类似于var，但是所声明的变量，只在let关键字所在的代码块内有效。
 ####不存在变量提升
 事由：var命令会发生“变量提升”现象，即变量可以在声明之前使用，值为  undefined。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声 明语句之后才可以使用。

 解决方法：为了纠正这种现象，let命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。**var 声明的变量挂载在 window 对象下，而 let则没有。 let 不允许重复声明。**

###作用域
ES5 只有全局作用域和函数作用域，没有块级作用域，使用 let 关键字可以支持块级作用域。

###const
const声明一个*只读的常量*。一旦声明，常量的值就*不能改变*。

##模板字符串
模板字符串（template string）是增强版的字符串，用反引号（\`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。
```js
// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```
##rest参数

 ###rest参数定义
ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。
```js
function add(...values) {
  let sum = 0;
  for (var val of values) {
    sum += val;
  }
  return sum;
}
add(2, 5, 3) // 10
```

 ###...在数组中的作用
... 在数组中时作为展开运算符使用。

##箭头函数
 ###定义箭头函数
ES6 允许使用“箭头”（=>）定义函数。
 ###省略格式的几种方法
- 箭头函数只有一个参数时　圆括号可以省略
```js
	let f = v =>{return v}
```
- 箭头函数，函数体中只有一条有效语句时，花括号可以省略。
```js
	let f = v => console.log(v)
```
- 箭头函数，省略花括号时如果要返回数据给调用者时不可以使用 return 关键字。
```js
	let f = ()=> 1//返回值格调用者
```
>1.函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
>2.不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
>3.不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

##函数默认值
 ###函数默认值的用法
ES6 允许为函数的参数指定默认值。
```js
function foo(num=20){
    num//
}
foo()
let f3 = (num=33){
    return num//33
}
f3()
```
当调用函数时没有给函数传递实际参数时就会使用参数的默认值。
##Set
 ###Set 的定义
 ES6 提供了新的数据结构 Set。它**类似于数组**，但是成员的值都是唯一的，没有重复的值。可以用来对数组*去重*。
 ```js
 let set = new Set()
 ```
###Set的属性和方法

- `set.size`: 返回Set实例的成员总数。
- `set.add(value)`: 添加某个值，返回 Set 结构本身。（重点）
- `set.delete(value)`: 删除某个值，返回一个布尔值，表示删除是否成功。（重点）
- `set.has(value)`: 返回一个布尔值，表示该值是否为Set的成员。
- `set.clear()`: 清除所有成员，没有返回值。
- `set.keys()`: 返回键名的遍历器
- `set.values()`: 返回键值的遍历器
- `set.entries()`: 返回键值对的遍历器
- `set.forEach()`: 使用回调函数遍历每个成员

```js
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]
```

> Set 也可以使用展开运算符 `... new Set([1,3,4,6])` 

## Map

 ### Map的定义

ES6 提供了 Map 数据结构。它**类似于对象**，也是**键值对的集合**，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。 

```js
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

###Map的属性和方法

- `map.size`: 属性返回 Map 结构的成员总数。
- `map.set(key, value)`: set方法设置键名key对应的键值为value，然后返回整个 Map 结构。
- `map.get(key)`: get方法读取key对应的键值，如果找不到key，返回undefined。
- `map.has(key)`: has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。
- `map.delete(key)`: delete方法删除某个键，返回true。如果删除失败，返回false。
- `map.clear()`: clear方法清除所有成员，没有返回值。
- `map.keys()`: 返回键名的遍历器。
- `map.values()`: 返回键值的遍历器。
- `map.entries()`: 返回所有成员的遍历器。
- `map.forEach()`: 遍历 Map 的所有成员。

```js
const map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);

for (let key of map.keys()) {
  console.log(key);
}
// "F"
// "T"

for (let value of map.values()) {
  console.log(value);
}
// "no"
// "yes"

for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
// "F" "no"
// "T" "yes"

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"

// 等同于使用map.entries()
for (let [key, value] of map) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"

map.forEach((val,index,map)=>{
    console.log(val,index,map)
})
// no F Map(2) {"F" => "no", "T" => "yes"}
//yes T Map(2) {"F" => "no", "T" => "yes"}
```

## class

### class用法

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。

新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

```js
class Human {
    constructor(name, age, sex) {
        this.name = name
        this.age = age
        this.sex = sex
    }
    toString() {
        console.log(this.name + " : " + this.age + " : " + this.sex)
    }
}

let h1 = new Human('xiaoMing', 19, 'man')
```

- ` class` 关键字表示定义一个类。
- `constructor`构造函数， 在实例化时第一个被调用的函数，成员要在 `constructor` 构造中定义。一个类只能有一个构造函数，如果没有定义则会自动生成一个空的 `constructor`。 
-  `toString` 成员方法。成员方法前面不能添加 function 并且成员之间不能使用 ， 逗号分隔。 

### static 静态成员

- 静态方法：类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接**通过类**来调用，这就称为“静态方法”。

```js
class Human {
    constructor(name, age, sex) {
        this.name = name
        this.age = age
        this.sex = sex
    }
    // 对象成员
    toString() {
        console.log(this.name + " : " + this.age + " : " + this.sex)
    }
    // 静态方法，不属于对象
    static say(){
        console.log('静态方法')
    }
}
// 调用静态方法
Human.say()
```

> 父类的静态方法，可以被子类继承。Class 内部只有静态方法，没有静态属性。

###  私有方法和私有属性

私有方法和私有属性，是只能在类的内部访问的方法和属性，外部不能访问。ES6 不提供私有方法和私有属性。 

### extends

class 可以通过extend关键字实现继承，这比ES5的通过修改原型链实现继承，要清晰方便很多。

```js
// 父类
class Human {
    constructor(name, age, sex) {
        this.name = name
        this.age = age
        this.sex = sex
    }
    // 对象成员
    toString() {
        console.log(this.name + " : " + this.age + " : " + this.sex)
    }
    // 静态方法，不属于对象
    static say(){
        console.log('静态方法')
    }
}
// 继承Human类
class Man extends Human{
    constructor(name,age,job){
        // 调用父类的构造方法
        super(name,age,'man')
        this.job = job
    }
}
```

- `super` 表示父类对象。
- `super()` 表示父类构造方法。
- 子类中如果显示包含 `constructor` 那么**必须在`constructor`最上方调用 `super()`父类构造方法**。实例化子类时会先实例化父类。

## Promise对象

### Promise定义

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。ES6 将其写进了语言标准，统一了用法，原生提供了Promise对象。

Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。

### Promise对象三种状态

1. **pending（进行中）**
2. **fulfilled（已成功）**
3. **rejected（已失败）**

> 只有异步操作的结果，可以决定当前是哪一种状态，状态一旦确认，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。 

### Promise 对象创建

```js
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value); //触发成功状态
  } else {
    reject(error); //触发失败状态
  }
});
//监听状态发生变化
promise.then(function(value) {
  // success 成功
}, function(error) {
  // failure 失败
});
```

实例化 Promise 对象时参数为一个回调函数，该回调函数有两个参数分别是 **resolve**（成功状态）和**reject**（失败状态）。 

 - `resolve(value)`   函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去； 

 - `reject(value)`   函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。


#### then

`promise.then() `   Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。

- 参数1：成功状态触发该的回调函数 。
- 参数2：状态为失败触发的回调函数 。

> then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。 

```js
//监听状态发生变化
promise
    .then(function (value) {
        // success 成功
        return 'success'
    }, function (error) {
        // failure 失败
        return 'error'
    })
    // 接收上一个then()的数据
    .then(function(value){
        console.log( value )
        return 'hello'
    })
```

#### catch

- Promise.prototype.catch方法是`.then(null, rejection)`或 `.then(undefined, rejection)` 的别名，用于指定发生错误时的回调函数。
- 使用**catch**方法就可以不再指定**then**中第二个参数，这样代码会更加易读

```js
promise
    .then(function (value) {
        console.log( value )
    })//接收上一个promise成功执行的返回值
    .catch(function(err){
        console.log( err )
    })//接收上一个promise执行失败的返回值
```

### Module

#### module的定义

模块（module）体系，是将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。

- `<script>` 标签中要使用模块功能需要设置 `type="module"` 

#### module示例：

	- `m1.js`

```js
//导出模块中数据
export default { name: "小明" };
```

- `main.js`

```js
//导入模块中数据
import obj from './m1.js';
console.log(obj)
```

-`index.html`

```html
<!-- 加载一个外部文件作为模块 -->
<script type="module" src="./main.js"></script>

<!-- 在内嵌块中加载模块 -->
<script type="module">
    import obj from './m1.js';
    console.log(obj)
</script>
```