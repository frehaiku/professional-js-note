# 第三章 基本概念

## 语法

### 标识符

指变量、函数、属性的名字，或者函数参数。规则如下：

- 第一个字符必须是字母、下划线（_）或者一个美元符号（$）
- 其他字符可以是字母、下划线、美元符号或数字
- 不能把关键字、保留字、`true`、`false`和`null`作为标识符

按照规范，ECMAScript标识符采用驼峰命名法，也就是变量首字母小写，剩下的每个单词的首字母大写。

### 区分大小写

ECMAScript的变量、函数名和操作符都是区分大小写的，变量名 `test` 和变量名 `Test` 分别表示两个不同的变量

### 注释

包括单行注释和块级注释。单行注释以两个斜杠开头，如下所示：

```javascript
// 单行注释
```

块级注释以一个斜杠和一个星号开头`/*`，以一个星号和一个斜杠`*/`结尾，如下所示：

```javascript
/*
 * 这是一个多行
 * （块级）注释
 */
```
### 严格模式

处理一些不确定的行为，对某些不安全的操作抛出错误。启用严格模式，可以在顶部加上如下代码：

```javascript
'use strict'
```

支持严格模式的浏览器包括 IE10+、Firefox 4+、Safari 5.1+、Opera 12+和 Chrome

### 语句

语句以一个分号结尾;如果省略分号，则由解析器确定语句的结尾

虽然条件控制语句（如if语句）只在执行多条语句的情况下才要求使用代码块，但最佳实践是始终在控制语句中使用代码块————即使代码块中只有一条语句

```javascript
if (test) {
    alert(test);
}
```

## 数据类型

有5种简单数据类型（也称作基本数据类型）：`Undefined`、`Null`、`Boolean`、`Number`和`String`。还有一种复杂数据类型————`Object`,`Object`的本质是由一组无序的名值对组成的。

### typeof操作符

typeof用来检测给定变量的数据类型。对一个值使用 `typeof` 操作符可能返回下列某个字符串：

- `undefined` 如果这个值未定义
- `boolean` 如果这个值是布尔值
- `string` 如果这个值是字符串
- `number` 如果这个值是数值
- `object` 如果这个值是对象或 `null`
- `function` 如果这个值是函数

下面是几个使用 `typeof` 操作符的例子：

```javascript
var message = 'some msg';
console.log(typeof message);    // string
console.log(typeof [1,2,3]);    // object
console.log(typeof null);   // object
console.log(typeof Array.prototype.forEach);    // function
```

有些时候， `typeof` 操作符会返回一些令人疑惑的值。比如，调用 `typeof null` 返回了 `object` ，因为特殊值 `null` 被认为是一个空的对象引用

### Undefined类型

使用 `var` 声明变量但未对其加以初始化时，这个变量的值就是 `undefined`

```javascript
var message;
console.log(typeof message);    // undefined
console.log(typeof age);    // undefined
````

### Null类型
null类型是第二个只有一个值的数据类型，这个特殊的值是null。从逻辑角度来看，null值表示一个空对象指针，而这正是 `typeof` 操作符检测 `null` 值会返回 `object` 的原因

如果定义的变量在将来用于保存对象，那么最好将该变量初始化为 `null` 而不是其他值。这样一来，只要直接检查 `null` 值就可以知道相应的变量是否已经保存了一个对象的引用。

实际上， **`undefined` 值是派生自 `null` 值的，因此规定对它们的相等性测试要返回true** 。不过要注意的是，这个操作符出于比较目的会转换其他操作数

```javascript
console.log(undefined == null);     // true
```

### Boolean类型

在代码里面使用最多的一种类型，该类型只有两个字面值： `true` 和 `false` 。这两个值与数字值不是一回事，因此 `true` 不一定等于1，而 `false` 不一定等于0。

需要注意的是， Boolean类型的字面值 `true` 和 `false` 是区分大小写的。也就是说 `True` 和 `False` 都不是布尔值，只是标识符。

要将这个值转换为Boolean类型，可以调用 `Boolean()` ，如下所示：

```javascript
var message = 'Hello world';
console.log( Boolean(message) );  // false
```

下表是各种数据类型及其对应的转换规则，这些规则对理解流控制语句（如if语句）自动执行的Boolean转换非常重要

数据类型     | 转换为true值                | 转换为false值
----------- | -------------------------- | ------------
Boolean     |true                        | false
String      |非空字符串                    | ""（空字符串）
Number      |任何非零数字值（包括无穷大）    | 0或NaN
Object      |任何对象                     |null
Undefined   |N/A                         |undefined

### Number类型

#### 1.浮点数值

由于保存浮点数值需要的内存空间是保存整数值的两倍，因此下面两种情况下ECMAScript会不失时机地将浮点数值转换为整数值。

- 小数点后面没有跟任何数字，如：1.
- 浮点数值本身表示的就是一个整数，如1.0

对于那些极大或极小的数值，可以用e表示法（科学计数法）表示的浮点数值表示。前面是一个数值，中间是一个大写或小写的字母E，后面是10的幂指数，该幂值将用来与前面的数相乘。下面是一个使用e表示法表示数值的例子：

```javascript
var hugeNum = 3.125e7;     // 等于31250000
var miniNum = 3e-17;     // 等于0.00000000000000003
```

对于 **极大数** 来说，在默认情况下，ECMAScript会将那些小数点前面带有21个零以上的数值转换为以e表示法表示的数值。

对于 **极小数** 来说，在默认情况下，ECMAScript会将那些小数点后面带有6个零以上的浮点数值转换为以e表示法表示的数值。

浮点数值的最高精度是17位小数，但在进行算术运算时其精确度远远不如整数，原因：这是使用基于IEEE754数值的浮点计算的通病。例如，0.1加0.2的结果不是0.3，而是0.30000000000000004。因此，永远不要测试某个特定的浮点数值

#### 2.数值范围

ECMAScript能够表示的最小数值保存在 `Number.MIN_VALUE` 中————在大多数浏览器中，这个值是 `5e-324` ；能够表示最大数值保存在 `Number.MAX_VALUE` 中————在大多数浏览器中，这个值是 `1.7976931348623157e+308`。

如果某次计算的结果超出了JS的数值范围，那么这个数值将自动转换成特殊的 `Infinity` 值。如果这个值是负数，则会被转换为 `-Infinity` （负无穷），如果这个值是整数，则会转换为 `Infinity` （正无穷）。

如果某次计算返回了正或者负的 `Infinity` 的值，那么该值就 **无法继续参与下一次计算** 。要确定一个数值是不是有穷的，可以用 `isFinite()` 函数。这个函数在参数位于最小与最大数值之间时会返回 `true` ，如下面的例子：

```javascript
var result = Number.MAX_VALUE + Number.MAX_VALUE;
console.log( isFinite(result) );    // false
```

#### 3.NaN

NaN，即非数值（Not A Number）是用来表示本来要返回数值的操作数未返回数值的情况，这样就不会抛出错误了，主要出现在将字符串解析成数字出错的场合。例如： `5 - 'x' //NaN`

任何数值除以0都会导致错误，从而停止代码的执行。但在JS中，实际上只有0除以0才会返回NaN，正数除以0返回 `Infinity` ，负数除以0返回 `-Infinity` ，因此不会影响代码的执行。

NaN的特点

- 任何涉及 `NaN` 的操作都会返回 `NaN`
    - `NaN + 5  // false`
- NaN与任何值都不相等，包括 `NaN` 本身
    - `NaN == NaN   // false`

需要注意的是， `NaN` 不是一个独立的数据类型， 而是一种特殊的数值，它的数据类型依然属于 `Number`, 使用 `typeof` 运算符可以看的很清楚

```javascript
typeof NaN;     // 'number'
````

针对这两个特点定义了 `isNaN()` 函数，这个函数会确定参数是否 “不是数值”。 `isNaN()` 在接收到一个值之后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，例如字符串 `"10"` 或 `Boolean` 值。而任何不能被转换为数值的值都会导致函数返回 `true`。

但对于一个 **空数组** 和 **只有一个数值成员** 的数组， `isNaN` 返回 `false` 。 **内部机制** ：先调用对象的 `valueOf()` 方法，确定是否能转换成数值。如果不能，则基于这个值调用 `toString()` 方法，再返回测试值。

```javascript
isNaN( [] );  // false
isNaN( [789] );   // false
isNaN( ['789'] );     // false
```

因此，判断 `NaN` 更可靠的方法是利用其与任何值都不相等的特性。

```javascript
function myIsNaN(value) {
  return value !== value;
}
```

#### 4.数值转换

- `Number()` 函数，将数值转换为数值，用于任何数据类型，具体转换规则如下：
    - 如果是Boolean值，true和false将分别被转换为1和0
    - 如果是null，返回0
    - 如果是undefined，返回NaN
    - 如果是数字型，返回本身
    - 如果是字符串，会忽略前导零，分几种情况
        - 只包含数字，则将其转换为十进制数值
        - 包含有效的浮点格式，则将其转换为对应的浮点数值
        - 包含有效的十六进制格式，则将其转换为对应的十进制格式
        - 字符串是空的，将其转换为0
        - 其余情况返回NaN
    - 如果是对象，则调用对象的 valueOf() 方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的 toString() 方法，然后再次依照前面的规则转换返回的字符串值