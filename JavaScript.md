# JavaScript

### 概念

JS=ECMAScript+DOM+BOM

书写位置

- 行内式 
- 内嵌式
- 外部式

### 变量和运算符

#### 声明变量

- `let`:现代版本JS的新关键字，推荐使用
- `var`:最初JS声明变量的关键字，不推荐
- `var`容许变量提升和重复声明，易使代码混乱

#### 变量类型  

JS是动态类型语言，声明变量无需指定类型。  
`typeof a`返回变量的数据类型

- `number`:无论整数与浮点数，±2^53-1

  - 以及NaN（typeof仍然为number）

- `bigInt`（不支持IE）

- `string`:单双引号均可

  - 还可用Backticks``，可嵌入${variable}

- `boolean`:可直接以表达式赋值

- `symbol` for unique identifiers

- `null`

  - `typeof null`结果为`object`是遗留错误

  > Definitely, `null` is not an object. It is a special value with a separate type of its own.

- `undefined`

以上为7种原始数据类型

`object`:如`let dog = { name : 'Spot', breed : 'Dalmatian' };`

`array`:方括号括起来，并用逗号分隔

#### 算术运算符

- `/`除法:非欧几里得除法
- `**`:幂运算，等价于[`Math.pow(x,y)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/pow) ,指数可非整数

#### 比较运算符

- `===`:严格等于,左右值和数据类型均须相同
- `==`:仅测试值是否相同
  - An equality check converts values using the numeric conversion (hence `"0"` becomes `0`), while the explicit `Boolean` conversion uses another set of rules
  - For `null` and `undefined`,equality check is defined such that, without any conversions, they equal each other and don’t equal anything else. That’s why (2) `null == 0` is false.

#### logical operators

`&&`:the first truthy ,otherwise the last
`||`: the first falsy,otherwise the last

#### Nullish coalescing operator '??'

`a??b` 相当于 `(a !== null && a !== undefined) ? a : b;`
即if a is defined, then a;else b

The OR `||` operator can be used in the same way as `??`

- `||` returns the first *truthy* value.
- `??` returns the first *defined* value.

#### 运算符用于**类型转换**

- String concatenation with binary +
  - eg.`alert(2 + 2 + '1' ); // "41" and not "221"`
- Numeric conversion, unary +
  - It actually does the same thing as `Number(...)`, but is shorter.

#### The comma operator `,`

- **Comma has a very low precedence**,lower than `=`,so parentheses are important

### 输出窗口

[`alert(message)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) shows a message

[`prompt(question,[default])`](https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt) shows a message asking the user to input text. It returns the text or, if Cancel button or Esc is clicked, `null`.

[`confirm(question)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/confirm) shows a message and waits for the user to press “OK” or “Cancel”. It returns true for OK and false for Cancel/Esc.

All these methods are **modal**: they **pause script execution** and **don’t allow the visitor to interact** with the rest of the page until the window has been dismissed.

Limitations of all three methods above:

1. The exact location of the modal window is determined by the browser. Usually, it’s in the center.
2. The exact look of the window also depends on the browser. We can’t modify it.

### 类型转换

#### String Conversion

`String(value)`

#### Numeric Conversion

`Number(value)`

| Value            | Becomes…                                                     |
| :--------------- | :----------------------------------------------------------- |
| `undefined`      | `NaN`                                                        |
| `null`           | `0`                                                          |
| `true and false` | `1` and `0`                                                  |
| `string`         | Whitespaces from the start and end are removed. If the remaining string is empty, the result is `0`. Otherwise, the number is “read” from the string. An error gives `NaN`. |

#### Boolean Conversion

`Boolean(value)`

- Values that are intuitively “empty”, like `0`, an empty string, `null`, `undefined`, and `NaN`, become `false`.
- Other values become `true`.

**NOTE**:Some languages (namely PHP) treat `"0"` as `false`.But in JS,**a non-empty string is always `true`**

Arrow Functions

```javascript
let func = (arg1, arg2, ...argN) => expression
```

### Specials

https://javascript.info/javascript-specials

`'use strict';` enable all modern features of JS

### Comments

**Avoid** “explanatory” comments about  “what is going on in the code”,since the code **should** be easy, clear and and self-descriptive to understand without them,or it may need to be rewritten.Functions themselves tell what’s going on.

Good Comments

- **Describe the architecture**:Provide a **high-level overview** of components, how they interact, what’s the control flow in various situations
- **Document function parameters and usage**:allow us to understand the **purpose of the function** and **use it the right way without looking in its code**
- **Why is the task solved this way?**:What’s written is important. But what’s ***not*** written may be even more important to understand what’s going on.They help to continue development the right way.

### 字符串

基本语法似Python，实质是对象

- `s.length`属性，字符串的长度
- `s1.indexOf(s2)`方法，返回s2在s1中开始的位置，若无则-1
- `s.slice(i,j)`方法，同Python切片，可省略终止位置
- `toLowerCase()`转小写，`toUpperCase()`转大写
- `s.replace(s1,s2)`，返回的字符串中子串s2替换为s1

### 数组

基本语法似Python

- `push()`方法，将一**或多**个元素插入末尾，返回push后数组长度
- `pop()`方法，弹出最后一个元素并返回之
- `unshift()`方法，在开头`push()`
- `shift()`方法，在末尾`pop()`

数组合成字符串，如`myArray.join(',')`,相较`toString()`方法还能指定分隔符不为逗号  
字符串拆成数组，如`s.split(',')`

### Object

#### Create Objects

Objects are created with figure brackets `{…}` with an optional list of ***properties***,which are "**key:value**" pairs.

key is a **string**(also called a "**property name**"),value can be anything

An empty object (“empty cabinet”) can be created using one of two syntaxes:

```javascript
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
let user = {
  name: "John",
  "likes birds": true,  //multiword property name must be quoted
  age: 30,  //建议使用trailing comma(尾随逗号)或hanging comma(悬挂逗号)，便于对行进行修改
}
```

**Object with const can be changed**

```javascript
const user = {  //The `const` fixes the value of `user`, but not its contents.
  name: "John"
};
user.name = "Pete"; // Accepted
user = user2;  //Error!
```

#### square bracket notation: powerful, also cumbersome

```js
let user = {};
// set
user["likes birds"] = true;
// get
alert(user["likes birds"]); // true
// delete
delete user["likes birds"];

let key = prompt("What do you want to know about the user?", "name");
```

In square brackets notation, the variable `key` may be **calculated at run-time or depend on the user input**. And then we use it to access the property. That gives us a great deal of flexibility.The dot notation cannot be used in a similar way

```js
// access by variable
alert( user[key] ); // John (if enter "name")
//The dot notation cannot be used in a similar way:
let key = "name";
alert( user.key ) // undefined
```

**[Computed properties]**(https://javascript.info/object#computed-properties)

We can use square brackets in an object literal when creating an object.

```js
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // take property name from the fruit variable
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};

```

#### [Property value shorthand](https://javascript.info/object#property-value-shorthand)

```js
function makeUser(name, age) {
  return {
    name, // same as name: name
    age,  // same as age: age
    // ...
  };
}
let user = {
  name,  // same as name:name
  age: 30  //可以混用
};
```

#### [Property names limitations](https://javascript.info/object#property-names-limitations)

Any strings or symbols!  Except a special property named `__proto__`

#### [Property existence test, “in” operator](https://javascript.info/object#property-existence-test-in-operator)

```js
"key" in obj  //Syntax. Examples are as follows
let user = { name: "John", age: 30 };
alert( "age" in user ); // true, user.age exists
alert( "blabla" in user ); // false, user.blabla doesn't exist
```

#### Object Copying, references

**A variable stores not the object itself, but its “address in memory”, in other words “a reference” to it.**

**When an object variable is copied – the reference is copied, the object is not duplicated.**

Comparison by reference

The equality `==` and strict equality `===` operators for **objects** work exactly the **same**.

**Two objects are equal only if they are the same object.**

#### Object cloning, `Object.assign`

No built-in method to duplicate an object, we can create a new object and copy the properties of the existing object on the primitive level using `for..in` loop.

Or use the method [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

```js
let user = { name: "John" };
let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// copies all properties from permissions1 and permissions2 into user
Object.assign(user, permissions1, permissions2);
// now user = { name: "John", canView: true, canEdit: true }

// If the copied property name already exists, it gets overwritten:
Object.assign(user, { name: "Pete" });
alert(user.name); // now user = { name: "Pete" }

//use Object.assign for simple cloning
let clone = Object.assign({}, user);
```

`Object.assign` is still so-called “shallow copy” (**nested objects** are copied by reference) or a “deep cloning” function, such as [_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep).