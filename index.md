# JavaScript for Python

> Author: *_Kerman*

## 前言

这本书，试图通过介绍 JavaScript，以及它与 Python 之间的关联和异同，来阐释一些**单从 Python 角度不易说明**的东西，以期加深读者对于 Python 的理解，尤其是，解决一些**Python 为什么这样做**的问题。

本书适合**无 JavaScript 基础**，**有一定 Python 基础(必修部分)**的**高中技术选考生**，因此本书的写作也将尽可能符合高考 Python 的需要，略去了一些 JavaScript 中关系不大的内容，希望能对你有所帮助~

> TypeScript 作为 JavaScript 的超集(superset)，也在本书的讨论范围之内。


## outline

- 简介
- 范式
- 索引/成员
- 类/原型链
- 类型（包括类型转换）
- 引用/值
- 函数式
- 命名/Symbol/Dunder methods
- 解包
- 模块
- 异常
- async/await
- 迭代器/生成器
- 数据结构
- 重载/重写
- 符号/语言内部协议
- 其他，站在 js 角度对 Python 的看法

ducktype

## 简介

### 何为JavaScript？

JavaScript，简称 **JS**，其正式名称是 ECMAScript，在 web 开发中处于不可代替的地位，随着[Electron.js]()、[taori]()和[Node.js]()、[deno]()的出现，也在本机应用、服务器等方面占据了一席之地。

> 现在的 JavaScript，已经和 10 年前的 JavaScript 完全不同了，现在的 JavaScript 已经一门足够现代、充满生机的语言。如果你在网上看到蹩脚的 JavaScript 代码，很大可能，它是从坟墓里爬出来的。

> JavaScript 和 Java(无论是那门语言，那个岛，或者某种咖啡)都没有任何关系。当年取名 JavaScript，只是一种营销策略。%TODO: link%

### TypeScript, JavaScript的超集

TypeScript，简称 **TS**，由微软主持开发，作者是 Anders Hejlsberg(他同时也是Delphi和C#的作者)。

Typescript 在 JavaScript 的基础上，提供了类型的支持（类似 Python 中的类型注解）。TypeScript不能直接执行，而是会被编译到 JavaScript 然后像普通的JavaScript那样执行。

### JavaScript与Python的相似性

1. 高度动态性
2. 自动的内存管理
3. 范式上相似（见下章）
4. 都是解释型语言%?%

## 范式

世界上的编程语言，分为两大阵营%找一段专业的解释%

（函数式和命令式，各种语言的那张图）

由此可见，JavaScript 与 Python 都是

## JavaScript 入门

### 配置开发环境

#### 安装 `Node.js`

#### 安装 `VSCode`

推荐使用 VSCode 作为 IDE(集成开发环境)。

#### Hello world

```javascript
console.log("Hello world!");
```

恭喜你成为来一名JavaScript程序员，同时，你也成为了一名TypeScript程序员——这段代码同时也是良好的TypeScript代码。

或许你会觉得这段代码又熟悉又陌生。引号包裹的字符串、使用小括号进行函数调用，这些都与Python一模一样。

`console.log`比`print`要长一倍。这里浅浅解释一下它的含义。相信你在阅读完本书后，会对这段代码的每一个字都有更深刻的理解。

- `console`的中文是**控制台**。不同环境的下的控制台并不相同，在浏览器中它藏在开发工具里，在Node.js环境中，它就是你眼前这个黑色背景的窗口。
- `log`的中文是**日志**，它有个别名叫`info`，表示输出一些信息。
- 所以，`console.log`就是**控制台对象的日志函数**。

### 语法概览

JavaScript 的语法总体上和C/C++非常相近，与Python也有很多相似之处，但是有这几个显著的不同：

- 使用大括号包裹语句块，而不是通过缩进。
- 语句末尾有分号（多数情况下可以省略不写，但推荐全部写上）。

### 字面量与基本类型概览

就像抽象的代数运算中，除了字母往往也有普通的数字，代码中往往也有普通的数据。这些数据就是**字面量**。

1. 数值(`number`)

  在Python中数值分为`int`、`float`等，而JavaScript中的`number`表示是**实数**，包括整数和小数，比如`1`、`3.14`。

  有趣的是，JavaScript中的数值类型，还可以取`Infinity`、`-Infinity`、`NaN`这三个特殊的值。

  - `Infinity`表示无限大，`-Infinity`表示无限小。

    比如，要找出数列中最大的数时，我们就可以把存储最大值的变量的初始化为`-Infinity`。

  - `NaN`是Not a Number的缩写，表示它不是一个合法的数字。

    把`0`作为除数，在数学上是不被允许的。这样的行为，在Python中，会抛出`ZeroDivisionError`，而在JavaScript中，则有如下表现：

    ```javascript
    1/0   //--> Infinity
    1/-0  //--> -Infinity，是不是很离谱？
    0/0   //--> NaN
    100+Infinity //--> Infinity
    Infinity-Infinity //--> NaN
    NaN+1 //--> NaN
    0===+0 //--> true
    +0===-0 //--> true
    ```

    其实，这样的结果，是符合数学上的关于极限的计算的。`+0`(就是`0`)，相当于数学中的`x, lim x→+0`，`-0`就相当于`x, x→-0`。当只有有限大的数值时，它们之间的差(通俗地说)因为太小，被忽略了；而当涉及到无限大时，它们的区别就显现出来了。
  
2. 字符串(`string`)

  与Python中一样，JavaScript中**没有字符类型，只有字符串类型**。

  以下代码包含通过三种不同引号创建的字符串字面量：

  ```javascript
  "Hello"
  'Hi'
  `Nice`
  ```
  
  前两种引号，与Python中是一样的，它们只能容纳
  
  第三种引号叫做“抑音符”，或者叫“反引号”，一般来说在键盘的左上角。通过这种引号构造的字符串字面量，叫做**模板字符串**，有这两个特别的功能：
  
  1. 就像Python中的三引号(`""" """`或`''' '''`)字符串，<code>` `</code>可以容纳中间的任何文本，包括换行和空格。

  2. 可以使用字符串插值：

    ```javascript
    const s="Hi", x=3;
    console.log(`s is ${s}, x is ${x}`);
    // 输出：s is Hi, x is 3
    ```
  
  <!-- 模板字符串传递给函数的写法，就不讲了？ -->

  编写字符串字面量时，还需考虑**字符串转义**的问题：

  与Python一样，一些特殊的字符如果要放在字符串字面量中，需要经过转义。下表是一些常见的转义字符，既适用于Python，也适用于JavaScript：

  | 字符名称 | 转义字符串 |
  | ------ | -------- |
  | 换行符  | `"\n"`(**n**ext line) |
  | 制表符  | `"\t"`(**t**ab) |
  | 引号    | `\'`和`\"`，JS中还有<code>\\`</code> |
  | 反斜杠  | `\\`     |

  > 在一种引号中使用另外一种引号不需要转义：`"say 'hello'"`和`'say "hi"'`都是合法的字符串字面量。

3. 数组(`Array`)

  JavaScript的数组就像Python中的列表，其元素个数可变、类型不要求相同，索引(下标)也是以0为起始。

  ```javascript
  const arr=[1,2,3];
  arr[1] //--> 2
  ```

  要获取一个数组的元素个数，在Python中可以使用`len()`函数。在JavaScipt中，我们使用数组的`length`属性：

  ```javascript
  const arr=["a","b","c"];
  arr.length //--> 3
  ```

### 变量

在 Python 中，变量无须声明，直接赋值即可：

```python
a = 1
print(a)  #--> 1
```

而在 JavaScript 中，变量必须先声明，才可被赋值使用：

```javascript
let a = 1;
let c; //声明但不赋值, c目前是undefined
b = 2; //抛出异常：TypeError: b is used before defined.
a = 3; //重新赋值，现在a是3
```

> **TypeScript**
>
> 在 ts 中，可以用如下方式指定变量类型：
>
> ```typescript
> let a: number; //指定a是整数类型的变量
> ```
>
> 大部分情况下，变量的类型可以被自动推断出来，不需要手动指定：
>
> ```typescript
> let a = 1;
> //  ^number
> ```

### 运算

`+`、`-`、`*`、`%`、`<=`等数值运算符，相信你在小学二年级就已经学习过了。

相信你一定有过在 Python 判断语句中，把`==`错写成`=`的经历，幸好是在 Python，这被设计成了一个语法错误，可以及时被发现，不然恐怕得调试好半天呢。

> 在Python中，若真的需要在判断语句中赋值，请使用`:=`。

在 JavaScript 中，也有`==`，但是推荐使用`===`进行相等性判断，以避免隐式转换带来的麻烦。同理，推荐使用`!==`而不是`!=`。

> `===`相比`==`，是否更难和`=`弄混了呢？

需要注意的是，JavaScript 和 Python 的逻辑运算符写法并不相同，但与 C/C++是差不多的。下面是一张对照表：

| Python    | JavaScript            |
| --------- | --------------------- |
| `not x`   | `!x`                  |
| `x and y` | `x && y`              |
| `x or y`  | <code>x \|\| y</code> |

无论是 Python 还是 JavaScript，逻辑与 和 逻辑或 运算都是**短路**的。请看下例：

```javascript
function T(){
  console.log("T");
  return true;
}
function F(){
  console.log("F");
  retuan false;
}

let a=T()&&F(); //-->false，输出：TF
let b=F()&&T(); //-->false，输出：F
let c=T()||F(); //-->true ，输出：T
let d=F()||T(); //-->true ，输出：FT
```

显然，逻辑与 和 逻辑或 运算，从结果上看，是满足交换率的；但是由于“短路”的特性，交换顺序之后运行结果并不相同。

短路就是指，一旦计算的结果已经确定，就没有必要去计算接下去的部分了。比如上例在计算`b`时，因为`F()`已经返回`false`，无论`T()`返回`true`还是`false`，逻辑与运算的结果都一定是`false`，因此就无需执行`T()`了。

逻辑运算符短路的特性，在编写代码时，一方面可以拿它作为优化运行速度的工具，一方面也要防止落入“一定会被执行”的陷阱之中。

### 逻辑控制

作为偏向命令式的语言，逻辑控制是必不可少的部分。

在 Python 中，有`if`、`for`、`while`、`match`、`return`等关键字用于逻辑控制，在 JavaScript 中也是大同小异。

#### 判断：`if`-`else`

先上例子：

```javascript
const a = 15;
if (a % 2 === 0) {
  console.log("a是偶数");
} else {
  console.log("a是奇数");
}
```

- `if`后面有一组**小括号**包裹条件表达式
- 语句块由一组**大括号**包裹

##### 连续的多个`if`-`else`

在 Python 中，通过`elif`进行多选一的判断。

在 JavaScript 中，则是这样做的：

```javascript
if (a % 3 === 0) {
  //...
} else if (a % 3 === 1) {
  //...
} else {
  //...
}
```

##### 为什么 Python 需要`elif`？

关键字是一种稀缺的资源。语言的创造者不会创造一个没用的关键字。Python 中的`elif`，明明就是`else if`的简写，少写 3 个字母的好处显然不构成它存在的充分理由。

###### `else if`的实质

在 JavaScript 中，`else if`（就像 C/C++那样），其实是`else`后面省略了包裹下一个`if`的花括号。因为下一个`if`对于上一个`else`而言，其实就是一条语句，就像大括号把一系列语句*包裹*成了一个语句

上面的代码其实等价于如下代码：

```javascript
if (a % 3 === 0) {
  //...
} else {
  if (a % 3 === 1) {
    //...
  } else {
    //...
  }
}
```

> 也可以这样理解：
>
> 在 JavaScript 中，无论`if`、`else`还是`for`，都默认作用在紧接着的**第一个**语句上，就像这样：
>
> ```javascript
> if (cond1) console.log("print if cond1 is true");
> console.log("always print");
> ```
>
> > 注意：这里的缩进并没有语法上的任何作用！只是出于美观的考虑。
>
> 而**大括号的作用，就是把多条语句并作一条语句**。

##### 如果 Python 没有`elif`

在 Python 中，没有大括号去区分代码块，也没有默认包裹下一条语句的规则，只有**缩进是区分代码层级的唯一标准**。假设 Python 没有`elif`，那么我们将只能这么写：

```python
if a%3==0:
  # ...
else:
  if a%3==1:
    # ...
  else:
    # ...
```

随着`if-else`嵌套的增多（在实际开发中，多达 5 个以上的`if-else`并非不存在），Python 代码将横向生长，产生大量的空白，不易读也不美观。

这就是为什么 Python 需要`elif`关键字。

#### 循环：`for`/`while`/`do`-`while`

JavaScript 的`while`、`do`-`while`，和 Python 的`while`并没有什么区别区别：

```javascript
while (cond1) {
  doSomething();
}
```

而 JavaScript 的`for`，更像是 C/C++和 Python 的`for`的组合。

以下代码实现了循环 10 次，与 C/C++的写法几乎没有区别：

```javascript
for (let i = 0; i < 10; i++) {
  doSomething();
}
```

以下代码遍历了一个数组(array, 可以简单理解为 list)，则与 Python 的写法几乎没有区别：

```javascript
const arr = [1, 2, 3];
for (const x of arr) {
  console.log(x);
}
```

需要强调的是，JavaScript 中，使用`for`-`of`而不是`for`-`in`来遍历一个数组。`for`-`in`被赋予了另外的含义。参见《迭代器》。

#### 函数

函数的作用，主要有这两点：

- 复用代码：避免重复写同一段代码，提高效率的同时，便于维护
- 拆分步骤：避免出现一段非常长连续代码，增强可读性
- 作为过程：可以传递给高阶函数，也可以进行更加复杂的流程控制

在 JavaScript 中，使用`function`关键字定义函数，就像 Python 中的`def`关键字：

```javascript
function fn(x, y, z = 0) {
  return x + y * z;
}
```

其中，`z = 0`表示一个有默认值的参数，可以有多个，但只能放在最后，与在 Python 中是一样的。

值得注意的是，有默认值的参数只能放在最后的缺点，恰是 Python 关键字参数的优点之一。

Python 的参数分为 3 类：

1. 只可作为位置参数
2. 既可作为位置参数，也可作为关键字参数
3. 只可作为关键字参数

一般情况，下我们定义的参数默认属于第 2 类。如何定义其他两类参数，以及一些相关细节，并不是重要的内容，所以本书不会展开讨论。可以阅读 Python 的有关文档。

> 如果 Pandas 的所有函数，都只使用关键字参数，那么是会更好记还是更难记？
>
> 好记：
>
> - 无需记忆参数的顺序
>
> 难记：
>
> - 需要记住参数的名称
>
> 其实参数的顺序或名称，都有一定的规律，但是对于不同函数，它们符合规律的情况有差异，我们可以选取其中更好记的一种。
>
> 1. 如果这个参数是必须的，
>
> ```python
>
>
> ```

调用函数：

```javascript
fn(1, 2, 3); //-->7
fn(4, 5); //-->4，等价于 fn(4, 5, 0)
```

> **TypeScript**
>
> 函数的参数，除非有默认值，不然无法自动推断出参数类型。这时，我们需要手动指定它们的类型：
>
> 函数的返回值的类型，也可以手动指定。
>
> ```typescript
> function fn2(s: string, n: number): boolean {
>   return s.length === n;
> }
> ```

函数的参数，既可以是普通的量，也可以是函数，在 JavaScript 和 Python 中，都是如此，并且非常常用。

##### 高阶函数

接受函数作为参数的函数，叫做**高阶函数**(high-order function)，数学上，有个与之类似的概念，叫泛函(functional)

我们来看一段 TypeScript 代码，其中也涉及如何**给作为参数的函数标注类型**：

```typescript
function applyTwice(x: number, fn: (x: number) => number) {
  return fn(fn(x));
}

function add1(x: number) {
  return x + 1;
}
applyTwice(3, add1); //--> 5
```

##### lambda(λ)表达式

lambda(λ)一词来源于 λ 演算，是函数式编程的核心概念。在 Pythony 与 JavaScript 中，都有通过一个表达式创建函数的功能。

下面是一段你一定不陌生的 Python 代码，它常常在题目中以提示出现，实现了按照`"id"`的大小排序的功能：

```python
d=[{ "id":3 },
   { "id":1 },
   { "id":2 }]
sorted(d, key=lambda v:v["id"])
```

这里的`lambda v:v["id"]`就是一个 lambda 表达式。它临时创建了一个函数，

##### 可变长参数

Python 中的`print`，相信你已经使用了无数次了。是否好奇过它是怎么接受不同数目的参数的？

下面是一个类似`print`的函数，它把每个参数组合成字符串返回。

```python
def my_print(n, *args):
  result=""
  for arg in args:
    result+=str(arg)+" "*n
  return result[:-n]

my_print(2, "a", 1)  #--> "a  1"
```

在 JavaScript 中，也可以写出这样的函数。以下这段代码用 TypeScript 呈现，以便展示可变参数打包之后的类型。

```typescript
function myPrint(n: number, ...args: any[]) {
  let result = "";
  for (const arg of args) {
    result += arg + " ".repeat(n);
  }
  return result.slice(0, -n);
}
```

可以看到，在 Python 中用`*`，在 JavaScript 中用`...`，可以表示这个参数是可变长的。

> 另：Python 中`**kwargs`这样的写法，可以表示可变数目的关键字参数。其中`kwargs`的类型将会是一个字典。

无论是 Python 还是 JavaScript，可变长参数都会是一个**列表**/**数组**%这里关于 Python 的部分存疑%

函数的参数，可以看作是一个数组。下面这段 JavaScript 代码，也用到了`...`运算符：

```javascript
let [n, ...args] = [2, "a", 1];
console.log(n); //--> 2
console.log(args); //--> ["a", 1]
```

与可变长参数多么相似！

这样的操作，叫做**解包**(unpack)。在 Python 中也是一样的：

```python
[n, *args] = [2, "a", 1]
# or
n, *args = 2, "a", 1
```

在 JavaScript 中，不但数组可以解包，普通的对象也可以：

> 当然，JavaScript 的数组也是一个对象！

```javascript
const basic = {
  name: "_Kerman",
  status: "sync",
};

const expended = {
  ...basic,
  country: "China",
  status: "async",
};

// expended是：
({
  name: "_Kerman",
  status: "async", //解包获取的值被覆盖了
  country: "China",
});
```

用这种方式，可以实现合并两个对象/数组：

```javascript
const arr = [...arr1, arr2];
const obj = { ...obj1, obj2 };
```

> 注：**解包实际上进行了一次迭代，并将迭代的结果传递下去**，因此，只有可迭代出来的成员可以被解包。以下两类成员不可被迭代，因此不会被解包：
>
> 1. 继承自原型的成员
> 2. 描述符(descriptor)被设置为`enumerable: false`的成员
>
> 这也是为什么，数组作为对象，解包时不会给出诸如`[].push`这样的方法。

## 索引/成员

字符串(`str`)、列表(`list`)与字典(`dict`)是 Python 的基础内容。相信你对于下面这些写法并不陌生：

```python
# 中括号
"ABCDEFG"[2]    #--> "C"
"ABCDEFG"[3:5]  #--> "DE"
[1,2,3,4][-1]   #--> 4
[1,2,3,4][::-1] #--> [4,3,2,1]
{"a": 1}["a"]   #--> 1

# 点号
"abc".upper()   #--> "ABC"
{"a": 1}.keys() #--> ["a"]
```

使用 Pandas 库的时候，用`[ ]`和`.`都可以获得一列的数据：

```python
df = pd.DataFrame(..., columns=["a", "b"])

df["a"]
df.a
```

但是这两种方式是不相同的：

```python
col_name = chr(ord("a") + x%2)
df[col_name]    #--> df["a"] 或 df["b"]
df.col_name     #抛出异常：AttributeError: has no attribute 'col_name'
```

对于一个 Python 中的字典，二者的区别更加明显：

```python
d  #type: dict
d["a"] # 不能写成 d.a
```

究其原因，在 Python 中，`[ ]`作为一种运算符，调用了%?%

在 JavaScript 中，并没有运算符重载这回事，因此`[ ]`和`.`没有实质上的不同。

下面这段 JavaScript 代码，涉及了**对象的创建**与**通过索引获取成员**：

> JavaScript 中的对象(object)，既起到了 Python 中字典的功能，也是所有数据结构的基础模型。

```javascript
const k = "c";
let obj = {
  a: 1,
  "b": 2,  //等价于 ["b"]: 2
  [k]: 3,  //等价于 ["c"]: 3
  "+": 4,
};

obj.a;    //-->1
obj["a"]; //--> 1

obj.b === obj["b"];

obj.k;    //--> undefined
obj[k];   //--> 3

obj.+     //语法错误！
obj["+"]; //--> 4
```

由此可见：

- `.`是`[ ]`的**语法糖**：`a.b`就是`a["b"]`
- 如果索引是变量，只能使用`[ ]`
- 如果索引不是合法标识符，只能使用`.`（比如`obj["+"]`）

> 在 JavaScript 中，索引只能是`string`、`number`或者`Symbol`类型。其中`number`作为索引时，会被隐式转换为`string`。

既然在 JavaScript 中，`[ ]`可以实现所有`.`可以做到的事，为什么我们还需要`.`呢？

One possible answer: **短 → 可读性强**

**这也是为什么 Python 的 Pandas 同时支持用`[ ]`和`.`来取出一列数据**。

## 异常

异常(Exception)实际上是一种控制流程。程序运行出现错误，往往不应该立即终止整个程序。这时可以抛出一个异常，并由最靠近它的`try`语句块捕获。

```javascript
function thisMayFail() {
  console.log("before");
  throw Error("Something went wrong!");
  console.log("after");
}

try {
  thisMayFail();
} catch (e) {
  console.error(e);
}
/*输出：
before
Something went wrong!
*/
```

可以看到，一旦通过`throw`抛出了一个异常，程序的控制权直接来到了`catch`部分。

> `throw`理论上可以抛出任何值，但是，我们**应当**只抛出`Error`或继承自`Error`的值。

下面是一个更加复杂的例子：

```javascript
// thisMayFail函数同上例

function midware() {
  //...
  thisMayFail();
  //...
}

try {
  try {
    midware();
  } catch (e) {
    throw new Error("oops: " + e.message);
  }
} catch (e) {
  console.log(e);
}

/*输出：
before
oops: Something went wrong!
*/
```

可以看到，抛出的异常将*穿过*中间的各层函数，直接来到包裹它的**最内层**`catch`块中。同时，`catch`块中也可以抛出异常，这个异常又将来到更外层的`catch`块中。

> 如果一个异常抛出之后，却没有`catch`块捕获它，它将直接导致程序终止。

Python 中，异常这件事与 JavaScript 有些许不同：

```python
def thisMayFail():
  raise Exception()

try:
  thisMayFail()
except Exception as e:
  print(e)
```

- 可以有多个`except`块，捕获异常时将从上到下，进入**第一个**符合匹配条件的`except`块。
- Python 中的异常，不一定是发生了错误。比如`raise StopIteration()`只是表明迭代已经完成。因此，JavaScript 中的异常更多是一种**处理错误**的工具，而 Python 中的异常更多是一种**控制运行流程**的工具。
