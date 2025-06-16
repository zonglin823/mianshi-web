# Typescript 面试题

Typescript 已经全面普及，尤其大厂大型项目，前端熟悉 Typescript 是标配。

::: tip
如有疑问，可免费 [加群](/docs/services/group.md) 讨论咨询，也可参与 [1v1 面试咨询服务](/docs/services/1v1.md)， 专业、系统、高效、全流程 准备前端面试
:::

## TS 优缺点，使用场景

参考答案

::: details

优点

- 静态类型，减少类型错误
- 有错误会在编译时提醒，而非运行时报错 —— 解释“编译时”和“运行时”
- 智能提示，提高开发效率

缺点

- 学习成本高
- 某些场景下，类型定义会过于混乱，可读性不好，如下代码
- 使用不当会变成 anyscript

```ts
type ModelFieldResolver<T, TKey extends keyof T = any> = (
  this: T,
  ...params: T[TKey] extends (...args: any) => any ? Parameters<T[TKey]> : never
) => T[TKey]
```

适用场景

- 大型项目，业务复杂，维护人员多
- 逻辑性比较强的代码，依赖类型更多
- 组内要有一个熟悉 TS 的架构人员，负责代码规范和质量

:::

PS. 虽然 TS 有很多问题，网上也有很多“弃用 TS”的说法，但目前 TS 仍然是最优解，而且各大前端框架都默认使用 TS 。

## TS 基础类型有哪些

参考答案

::: details

- boolean
- number
- string
- symbol
- bigint
- Enum 枚举
- Array 数组
- Tuple 元祖
- Object 对象
- undefined
- null
- any void never unknown

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/basic-types.html

:::

## 数组 Array 和元组 Tuple 的区别是什么

参考答案

::: details

数组元素只能有一种类型，元祖元素可以有多种类型。

```ts
// 数组，两种定义方式
const list1: number[] = [1, 2, 3]
const list2: Array<string> = ['a', 'b', 'c']

// 元组
let x: [string, number] = ['x', 10]
```

:::

## 枚举 enum 是什么？有什么使用场景？

JS 中没有 enum 枚举，只学过 JS 你可能不知道 enum 。其实在 Java 和 C# 等高级语言中早就有了，TS 中也有。

参考答案

::: details

enum 枚举，一般用于表示有限的一些选项，例如使用 enum 定义 4 个方向

```ts
enum Direction {
  Up = 'UP',
  Down = 'DOWN',
  Left = 'LEFT',
  Right = 'RIGHT',
}
```

其他代码中，我们可以获取某一个方向，用于展示或存储。这样代码更具有可读性和维护行。

```ts
const d = Direction.Up
```

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/enums.html

:::

## keyof 和 typeof 有什么区别？

参考答案

::: details

`typeof` 是 JS 基础用法，用于获取类型，这个很简单。

`keyof` 是 TS 语法，用于获取所有 key 的类型，例如

```ts
interface Person {
  name: string
  age: number
  location: string
}

type PersonType = keyof Person
// 等价于 type PersonType = 'name' | 'age' | 'location'
```

可以把代码拷贝到这里来练习 https://www.tslang.cn/play/index.html

:::

参考资料

::: details

- https://juejin.cn/post/7023238396931735583
- https://juejin.cn/post/7096869746481561608

:::

## any void never unknown 有什么区别

参考答案

::: details

主要区别：

- `any` 任意类型（不进行类型检查）
- `void` 没有任何类型，和 `any` 相反
- `never` 永不存在的值的类型
- `unknown` 未知类型（一个更安全的 any）

代码示例

```ts
function fn(): void {} // void 一般定义函数返回值

// 返回 never 的函数，必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message)
}
function infiniteLoop(): never {
  while (true) {}
}

// unknown 比直接使用 any 更安全
const a: any = 'abc'
console.log(a.toUpperCase()) // 不会报错，但不安全

const b: unknown = 'abc'
// console.log( b.toUpperCase() ) // 会报错！！！
console.log((b as string).toUpperCase()) // 使用 as 转换类型，意思是告诉 TS 编译器：“我知道 b 的类型，我对安全负责”
```

PS：但现在 unknown 用的比 any 少很多，因为麻烦

:::

## unknown 和 any 区别

参考答案

::: details

`unknown` 是更安全的 `any` ，如下代码

```js
const a: any = 'x'
a.toString() // 不报错

const b: unknown = 'y'
// b.toString() // 报错
;(b as string).toString() // 不报错
```

:::

## TS 访问修饰符 public protected private 有什么作用

参考答案

::: details

- public 公开的，谁都能用 （默认）
- protected 受保护的，只有自己和子类可以访问
- private 私有的，仅自己可以访问

这些规则很难用语法去具体描述，看代码示例

```ts
class Person {
  name: string = ''
  protected age: number = 0
  private girlfriend = '小丽'

  // public protected private 也可以修饰方法、getter 等

  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }
}

class Employee extends Person {
  constructor(name: string, age: number) {
    super(name, age)
  }

  getInfo() {
    console.log(this.name)
    console.log(this.age)
    // console.log(this.girlfriend) // 这里会报错，private 属性不能在子类中访问
  }
}

const zhangsan = new Employee('张三', 20)
console.log(zhangsan.name)
// console.log(zhangsan.age) // 这里会报错，protected 属性不能在子类对象中访问，只能在子类中访问
```

:::

追问：`#` 和 `private` 有什么区别呢？

::: details

`#` 在 TS 中可定义私有属性

```ts
class Person {
  #salary: number
  constructor(
    private name: string,
    salary: number
  ) {
    this.#salary = salary
  }
}

const p = new Person('xxx', 5000)
// const n = p.name // 报错
const n = (p as any).name // 可以通过“投机取巧”获取到
console.log('name', n)

// const s = p.#salary // 报错
// const s = (p as any).#salary // 报错
```

区别：

- `#` 属性，不能在参数中定义
- `private` 属性，可通过 `as any` 强制获取
- `#` 属性，更私密

:::

## type 和 interface 共同和区别，如何选择

type 和 interface 有很多相同之处，很多人因此而产生“选择困难症”，这也是 TS 热议的话题。

共同点

::: details

- 都能描述一个对象结构
- 都能被 class 实现
- 都能被扩展

```ts
// 接口
interface User {
  name: string
  age: number
  getName: () => string
}

// 自定义类型
type UserType = {
  name: string
  age: number
  getName: () => string
}

// class UserClass implements User {
class UserClass implements UserType {
  name = 'x'
  age = 20
  getName() {
    return this.name
  }
}
```

:::

区别

::: details

- type 可以声明基础类型
- type 有联合类型和交差类型
- type 可以被 `typeof` 赋值

```ts
// type 基础类型
type name = string
type list = Array<string>

// type 联合类型
type info = string | number

type T1 = { name: string }
type T2 = { age: number }
// interface T2 { age: number  } // 联合，还可以是 interface ，乱吧...
type T3 = T1 | T2
const a: T3 = { name: 'x' }
type T4 = T1 & T2
const b: T4 = { age: 20, name: 'x' }

// typeof 获取
type T5 = typeof b

//【补充】还有个 keyof ，它和 typeof 完全不同，它是获取 key 类型的
type K1 = keyof T5
const k: K1 = 'name'
```

:::

如何选择？

::: details

根据社区的使用习惯，推荐使用方式

- 能用 interface 就尽量用 interface
- 除非必须用 type 的时候才用 type

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/interfaces.html

:::

PS. 其实你混淆 type 和 interface 不是你的问题，这是 TS 设计的问题，或者说 TS 设计初衷和后来演变带来的副作用。

## 什么是泛型，如何使用它？

只学过 JS 的同学不知道泛型，其实它早就是 C# 和 Java 中的重要概念了。初学泛型可能会比较迷惑，需要多些代码多练习。

泛型的定义

::: details

泛型 Generics 即通用类型，可以灵活的定义类型而无需写死。

```ts
const list: Array<string> = ['a', 'b']
const numbers: Array<number> = [10, 20]

interface User {
  name: string
  age: number
}
const userList: Array<User> = [{ name: 'x', age: 20 }]
```

:::

泛型的使用

::: details

1. 用于函数

```ts
// Type 一般可简写为 T
function fn<Type>(arg: Type): Type {
  return arg
}
const x1 = fn<string>('xxx')

// 可以有多个泛型，名称自己定义
function fn<T, K>(a: T, b: K) {
  console.log(a, b)
}
fn<string, number>('x', 10)
```

2. 用于 class

```ts
class SomeClass<T> {
  name: T
  constructor(name: T) {
    this.name = name
  }
  getName(): T {
    return this.name
  }
}
const s1 = new SomeClass<String>('xx')
```

3. 用于 type

```ts
function fn<T>(arg: T): T {
  return arg
}

const myFn: <U>(arg: U) => U = fn // U T 随便定义
```

4. 用于 interface

```ts
// interface F1 {
//   <T>(arg: T): T;
// }
interface F1<T> {
  (arg: T): T
}
function fn<T>(arg: T): T {
  return arg
}
const myFn: F1<number> = fn
```

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/generics.html

:::

## 什么是交叉类型和联合类型

### 交叉类型 `T1 & T2`

交叉类型是将多个类型合并为一个类型，包含了所需的所有类型的特性。例如 `T1 & T2 & T3`

代码示例

::: details

```ts
interface U1 {
  name: string
  city: string
}
interface U2 {
  name: string
  age: number
}
type UserType1 = U1 & U2
const userA: UserType1 = { name: 'x', age: 20, city: 'beijing' }

// 可在 userA 获取所有属性，相当于“并集”
userA.name
userA.age
userA.city
```

:::

注意事项

::: details

1. 两个类型的相同属性，如果类型不同（冲突了），则该属性是 `never` 类型

```ts
// 如上代码
// U1 name:string ，U2 name: number
// 则 UserType1 name 是 never
```

2. 基础类型没办法交叉，会返回 `never`

```ts
type T = string & number // never
```

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/advanced-types.html

:::

### 联合类型 `T1 | T2`

一种“或”的关系。格式如 `T1 | T2 | T3`。代码示例如下

::: details

```ts
interface U1 {
  name: string
  city: string
}
interface U2 {
  name: string
  age: number
}

function fn(): U1 | U2 {
  return {
    name: 'x',
    age: 20,
  }
}
```

:::

注意事项

::: details

基础类型可以联合

```ts
type T = string | number
const a: T = 'x'
const b: T = 100
```

但如果未赋值的情况下，联合类型无法使用 string 或 number 的方法

```ts
function fn(x: string | number) {
  console.log(x.length) // 报错
}
```

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/advanced-types.html

:::

## 是否用过工具类型

TS 工具类型有 `Partial` `Required` `Omit` `ReadOnly` 等，熟练使用 TS 的人都会熟悉这些工具类型。

参考答案

::: details

`Partial<T>` 属性设置为可选

```ts
interface User {
  name: string
  age: number
}
type User1 = Partial<User> // 属性全部可选，类似 `?`
const u: User1 = {}
```

`Require<T>` 属性设置为必选 （和 Partial 相反）

`Pick<T, K>` 挑选部分属性

```ts
interface User {
  name: string
  age: number
  city: string
}
type User1 = Pick<User, 'name' | 'age'> // 只选择两个属性
const u: User1 = { name: 'x', age: 20 }
```

`Omit<T, K>` 剔除部分属性（和 Pick 相反）

`ReadOnly<T>` 属性设置为只读

相当于为每个属性都设置一遍 `readonly`

```ts
interface User {
  name: string
  age: number
}
type User1 = Readonly<User>
const u: User1 = { name: 'x', age: 20 }
// u.name = 'y' // 报错
```

:::

## TS 这些符号 `?` `?.` `??` `!` `_` `&` `|` `#` 分别什么意思

参考答案

::: details

`?` 可选属性，可选参数

```ts
interface User {
  name: string
  age?: number
}
const u: User = { name: 'xx' } // age 可写 可不写

function fn(a: number, b?: number) {
  console.log(a, b)
}
fn(10) // 第二个参数可不传
```

`?.` 可选链：有则获取，没有则返回 undefined ，但不报错。

```ts
const user: any = {
  info: {
    city: '北京',
  },
}
// const c = user && user.info && user.info.city
const c = user?.info?.city
console.log(c)
```

`??` 空值合并运算符：当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数。

```ts
const user: any = {
  // name: '张三'
  index: 0,
}
// const n1 = user.name ?? '暂无姓名'
const n2 = user.name || '暂无姓名' // 某些情况可用 || 代替
console.log('name', n2)

const i1 = user.index ?? '暂无 index'
const i2 = user.index || '暂无 index' // 当是 0 （或 false 空字符串等）时，就不能直接用 || 代替
console.log('index', i1)
```

`!` 非空断言操作符：忽略 undefined null ，自己把控风险

```ts
function fn(a?: string) {
  return a!.length // 加 ! 表示忽略 undefined 情况
}
```

`_` 数字分隔符：分割数字，增加可读性

```ts
const million = 1_000_000
const phone = 173_1777_7777

// 编译出 js 就是普通数字
```

其他的本文都有讲解

- `&` 交叉类型
- `_` 联合类型
- `#` 私有属性

:::

## 什么是抽象类 abstract class

抽象类是 C# 和 Java 的常见语法，TS 也有，但日常前端开发使用并不多。

参考答案

::: details

抽象类，不能直接被实例化，必须派生一个子类才能使用。

```ts
abstract class Animal {
  abstract makeSound(): void
  move(): void {
    console.log('roaming the earch...')
  }
}

// const a = new Animal() // 直接实例化，报错

class Dog extends Animal {
  // 必须要实现 Animal 中的抽象方法，否则报错
  makeSound() {
    console.log('wang wang')
  }
}

const d = new Dog()
d.makeSound()
d.move()
```

:::

参考资料

::: details

- https://www.tslang.cn/docs/handbook/classes.html 其中搜索 `abstract class`

:::

## 如何扩展 window 属性，如何定义第三方模块的类型

参考答案

::: details

```ts
declare interface Window {
  test: string
}

window.test = 'aa'
console.log(window.test)
```

:::

## 是否有过真实的 Typescript 开发经验，讲一下你的使用体验

开放性问题，需要结合你实际开发经验来总结。可以从以下几个方面考虑

::: details

- 在 Vue React 或其他框架使用时遇到的障碍？
- 在打包构建时，有没有遇到 TS 语法问题而打包失败？
- 有没有用很多 `any` ？如何避免 `any` 泛滥？

:::

参考资料

::: details

- https://juejin.cn/post/6929793926979125255


:::
## TypeScript中的基本数据类型有哪些？
::: details
TypeScript 提供了比 JavaScript 更丰富的类型系统，基本数据类型包括：

- 原始类型：boolean、number、string、null、undefined、symbol、bigint
- 对象类型：object、array、tuple(元组)
- 特殊类型：any、unknown、void、never、enum(枚举)
- TypeScript 类型系统的核心优势在于提供了静态类型检查，可以在编译阶段发现潜在问题。

详细解析📚

原始类型 💎 

boolean 布尔类型 ✅ 

```ts
let isDone: boolean = false;
```
number 数字类型 🔢
TypeScript 中所有数字都是浮点数，支持十进制、十六进制、二进制和八进制字面量。

```ts
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```
string 字符串类型 📝

```ts
let name: string = "TypeScript";
let sentence: string = `Hello, ${name}!`; // 模板字符串
```
null 和 undefined 类型 ⚠️
```ts
let n: null = null;
let u: undefined = undefined;
```
这两个类型比较特殊，默认情况下它们是所有类型的子类型，但开启 strictNullChecks 后，它们就只能赋值给 any 和它们各自的类型。

symbol 类型 🔑 

ES6 引入的新原始类型，表示唯一的标识符。


```ts
let sym1: symbol = Symbol();
let sym2: symbol = Symbol('key');
```
bigint 类型 🔄 

ES2020 引入，用于表示任意精度的整数。

```ts
let big: bigint = 100n;
```
对象类型 📦 

object 对象类型 🧩
```ts
let obj: object = { prop: 'value' };
```
array 数组类型 📚 

TypeScript 提供两种方式定义数组：

```ts
let list1: number[] = [1, 2, 3];
let list2: Array<number> = [1, 2, 3]; // 泛型语法
```
tuple 元组类型 📋 

元组类型允许表示一个已知元素数量和类型的数组。

```ts
let x: [string, number] = ["hello", 10];
```
特殊类型 🌟 

any 类型 🃏 

```ts
let notSure: any = 4;
notSure = "maybe a string";
notSure = false; // 都可以，编译器不会检查
```
unknown 类型 ❓ 

比 any 更安全的类型，需要进行类型检查或断言才能使用。

```ts
let value: unknown = 30;
if (typeof value === "number") {
    let sum = value + 10; // OK
}
```
void 类型 🚫 

表示没有任何类型，通常用作函数返回值。

```ts
function warnUser(): void {
    console.log("Warning message");
}
```
never 类型 ❌ 

表示永不存在的值的类型，常用于永远抛出异常或无法执行到终点的函数返回值类型。

```ts
function error(message: string): never {
    throw new Error(message);
}
```
enum 枚举类型 🔄
用于定义一组命名常量。

```ts
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```
类型系统示意图 📊 

类型的使用场景对比 📊
- 类型	适用场景	特点
- boolean	逻辑判断	只有 true/false 两种值
- number	数值计算	所有数字都是浮点数
- string	文本处理	支持模板字符串
- array	存储同类型数据集合	长度可变
- tuple	已知元素数量和类型的数组	固定长度和类型
- enum	命名常量集合	提高代码可读性
- any	不确定类型或动态内容	失去类型检查优势
- unknown	类型安全的 any	使用前需类型断言
- void	函数无返回值	通常用于函数声明
- never	永不返回的函数	抛出异常或无限循环
在日常开发中，我们应当尽量避免使用 any 类型，以充分利用 TypeScript 的类型检查优势。而 unknown 类型则是一个更安全的选择，因为它迫使我们在使用前进行类型检查。就像我经常跟同事说的："能用具体类型就别用 any，宁可多写几行代码，也别在半夜收到生产环境的 bug 通知！" 😄
:::
## any、unknown、never、void类型的区别？
::: details
TypeScript中这四种特殊类型各有不同的用途和限制：

any类型：==最宽松的类型==，可以赋值给任何类型，也可以接收任何类型值，完全跳过类型检查。

unknown类型：==类型安全的any==，可以接收任何类型值，但不能直接赋值给其他类型（必须先进行类型检查或断言）。

never类型：==最底层类型==，表示永远不会有值的类型，常用于表示永远不会返回的函数（如抛出异常或无限循环）。

void类型：==函数没有返回值==时使用，表示函数执行完后不返回任何值（或隐式返回undefined）。

详细解析📚 

any类型 - 类型系统的后门 🚪

any类型是TypeScript提供的"紧急出口"，当你不确定类型或需要快速迁移JavaScript代码时非常有用。但老实说，它就像是TypeScript世界里的"万能钥匙"，随意使用会让TypeScript的类型保护形同虚设。

```ts
let whatever: any = 42;
whatever = "嗨，我变成字符串啦";
whatever = { name: "我现在又变成对象啦" };
whatever.foo(); // 编译不会报错，但运行时可能会挂！
```
在实际项目中，我经常看到新手把any当作解决类型问题的"万能药"，但这会埋下隐患！如果你的代码里any满天飞，那基本上等于没用TypeScript🙈。

unknown类型 - 安全版的any 🛡️ 

unknown是TypeScript 3.0引入的，它更安全！可以把它理解为"我知道有值，但不确定是什么类型"。

```ts
let value: unknown = 42;
value = "现在是字符串";

// value.toUpperCase(); // ❌ 错误！不能直接操作unknown类型

// 必须先检查或断言类型
if (typeof value === "string") {
    value.toUpperCase(); // ✅ 现在安全了
}
```
个人感受：unknown就像是有保险栓的手枪，你得先解除安全锁（类型检查）才能使用，这样就避免了很多运行时的"意外走火"。

never类型 - 永远不可能 ⛔ 

never表示永远不会出现的值的类型。这听起来可能有点抽象，但实际上非常实用！

```ts
// 永远不会返回的函数
function throwError(message: string): never {
    throw new Error(message);
}

// 永远不会结束的函数
function infiniteLoop(): never {
    while (true) {}
}
```
never在联合类型中会被自动忽略，这一特性在做类型收窄时特别有用：

```ts
type Foo = string | number | never; // 等同于 string | number
```
void类型 - 没有返回值 🚫 

void表示函数没有返回值，或者说返回undefined：

```ts
function logMessage(message: string): void {
    console.log(message);
    // 不需要return语句，或者可以return;
}
```
和其他语言不同，TypeScript中的void类型实际上可以被赋值为undefined或null（在strictNullChecks为false时）。

类型层级关系 📊 

实战应用示例 💻
```ts
// 安全地处理未知类型的数据
function processData(input: unknown): string {
    // 必须先进行类型检查
    if (typeof input === "string") {
        return input.toUpperCase();
    } else if (typeof input === "number") {
        return input.toFixed(2);
    } else {
        // 处理其他情况或抛出错误
        return String(input);
    }
}

// 用never做穷尽检查
type Shape = Circle | Square;

function getArea(shape: Shape) {
    if ("radius" in shape) {
        return Math.PI * shape.radius ** 2;
    } else if ("width" in shape) {
        return shape.width ** 2;
    }
    
    // 如果未来Shape类型新增了其他形状，这里会报错
    const exhaustiveCheck: never = shape;
    return exhaustiveCheck;
}
```
说实话，这几个类型看似简单，但用好它们能让你的代码健壮性提升一个档次！特别是用unknown替代any，以及用never做穷尽性检查，这都是进阶TypeScript开发的必备技能。

记住，类型系统是为了帮助我们写出更可靠的代码，而不是绊脚石。灵活运用这些特殊类型，让TypeScript为你的开发保驾护航吧！

:::

## 什么是类型断言？有几种写法？

::: details

类型断言是 TypeScript 中的一种机制，允许开发者手动指定一个值的类型，从而覆盖编译器的自动类型推断。当你比 TypeScript 更了解某个值的类型时，类型断言特别有用。

TypeScript 中类型断言有两种写法：

尖括号语法：<类型>值 

as 语法：值 as 类型 

```ts
// 尖括号语法
let someValue: any = "这是一个字符串";
let strLength: number = (<string>someValue).length;

// as 语法
let someValue: any = "这是一个字符串";
let strLength: number = (someValue as string).length;
```
在 JSX 中只能使用 as 语法，因此 as 语法是更为推荐的写法。

详细解析📚 

类型断言是什么 🤔 

说实话，TypeScript 的类型断言有点像是在跟编译器"交流"："嘿，兄弟，我知道我在干啥，相信我！"

类型断言本质上是在告诉 TypeScript 编译器："虽然你不确定这个值的类型，但我确定，请按照我说的类型来处理"。

这就像你去医院，医生不确定你的病情，但你却说："我确定我是感冒，给我开点感冒药就行"一样。

类型断言的使用场景 🌟 

处理 DOM 元素  

```ts
// 没有类型断言时
const myButton = document.getElementById('myButton'); 
// myButton 的类型是 HTMLElement | null

// 使用类型断言
const myButton = document.getElementById('myButton') as HTMLButtonElement;
// 现在 myButton 的类型是 HTMLButtonElement
myButton.disabled = true; // 不会报错
```
处理联合类型

```ts
interface Bird {
  fly(): void;
  layEggs(): void;
}

interface Fish {
  swim(): void;
  layEggs(): void;
}

function getSmallPet(): Fish | Bird {
  // ...
  return { swim: () => {}, layEggs: () => {} };
}

let pet = getSmallPet();
// 使用类型断言确定是鱼
(pet as Fish).swim();

```
类型断言的注意事项 ⚠️ 

类型断言不是类型转换！它只在编译阶段起作用，不会改变运行时的类型或值。如果你断言的类型和实际类型不符，可能会导致运行时错误。

```ts
// 这在编译时不会报错
let someValue: string = "hello";
let num: number = (someValue as unknown as number); 

// 但运行时会出问题，因为字符串不能作为数字使用
console.log(num + 10); // "hello10" 而不是数学运算
```
从 TypeScript 3.0 开始，引入了更安全的const断言：值 as const，它会把字面量变成只读类型。

```ts
// 普通数组
let arr = [1, 2, 3]; // 类型是 number[]

// 使用 const 断言
let arr = [1, 2, 3] as const; // 类型是 readonly [1, 2, 3]
```
类型断言的最佳实践 📝 

类型断言与类型转换的区别 🔄

类型断言	类型转换

编译时行为	运行时行为
不改变运行时类型	实际转换值的类型
告诉编译器"相信我"	实际进行数据转换
例：`value as string`	例：`String(value)`
记住，类型断言就像是给编译器戴上有色眼镜，而不是真的把东西变成其他颜色！在实际项目中，尽量减少类型断言的使用，多使用类型声明和类型守卫，这样代码会更加健壮。

只有当你确实比 TypeScript 更了解情况的时候，再去使用类型断言。否则，还是乖乖听编译器的话吧！
:::
## 联合类型和交叉类型的区别及使用场景？
::: details
联合类型（Union Types）和交叉类型（Intersection Types）是 TypeScript 中两种重要的类型组合方式：

联合类型（|）：表示一个值可以是多种类型中的一种，只能访问所有类型的共有属性。常用于函数参数、多态变量等场景。

交叉类型（&）：表示将多个类型合并成一个新类型，包含所有类型的所有属性。常用于对象合并、混入模式等场景。

简记：联合类型是"或"关系（A 或 B），交叉类型是"与"关系（A 和 B）。

详细解析📚 

联合类型与交叉类型的本质区别 🧩 

联合类型和交叉类型乍看很像，但本质上完全不同。我经常用这个比喻来解释：联合类型就像"点菜"，你点的是鱼香肉丝或宫保鸡丁的其中一道；而交叉类型则像"套餐"，你同时得到了主食、菜品和饮料。

来看看它们在实际代码中的表现：

```ts
// 联合类型示例
type ID = string | number;
const id1: ID = "abc123"; // 可以是字符串
const id2: ID = 123456;   // 也可以是数字
const id3: ID = true;     // ❌ 错误！不能是布尔值

// 交叉类型示例
type Person = { name: string; age: number };
type Employee = { companyId: string; role: string };
type StaffMember = Person & Employee;

const staff: StaffMember = {
  name: "张三",      // 来自Person
  age: 30,          // 来自Person
  companyId: "C001", // 来自Employee
  role: "开发工程师"  // 来自Employee
}; // ✅ 必须同时包含所有属性
```
类型运算的可视化 📊 

这张图可以帮你直观理解两种类型的区别：

在原始类型上的行为差异 ⚡ 

这一点特别容易混淆！在原始类型上：

联合类型表现符合直觉：string | number 表示字符串或数字
交叉类型可能出人意料：string & number 结果是 never（因为没有同时是字符串和数字的值）
```ts
// 原始类型的联合 - 很好理解
type StringOrNumber = string | number; // 字符串或数字

// 原始类型的交叉 - 结果是never
type ImpossibleType = string & number; // never，因为没有值能同时是字符串和数字
```
实战应用场景分析 🛠️ 

联合类型的实战场景 

函数参数接受多种类型：

```ts
function formatId(id: string | number): string {
  if (typeof id === "string") {
    return id.toUpperCase();
  } else {
    return `ID-${id.toString().padStart(6, '0')}`;
  }
}
```
React组件接受不同类型的props：

```ts
type ButtonProps = 
  | { variant: "text"; color?: string }
  | { variant: "outlined"; color: string; borderWidth: number }
  | { variant: "contained"; color: string; elevation?: number };

function Button(props: ButtonProps) {
  // 实现按钮逻辑
}
```
交叉类型的实战场景 

扩展现有类型：
```ts
type BaseConfig = {
  apiUrl: string;
  timeout: number;
};

type DevConfig = BaseConfig & {
  debugMode: boolean;
  mockData: boolean;
};

const config: DevConfig = {
  apiUrl: "https://api.example.com",
  timeout: 3000,
  debugMode: true,
  mockData: true
};
```
实现混入模式：
```ts
type Loggable = {
  log: (message: string) => void;
};

type Serializable = {
  serialize: () => string;
};

// 一个既可日志记录又可序列化的对象
type LoggableAndSerializable = Loggable & Serializable;

const item: LoggableAndSerializable = {
  log(message) { console.log(message); },
  serialize() { return JSON.stringify(this); }
};
```
使用时的常见陷阱 ⚠️ 

联合类型陷阱

使用联合类型时，你只能访问所有可能类型的共有属性和方法：

```ts
type Bird = { fly(): void; layEggs(): void };
type Fish = { swim(): void; layEggs(): void };

function getSmallPet(): Bird | Fish {
  // 返回Bird或Fish
  return Math.random() > 0.5 
    ? { fly() {}, layEggs() {} } 
    : { swim() {}, layEggs() {} };
}

const pet = getSmallPet();
pet.layEggs(); // ✅ 没问题，两种类型都有这个方法
pet.fly();     // ❌ 错误！Fish没有fly方法
```
交叉类型陷阱 

交叉类型可能产生冲突的属性类型：

```ts
type A = { x: number };
type B = { x: string };
type AB = A & B; // x的类型是 number & string，即 never

const value: AB = { 
  x: 10 as never // 必须用断言，因为实际上不可能满足这个类型
};
```
小技巧：类型保护与区分联合类型 🛡️ 

在处理联合类型时，使用类型保护可以更安全地访问特定类型的属性：

```ts
type Square = { kind: "square"; size: number };
type Rectangle = { kind: "rectangle"; width: number; height: number };
type Circle = { kind: "circle"; radius: number };

type Shape = Square | Rectangle | Circle;

function area(shape: Shape): number {
  // 使用判别属性(discriminant)
  switch (shape.kind) {
    case "square":
      return shape.size * shape.size; // 这里TypeScript知道shape是Square类型
    case "rectangle":
      return shape.width * shape.height; // 这里是Rectangle类型
    case "circle":
      return Math.PI * shape.radius ** 2; // 这里是Circle类型
    default:
      return 0;
  }
}
```
总之，理解联合类型和交叉类型的区别对于用好TypeScript至关重要。联合类型让我们能灵活处理多种可能的值，而交叉类型则让我们能够组合不同的特性，打造出功能丰富的类型。在实际开发中，这两种类型组合方式常常一起使用，相互配合，让我们的代码既灵活又健壮！

:::
## 可选属性和只读属性如何定义？
::: details
在 TypeScript 中：

可选属性：使用 ? 符号定义，表示该属性可以存在也可以不存在

```ts
interface User {
  name: string;
  age?: number; // 可选属性
}
```
只读属性：使用 readonly 关键字定义，表示该属性只能在对象创建时被赋值，之后不能修改

```ts
interface Config {
  readonly apiKey: string; // 只读属性
  timeout: number;
}
```
详细解析📚 

可选属性 (Optional Properties) 🌱

可选属性让我们能够更灵活地定义接口，特别是在处理那些并非所有情况都需要的数据时非常有用。

```ts
interface Product {
  id: number;
  name: string;
  description?: string; // 可选的描述
  discount?: number;    // 可选的折扣
}

// 以下两种用法都是合法的
const phone: Product = { 
  id: 1, 
  name: "iPhone" 
};

const laptop: Product = { 
  id: 2, 
  name: "MacBook", 
  description: "M3芯片版本",
  discount: 0.1
};
```
在实际项目中，可选属性经常用于：

表单数据模型
API请求参数
配置对象
只读属性 (Readonly Properties) 🔒 

只读属性能够防止对象创建后被修改，增强了代码的安全性和可预测性。

```ts
interface ApiConfig {
  readonly baseUrl: string;
  readonly timeout: number;
  cacheEnabled: boolean; // 非只读属性
}

const config: ApiConfig = {
  baseUrl: "https://api.example.com",
  timeout: 3000,
  cacheEnabled: true
};

// 错误！不能修改只读属性
// config.baseUrl = "https://new-api.example.com"; ❌

// 可以修改非只读属性
config.cacheEnabled = false; // ✅
```
在我日常开发中，我发现只读属性特别适合：

配置对象
不可变数据模型
API响应类型定义
可选与只读属性的组合使用 🔄
有时候，我们需要同时使用这两种属性修饰符：

```ts
interface UserSettings {
  readonly id: number;
  readonly createdAt: Date;
  name: string;
  theme?: string;
  readonly apiKey?: string; // 既是只读又是可选的
}
```
直观对比 📊  

工作中的实战案例 💼

在一个电商项目中，我们可能会这样定义商品类型：

```ts
interface Product {
  readonly id: string;         // 商品ID创建后不应更改
  readonly createdAt: Date;    // 创建时间不应被修改
  name: string;                // 商品名称（必需且可修改）
  price: number;               // 价格（必需且可修改）
  description?: string;        // 描述（可选）
  images?: string[];           // 图片链接（可选）
  discount?: number;           // 折扣（可选）
  readonly sku?: string;       // 库存单位（可选且只读）
}
```
这样的类型定义既保证了核心数据的完整性，又提供了足够的灵活性，让我们能够应对各种商品数据场景。

在团队协作中，清晰的类型定义能大大减少沟通成本，新同事看到这样的接口定义就能立刻理解数据的约束和规则，减少不必要的bug。

:::
## 如何声明一个只读的数组？
::: details
在TypeScript中，声明只读数组主要有三种方式：

使用 readonly 修饰符：
```ts
const arr: readonly number[] = [1, 2, 3];
```
使用 `ReadonlyArray<T>` 类型：
```ts
const arr: ReadonlyArray<number> = [1, 2, 3];
```
使用 `as const` 断言（最严格的只读）：
```ts
const arr = [1, 2, 3] as const;
```
在JavaScript中，可以使用` Object.freeze()` 来实现：

```js
const arr = Object.freeze([1, 2, 3]);
```
这些方法都能确保数组不被修改，但实现细节和严格程度有所不同。

详细解析📚 

TypeScript中的只读数组 🛡️ 

TypeScript为我们提供了几种声明只读数组的方式，每种都有其特点：

readonly修饰符 ✨ 

readonly 是最常用的方式，它告诉编译器这个数组不应该被修改：

```ts
const arr: readonly number[] = [1, 2, 3];
// arr.push(4); // 错误：类型"readonly number[]"上不存在属性"push"
// arr[0] = 99; // 错误：无法分配到"0"，因为它是只读属性
```
ReadonlyArray类型 📊 

`ReadonlyArray<T>` 是一个特殊的泛型类型，专门用于只读数组：

```ts
const arr: ReadonlyArray<string> = ["张三", "李四", "王五"];
```
这种方式和 readonly T[] 效果几乎一样，只是写法不同。

as const断言 🔒
as const 是最严格的只读方式，它会将数组转换为只读元组，每个元素都是字面量类型：

```ts
// 类型为：readonly [1, 2, 3]，而不仅仅是readonly number[]
const arr = [1, 2, 3] as const;
```
来看看这三种方式的区别：

JavaScript中的只读数组 💡
JavaScript没有内置的类型系统，但我们可以用 Object.freeze() 来实现运行时的只读保护：

```js
const arr = Object.freeze([1, 2, 3]);

// 以下操作在严格模式下会报错，非严格模式下静默失败
arr.push(4); // 错误
arr[0] = 99; // 错误
```
但要注意，Object.freeze() 只是浅冻结，如果数组包含对象，那么这些对象的属性仍然可以被修改：


```js
const arr = Object.freeze([{name: '张三'}]);
arr[0].name = '李四'; // 这是可以的！
```
要实现深度冻结，需要递归调用 Object.freeze()：

```js  
function deepFreeze(obj) {
  Object.values(obj).forEach(value => {
    if (typeof value === 'object' && value !== null) {
      deepFreeze(value);
    }
  });
  return Object.freeze(obj);
}

const arr = deepFreeze([{name: '张三'}]);
```
实战场景 🚀 

只读数组在什么情况下特别有用呢？

配置数据：不希望被意外修改的配置

```ts
const ALLOWED_ROLES = ['admin', 'editor', 'viewer'] as const;
```
API响应：确保从API获取的数据不被意外修改

```ts
function fetchUsers(): Promise<ReadonlyArray<User>> {
  // 获取用户数据
}
```
组件Props：确保组件不会修改传入的数组数据

```ts
interface ListProps {
  items: readonly string[];
}
```
状态管理：在Redux或其他状态管理库中保证状态不可变性

```ts
// 使用不可变数据更新状态
const newState = {
  ...state,
  items: [...state.items, newItem]
};
```
只读数组是函数式编程和不可变数据理念的实践，它能帮助我们写出更可靠、更容易调试的代码。在大型前端应用中，数据不可变性是降低复杂度的关键因素之一！

:::
## Interface和Type的区别及使用场景？
::: details
TypeScript中的interface和type都用于定义类型，但它们有明显区别：

语法结构不同：


- interface是接口声明
- type是类型别名 

扩展方式不同：

- interface使用extends关键字继承
- type使用&交叉类型合并
核心区别：

- interface可以被重复声明并自动合并
- type不可重复声明，一个名字只能定义一次 

使用场景：

- interface适合定义对象结构和API契约
- type适合复杂类型组合和函数类型 

详细解析📚

Interface的特点 🏷️

interface本质上就是给对象定义一种"契约"，它告诉我们："嘿，符合这个接口的对象必须长这个样子！"

```ts
interface Person {
  name: string;
  age: number;
}
```
声明合并（超能力！）✨ 

interface最强大的特性是可以重复声明自动合并，这在扩展第三方库类型时特别有用：

```ts
interface Person {
  name: string;
}

interface Person { // 不会报错，会自动合并
  age: number;
}

// 等同于：
interface Person {
  name: string;
  age: number;
}
```
这简直就是给类型"打补丁"的绝佳方式！当你想扩展一些你无法修改源码的库时，这个特性简直是救星。

Type的特点 📝 

type是类型别名，它就像给类型取了个好记的"昵称"：

```ts
type Person = {
  name: string;
  age: number;
};
```
更强的组合能力 💪 

type最大的优势是它的"组合性"，可以轻松表达复杂类型：

```ts
// 联合类型
type ID = string | number;

// 条件类型
type MessageOf<T> = T extends { message: infer M } ? M : never;

// 映射类型
type Partial<T> = { [P in keyof T]?: T[P] };
```
两者选择的实战指南 🚀 

我整理了一张决策流程图，帮你快速选择该用哪个：

真实项目中的对比案例 🌟
下面用一个项目中的真实例子说明区别：

- 特性	Interface	Type	推荐选择
- 定义对象结构	✅ 很适合	✅ 可以用	Interface
- 多次声明合并	✅ 支持	❌ 不支持	Interface
- 联合&交叉类型	⚠️ 有限支持	✅ 完全支持	Type
- 计算属性	⚠️ 有限支持	✅ 完全支持	Type
- 元组和数组	⚠️ 可以但不够直观	✅ 更直观	Type
- 库扩展	✅ 最佳选择	❌ 不合适	Interface
我的实际使用心得 💭
老实说，我在日常开发中更偏向于使用type，尤其是在React项目中。为什么？因为type对组件props的定义更加灵活，特别是需要组合多种类型时。

但是！当我开发公共API或库时，我会毫不犹豫选择interface，因为它的声明合并特性让使用者可以轻松扩展类型。


记住一句话："Interface是开放的，Type是封闭的"。


当你需要让其他人"继续添加"，选interface；当你需要"精确定义"不希望被改变，选type。

性能考量 ⚡ 

在大型项目中，TypeScript编译器处理大量interface的性能略优于type，因为interface的设计更符合结构类型系统的实现方式。不过，对于大多数项目来说，这点差异几乎可以忽略不计。

别纠结太多，选择最适合你当前需求的就好！
:::
## 如何扩展接口和类型别名？
::: details
在 TypeScript 中扩展类型有两种主要方式：

接口扩展：接口可以通过 extends 关键字继承其他接口

```ts
interface Person { name: string }
interface Employee extends Person { employeeId: number }
```
类型别名扩展：类型别名使用 &（交叉类型）实现扩展

```ts
type Person = { name: string }
type Employee = Person & { employeeId: number }
```
核心区别：

接口可以被 重复声明并自动合并
类型别名 不可重复声明，但更灵活，可以表达更复杂的类型组合
详细解析📚 

接口扩展详解 🔄 

接口是 TypeScript 中最常用的类型声明方式之一，它真的非常灵活！

```ts
// 基础接口
interface Animal {
  name: string;
}

// 扩展单个接口
interface Dog extends Animal {
  bark(): void;
}

// 扩展多个接口
interface Pet {
  owner: string;
}

interface FamilyDog extends Dog, Pet {
  isGoodBoy: boolean;
}
```
接口有个超级好用的特性 - 声明合并。你可以多次声明同一个接口，TypeScript 会自动把它们合并在一起：

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

// 相当于：
// interface User {
//   name: string;
//   age: number;
// }
```
这在扩展第三方库的类型时特别有用，不用去修改源码，直接添加新属性就完事了！

类型别名扩展详解 🧩 

类型别名更像是给类型起个昵称，但它的能力可不止于此：

```ts
// 基础类型别名
type Person = {
  name: string;
};

// 使用 & 扩展类型
type Employee = Person & {
  employeeId: number;
};

// 扩展多个类型
type ContactInfo = {
  email: string;
  phone?: string;
};

type FullEmployee = Employee & ContactInfo;
```
类型别名的强大之处在于它几乎可以表示任何类型，甚至是一些接口无法表达的复杂类型：

```ts
// 联合类型
type ID = string | number;

// 条件类型
type IsString<T> = T extends string ? true : false;

// 工具类型
type Nullable<T> = T | null | undefined;
```
接口 vs 类型别名对比 ⚔️ 

实战案例 🛠️ 

来看一个实际开发中的例子 - 构建一个组件的 Props 类型：

<!-- ```ts -->
选择建议 🌟 

用 接口 当你需要：

定义对象结构且可能需要后续扩展
创建可被类实现的契约
利用声明合并特性
用 类型别名 当你需要：

定义非对象类型（如联合类型、映射类型）
使用更高级的类型操作
表达复杂的条件类型
记住，选择哪种方式主要看项目需求和团队习惯。在大多数情况下，两者都能完成任务，关键是保持一致性！
:::
## 什么是索引签名？如何使用？
::: details
索引签名是 TypeScript 中一种特殊的语法，它允许我们动态添加属性到对象类型中，并为这些属性指定统一的类型。

索引签名的基本语法是：

```ts
interface Dictionary {
  [key: string]: any;
}
```
使用索引签名时需要注意以下几点：

索引签名的键（key）只能是 string、number 或 symbol 类型
当一个类型同时拥有字符串和数字索引签名时，数字索引的返回值类型必须是字符串索引返回值类型的子类型
所有明确定义的属性类型必须与索引签名返回值类型兼容

详细解析📚 

什么是索引签名？ 📚 

想象一下，你在写代码时经常会遇到这种情况：需要创建一个对象，但你事先并不知道这个对象会有哪些属性名称，只知道所有属性的值都是相同类型的。这时候，索引签名就派上用场了！

索引签名本质上是告诉 TypeScript："嘿，这个对象可能会有各种各样的属性，但我保证它们的值都是某种特定类型的！"

基础用法 💡 

最简单的索引签名长这样：

```ts
interface StringDictionary {
  [key: string]: string;
}

// 可以这样使用
const dict: StringDictionary = {};
dict["name"] = "张三";  // ✅ 没问题
dict["age"] = 25;      // ❌ 错误！值必须是字符串类型
```
实战案例 🛠️ 

1. 创建配置对象
```ts
interface Config {
  [key: string]: string | number | boolean;
  version: string;  // 必须的属性
}

const appConfig: Config = {
  version: "1.0.0",
  enableDarkMode: true,
  maxUsers: 100,
  appName: "面试宝典"
};
```
2. 多种索引签名
```ts
interface MixedDictionary {
  [index: number]: string;
  [key: string]: string | number;
}

const mixed: MixedDictionary = {
  0: "零",      // 数字索引
  "one": "一",  // 字符串索引
  "count": 10   // 字符串索引可以是数字类型
};
```
索引签名的限制 ⚠️ 

使用索引签名时有几个需要注意的地方：

属性检查更宽松：使用索引签名后，TypeScript 的属性检查会变得宽松，可能隐藏一些拼写错误。

所有属性必须匹配索引签名：如果定义了索引签名，所有明确定义的属性类型必须与索引签名兼容。

```ts
interface Wrong {
  [key: string]: string;
  count: number;  // ❌ 错误！count的类型必须兼容string
}

interface Correct {
  [key: string]: string | number;
  count: number;  // ✅ 正确，number兼容索引签名的返回类型
}
```

索引签名 vs Record 类型 🔄 

在实际开发中，我们常常会用到 Record 工具类型，它是索引签名的一种便捷表达：

```ts
// 这两种写法等价
interface Dictionary {
  [key: string]: number;
}

type Dictionary2 = Record<string, number>;
```

来看个简单的流程图，帮你理解何时使用索引签名：

实际工作中的应用 💼 

在前端开发中，索引签名常见于以下场景：

状态管理：Redux 或 Vuex 的状态对象

表单处理：动态表单字段的类型定义

API 响应处理：处理后端返回的不确定结构的数据

国际化：定义多语言文本映射

```ts
// 国际化文本示例
interface I18nTexts {
  [locale: string]: {
    [key: string]: string;
  }
}

const texts: I18nTexts = {
  "zh-CN": {
    welcome: "欢迎使用我们的应用",
    login: "登录"
  },
  "en-US": {
    welcome: "Welcome to our application",
    login: "Login"
  }
};
```

索引签名让我们的代码既灵活又类型安全，真是 TypeScript 中的一把利器！记住，用好它可以让你的代码更健壮，但也别忘了在适当的时候使用更精确的类型定义。
:::
## 如何使用接口描述函数类型？
::: details

在 TypeScript 中，可以通过以下方式使用接口描述函数类型：

使用函数类型签名：
```ts
interface MathFunc {
  (x: number, y: number): number;
}

const add: MathFunc = (a, b) => a + b;
```
使用方法签名（在对象内部定义函数）：

```ts
interface Calculator {
  calculate(x: number, y: number): number;
}

const adder: Calculator = {
  calculate: (a, b) => a + b
};
```
使用可调用接口与泛型组合：
```ts
interface ProcessFunc<T, U> {
  (input: T): U;
}

const stringToNumber: ProcessFunc<string, number> = (str) => parseInt(str);
```

详细解析📚  


函数类型接口的本质 ⚙️

说实话，函数类型接口就是给函数定义一个"合同"，告诉TypeScript："嘿，这个函数应该长这样！"它规定了函数的参数类型和返回值类型。

当你在项目中与团队协作时，这简直是救命稻草！不用担心同事会传错参数类型，TypeScript直接在编码阶段就会给你报错。

函数接口的几种写法 📋 

函数类型签名（最常用）✨ 

这种方式直接定义了一个"可被调用"的接口：

```ts
interface GreetFunction {
  (name: string, age?: number): string;
}

// 使用接口
const greet: GreetFunction = (name, age) => {
  if (age !== undefined) {
    return `你好，${name}，你已经${age}岁啦！`;
  }
  return `你好，${name}！`;
};

console.log(greet('小明')); // 你好，小明！
console.log(greet('小红', 18)); // 你好，小红，你已经18岁啦！
```

对象方法签名 🔧 

这种方式定义对象内的方法：

```ts
interface UserService {
  findById(id: number): User;
  create(user: User): boolean;
}

// 实现接口
const userService: UserService = {
  findById(id) {
    // 查找用户逻辑
    return { id, name: '张三' };
  },
  create(user) {
    // 创建用户逻辑
    return true;
  }
};
```

函数重载与接口 🔄 

接口也可以用来描述函数重载：

```ts
interface StringArray {
  (key: string): string[];
  (key: number): string;
}
```

不过，老实说，这种写法在实际项目中用得不多，更常见的是直接用函数重载语法。

泛型与函数接口的强强联合 💪 

当你不确定具体的类型，但知道输入和输出之间的关系时，泛型简直是神器：

```ts
interface Transform<T, U> {
  (input: T): U;
}

const numberToString: Transform<number, string> = (num) => num.toString();
const stringToArray: Transform<string, string[]> = (str) => str.split('');

console.log(numberToString(123)); // "123"
console.log(stringToArray('abc')); // ["a", "b", "c"]
```

函数类型定义的不同方式对比 📊 

- 方式	优点	缺点	适用场景
- 接口定义	可复用性高，语义清晰	写法稍长	多处使用同一函数类型
- 类型别名	写法简洁	语义不如接口直观	简单函数类型定义
- 内联定义	最简洁	不可复用	只使用一次的场景
- 实战案例：事件处理函数 🎯
- 在React项目中，我经常这样定义事件处理函数类型：

```ts
interface ChangeEventHandler {
  (event: React.ChangeEvent<HTMLInputElement>): void;
}

const handleInputChange: ChangeEventHandler = (event) => {
  setInputValue(event.target.value);
};
```

函数类型接口的演化 🌱 

看看从简单到复杂的函数接口定义：

小结：什么时候该用函数接口？ 💡 

说实话，函数接口最大的优势在于代码复用和语义化。当你发现自己在多个地方定义同样结构的函数类型时，就该考虑抽象成接口了。

在我日常开发中，特别是写一些通用组件库时，合理定义函数接口能让API更加清晰，用户（也就是你的同事们）使用起来也更加顺手。而且，TypeScript编辑器的智能提示也会变得超级给力！

:::
## 什么是映射类型？
::: details
映射类型是 TypeScript 中的一种高级类型工具，允许你基于一个已有的类型创建新的类型，它通过遍历现有类型的所有属性键来生成新类型。映射类型使用的语法类似于索引签名，但目的是类型转换而非属性访问。

```ts
// 最常见的映射类型示例
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
}

// 使用
interface User {
  name: string;
  age: number;
}

// 所有属性变为只读
type ReadonlyUser = Readonly<User>;
```

详细解析📚 

映射类型的本质 🧬

映射类型说白了就是类型版的循环遍历！想象一下，我们有一个对象类型，然后想对它的每个属性都做同样的变化，比如全部变成可选的、只读的，或者完全换一种类型。手动一个个改太麻烦了，这时候映射类型就派上用场了。

映射类型的基本语法长这样:
```ts
type 新类型<T> = {
  [P in keyof T]: 某种类型表达式;
} 
```
这段代码的意思是：遍历 T 类型的所有属性键（用 P 表示），然后给每个属性设置新的类型。

TypeScript 内置的映射类型 🛠️ 

TypeScript 已经帮我们实现了几个超实用的映射类型:

`Partial<T>` - 把所有属性变成可选的
`Required<T>` - 把所有属性变成必需的
`Readonly<T>` - 把所有属性变成只读的
`Record<K, T>` - 创建属性键为 K，属性值为 T 的对象类型
```ts
// 这些类型的实现
type Partial<T> = { [P in keyof T]?: T[P] };
type Required<T> = { [P in keyof T]-?: T[P] };
type Readonly<T> = { readonly [P in keyof T]: T[P] };
type Record<K extends keyof any, T> = { [P in K]: T };

```
映射类型的修饰符 ✨ 

映射类型还支持两个额外的修饰符操作：

添加或移除 readonly - 用 readonly 或 -readonly
添加或移除可选性 - 用 ? 或 -?
```ts
// 移除所有属性的readonly修饰符
type Mutable<T> = {
  -readonly [P in keyof T]: T[P]
};

// 把所有可选属性变成必需的
type Concrete<T> = {
  [P in keyof T]-?: T[P]
};

```
映射类型与条件类型结合 🔄 

实战中，映射类型经常和条件类型一起使用，这组合简直就是类型体操的最强套路:

```ts
// 只保留对象中的函数属性
type FunctionProps<T> = {
  [K in keyof T]: T[K] extends Function ? T[K] : never
};

interface Mixed {
  name: string;
  age: number;
  greet: () => void;
  calculate: (x: number) => number;
}

// 结果只有 greet 和 calculate 属性
type OnlyFunctions = FunctionProps<Mixed>;

```
实战案例: 表单验证 📋
假设我们正在开发一个表单验证系统，使用映射类型可以很优雅地生成表单错误类型:

```ts
interface LoginForm {
  username: string;
  password: string;
  remember: boolean;
}

// 生成错误信息类型
type FormErrors<T> = {
  [K in keyof T]?: string;
};

// 使用
const errors: FormErrors<LoginForm> = {
  username: "用户名不能为空",
  password: "密码长度不足"
};

```

为什么需要学会映射类型？🤔

学会映射类型不是为了装X（好吧，有一点是），主要是它真的能大幅减少类型定义的重复代码。在大型项目中，很多相关的接口往往有相似的结构，用映射类型可以让你的类型定义既精简又严谨，随着一个类型的更新，相关的派生类型也能自动更新。

写好的类型系统就像是给未来的自己和同事的一份保障，在重构和维护时能帮你揪出各种潜在问题。映射类型是这个保障系统中的一把利器！

:::
## 函数重载如何实现及使用场景？
::: details
TypeScript中的函数重载允许我们为同一个函数提供多种类型定义，使函数能够根据不同的参数类型和返回值类型进行工作。实现函数重载主要通过以下步骤：

定义多个函数签名（不包含实现）
定义一个通用函数实现（包含所有重载情况的处理逻辑）
```ts
// 函数重载签名
function add(a: number, b: number): number;
function add(a: string, b: string): string;

// 函数实现
function add(a: any, b: any): any {
  return a + b;
}

```
常见使用场景：

- 处理不同类型参数的函数
- 需要根据参数类型返回不同类型结果的函数
- 构建灵活API时实现类型安全 

详细解析📚 

什么是函数重载？ 🤔

函数重载是TypeScript提供的一个强大特性，让我们能写出更加灵活又类型安全的代码。简单来说，就是一个函数名可以对应多种不同的参数和返回类型组合。

当你调用一个重载函数时，TypeScript编译器会根据你传入的参数类型，自动匹配最合适的函数签名，并提供相应的类型检查和代码补全。这真的超级方便！

函数重载的实现方式 ⚙️ 

在TypeScript中，函数重载的实现有点特别，它分为两部分：

重载签名部分
首先，我们需要定义多个函数签名（只有类型，没有函数体）：

```ts
function format(value: string): string;
function format(value: number, precision?: number): string;
function format(value: Date): string;

```
实现签名部分
然后，我们需要提供一个实际的函数实现，它必须兼容所有上面定义的重载签名：

```ts
function format(value: string | number | Date, precision?: number): string {
  if (typeof value === 'string') {
    return value.trim();
  } else if (typeof value === 'number') {
    return value.toFixed(precision || 2);
  } else {
    return value.toISOString();
  }
}

```
函数重载VS联合类型 🔄 

很多人会问：为什么不直接用联合类型呢？看看这个例子你就明白了：

```ts
// 使用联合类型
function process(x: number | string): number | string {
  if (typeof x === 'number') {
    return x * 2;
  } else {
    return x.toUpperCase();
  }
}

const result = process(10); // 类型为 number | string

```
问题来了！虽然我们知道当传入数字时返回的肯定是数字，但TypeScript不知道，它只知道返回类型是number | string。

而使用函数重载：

```ts
function process(x: number): number;
function process(x: string): string;
function process(x: number | string): number | string {
  if (typeof x === 'number') {
    return x * 2;
  } else {
    return x.toUpperCase();
  }
}

const result = process(10); // 类型为 number

```
这样调用`process(10)`的返回值类型就精确地是number，而不是联合类型了！

函数重载的使用场景 🌟 

让我们通过几个实际例子来看看函数重载的威力：

1. DOM操作函数
```ts
// 根据ID获取元素
function getElementById(id: string): HTMLElement | null;
// 根据选择器获取元素集合
function getElementById(selector: string, context: Element): NodeListOf<Element>;
// 实现
function getElementById(idOrSelector: string, context?: Element): HTMLElement | null | NodeListOf<Element> {
  if (context) {
    return context.querySelectorAll(idOrSelector);
  }
  return document.getElementById(idOrSelector);
}

```
2. 工具函数
```ts
// 字符串数组去重
function unique(arr: string[]): string[];
// 数字数组去重
function unique(arr: number[]): number[];
// 实现
function unique<T extends string | number>(arr: T[]): T[] {
  return [...new Set(arr)];
}
```
3. 处理不同数据类型
```ts
function convert(value: string): number;
function convert(value: number): string;
function convert(value: Date): string;
function convert(value: string | number | Date): string | number {
  if (typeof value === 'string') {
    return parseFloat(value);
  } else if (typeof value === 'number') {
    return String(value);
  } else {
    return value.toISOString();
  }
}

```
函数重载的最佳实践 🏆 

注意事项 ⚠️

实现签名必须兼容所有重载签名：实现函数的参数类型必须是所有重载签名参数类型的联合。

重载顺序很重要：TypeScript会按照定义的顺序尝试匹配重载签名，所以把更具体的签名放在前面。

避免过度使用：函数重载虽好，但如果过于复杂，可能导致代码难以维护，有时拆分为多个函数更清晰。

总之，函数重载是TypeScript中一个非常强大的特性，掌握它能让你的代码既灵活又类型安全，特别是在设计库或API时尤为有用！

:::
## 如何为函数参数和返回值添加类型注解？
::: details

TypeScript函数参数和返回值类型注解 📝 

在TypeScript中，为函数添加类型注解非常直观：

```ts
// 基本语法
function 函数名(参数1: 类型1, 参数2: 类型2): 返回值类型 {
  // 函数体
  return 返回值;
}

```
具体来说：

- 参数类型注解：在参数名后添加冒号和类型 参数名: 类型
- 返回值类型注解：在参数列表后添加冒号和类型 ): 返回值类型
- 箭头函数：const 函数名 = (参数: 类型): 返回值类型 => { 函数体 }
- 可选参数：使用问号标记 参数名?: 类型
- 默认参数：直接赋值 参数名: 类型 = 默认值

详细解析📚 

基础类型注解 🧩 

函数是TypeScript中最常用的结构之一，给它们加上类型注解不仅能让代码更易读，还能帮我们在编译时捕获潜在错误。

```ts
// 带类型注解的函数声明
function greet(name: string): string {
  return `你好，${name}！`;
}

// 带类型注解的箭头函数
const multiply = (a: number, b: number): number => {
  return a * b;
};

```
哎，TypeScript对咱前端开发者是真的友好，写代码时编辑器就会提示你参数类型不对，再也不用担心运行时才发现类型错误啦！

常见函数类型模式 🔄 

可选参数与默认值 ✨ 

```ts
// 可选参数（注意可选参数必须放在必选参数后面）
function buildName(firstName: string, lastName?: string): string {
  if (lastName) {
    return `${firstName} ${lastName}`;
  }
  return firstName;
}

// 默认参数
function greeting(name: string, message: string = "欢迎光临"): string {
  return `${message}，${name}！`;
}
```
使用可选参数时，记得做空值检查，不然TypeScript再强大也救不了运行时错误哦！

剩余参数 📊 

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

// 调用
console.log(sum(1, 2, 3, 4)); // 10

```
这个写法超级方便，再也不用担心参数个数不确定的情况了！

函数类型表达式 📈 

```ts
// 函数类型表达式
type MathOperation = (x: number, y: number) => number;

// 使用函数类型
const add: MathOperation = (a, b) => a + b;
const subtract: MathOperation = (a, b) => a - b;
```
这招特别适合团队协作，定义好类型后，同事们实现起来就轻松多了！

函数重载 🔄 

当同一个函数需要处理不同类型的输入时，函数重载就派上用场了：

```ts
// 重载签名
function process(x: number): number;
function process(x: string): string;

// 实现签名
function process(x: number | string): number | string {
  if (typeof x === "number") {
    return x * 2;
  } else {
    return x.repeat(2);
  }
}

// 调用
console.log(process(10));    // 20
console.log(process("Hi")); // "HiHi"

```
重载让我们的函数更智能，根据不同参数类型返回对应的类型，用起来贼爽！

泛型函数 🧬 

当函数的参数类型和返回值类型有关联时，泛型就是不二之选：

```ts
function identity<T>(arg: T): T {
  return arg;
}

// 调用方式
let output1 = identity<string>("myString");
let output2 = identity(42); // 类型推断为 number

```
泛型是TypeScript的一大杀器，灵活度简直拉满，写起通用函数来特别给力！

类型推断与最佳实践 🎯 

在实际开发中，我有这些小技巧分享给大家：

- 返回值类型尽量显式标注：即使TypeScript能推断出来，显式标注可以让代码更易读
- 复杂函数一定要加类型：特别是多人协作项目，类型注解就是最好的文档
- 参数类型放心交给推断：如果函数很简单，有时候可以省略参数类型，让TypeScript自己推断
- 实战案例：我们来看一个真实项目中的表单验证函数：

```ts
type ValidationResult = { valid: boolean; message?: string };

function validateForm(
  formData: Record<string, unknown>,
  rules: Record<string, (value: unknown) => ValidationResult>
): { isValid: boolean; errors: Record<string, string> } {
  const errors: Record<string, string> = {};
  let isValid = true;

  for (const field in rules) {
    if (Object.prototype.hasOwnProperty.call(rules, field)) {
      const result = rules[field](formData[field]);
      if (!result.valid) {
        isValid = false;
        errors[field] = result.message || `${field}验证失败`;
      }
    }
  }

  return { isValid, errors };
}

```
这个函数用起来特别灵活，既能保证类型安全，又能适应各种表单验证场景。

总之，TypeScript的类型注解是前端开发的一大利器，用好了能大大提高代码质量和开发效率。面试时能够清晰地讲解这些概念，绝对会给面试官留下专业的印象！

:::
## 可选参数、默认参数和剩余参数如何定义？
::: details

TypeScript中的可选参数、默认参数和剩余参数
在TypeScript中，函数参数有三种特殊类型：

可选参数 ⚙️

使用 ? 符号定义
语法: function funcName(param?: type) { }
必须放在必选参数后面
默认参数 🛠️

使用 = 赋予默认值
语法: function funcName(param: type = defaultValue) { }
调用时若省略该参数，将使用默认值
剩余参数 📦

使用 ... 语法收集多个参数到数组
语法: function funcName(...restParams: type[]) { }
只能有一个剩余参数且必须位于最后
typescript
复制代码
// 三种参数类型的组合示例
function processUser(
  id: number,              // 必选参数
  name?: string,           // 可选参数
  age: number = 18,        // 默认参数
  ...skills: string[]      // 剩余参数
) {
  // 函数实现...
}
详细解析📚
可选参数详解 ✨
可选参数让我们能够处理那些"可能存在也可能不存在"的参数，真的超级实用！

typescript
复制代码
function greet(name: string, title?: string) {
  if (title) {
    return `Hello, ${title} ${name}!`;
  }
  return `Hello, ${name}!`;
}

greet("小明");           // 输出: "Hello, 小明!"
greet("小明", "工程师");  // 输出: "Hello, 工程师 小明!"
在实际开发中，可选参数经常用于配置对象，让API更加灵活。但要记住，可选参数必须放在必选参数后面，否则编译器会报错！

默认参数详解 🎯
默认参数是我开发中的救星，它让代码更简洁也更健壮：

typescript
复制代码
function createProfile(
  name: string,
  role: string = "开发者",
  level: number = 1
) {
  return {
    name,
    role,
    level
  };
}

createProfile("张三");                  // { name: "张三", role: "开发者", level: 1 }
createProfile("李四", "设计师");         // { name: "李四", role: "设计师", level: 1 }
createProfile("王五", "产品经理", 3);    // { name: "王五", role: "产品经理", level: 3 }
与JavaScript不同，TypeScript会同时检查类型！如果你尝试传入错误类型的默认值，编译器会立刻提醒你。这就是为什么我喜欢TS的原因之一！

剩余参数详解 📚
剩余参数是处理未知数量参数的完美方案：

typescript
复制代码
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

sum(1, 2);          // 3
sum(1, 2, 3, 4, 5); // 15
在React组件开发中，剩余参数常用于传递props：

typescript
复制代码
interface ButtonProps {
  label: string;
  primary?: boolean;
}

function Button({ label, primary = false, ...restProps }: ButtonProps & React.HTMLAttributes<HTMLButtonElement>) {
  // 可以把剩余的props如onClick, className等传给底层元素
  return <button className={primary ? 'primary-btn' : 'default-btn'} {...restProps}>{label}</button>;
}
三种参数的使用场景对比 🔄
是

否

是

否

是

参数类型选择

是否一定需要此参数?

使用必选参数

是否有合理默认值?

使用默认参数 param=defaultValue

使用可选参数 param?

需要接收不定数量参数?

使用剩余参数 ...params


实战小技巧 💪
在日常开发中，我喜欢将这三种参数结合使用，特别是在构建灵活API时：

typescript
复制代码
// 一个实用的HTTP请求函数
function fetchData(
  url: string,                         // 必选 - API端点
  method: "GET" | "POST" = "GET",      // 默认参数 - HTTP方法
  body?: object,                       // 可选参数 - 请求体
  ...headers: [string, string][]       // 剩余参数 - 额外的头信息
) {
  const options: RequestInit = { method };
  
  if (body && method !== "GET") {
    options.body = JSON.stringify(body);
  }
  
  if (headers.length) {
    options.headers = Object.fromEntries(headers);
  }
  
  return fetch(url, options).then(res => res.json());
}

// 使用示例
fetchData("/api/users");  // 简单GET请求
fetchData("/api/users", "POST", { name: "新用户" });  // POST带请求体
fetchData("/api/users", "GET", undefined, ["Authorization", "Bearer token"]); // 带认证的GET请求
记住，参数设计是API设计的核心，好的参数设计可以让你的函数既易用又灵活，既安全又高效！

:::
## this在TypeScript中如何使用？
::: details

TypeScript 中的 this 主要通过以下几种方式使用：

显式声明 this 类型：在函数参数首位使用 this: Type 来声明函数内 this 的类型，这是 TS 特有的语法

箭头函数捕获外部 this：箭头函数不创建自己的 this 上下文，而是继承外部作用域的 this

类中的 this：在类方法中，this 默认指向类实例，TypeScript 会自动推导

this 参数装饰器：可以在函数首参数使用 this 关键字进行类型标注，增强类型安全

noImplicitThis 配置：启用此配置强制要求明确 this 的类型，提高代码健壮性

详细解析📚
this 的基本概念与特性 🧩
在 JavaScript 中，this 的指向一直是个让人头疼的问题，而 TypeScript 在此基础上增加了类型系统的支持。说实话，我第一次接触 TS 中的 this 处理时也是一脸懵逼，直到搞清楚了几个关键点才算开窍。

在 TypeScript 中，this 的类型检查主要是为了解决 JS 中 this 上下文丢失的问题。你想想，JS 中的 this 可是会随着调用方式变来变去的，这对类型系统是个巨大挑战！

typescript
复制代码
// 这样写在 JS 中没问题，但在 TS 中会报错
const button = document.querySelector('button');
button.addEventListener('click', function() {
  this.innerHTML = 'Clicked!'; // TS 报错：'this' 隐式具有 'any' 类型
});
显式 this 类型标注 ✍️
TypeScript 提供了一种特殊语法，允许我们在函数的第一个参数位置声明 this 的类型（这个参数在运行时是不存在的）：

typescript
复制代码
function myMethod(this: MyClass, arg1: string, arg2: number) {
  // 这里的 this 被指定为 MyClass 类型
  this.property = arg1;
}
这简直是救命稻草！特别是在处理回调函数时，可以确保 this 指向正确的对象。

在类中使用 this 🏛️
TypeScript 中的类是最容易处理 this 的地方，因为类方法中的 this 默认指向类实例：

typescript
复制代码
class Counter {
  private count: number = 0;
  
  increment() {
    // 这里的 this 被自动推导为 Counter 类型
    this.count++;
    return this.count;
  }
  
  // 这里可能会有问题
  getCounterFunc() {
    return function() {
      // 错误：this 的类型是 any
      return this.count;
    };
  }
  
  // 使用箭头函数捕获正确的 this
  getCounterArrowFunc() {
    return () => {
      // 正确：this 是 Counter 类型
      return this.count;
    };
  }
}
this 类型与泛型结合 🔄
还有个实用技巧是将 this 类型与泛型结合，实现链式调用：

typescript
复制代码
class Chain<T> {
  // 返回 this 类型，支持链式调用
  process(data: T): this {
    // 处理数据
    return this;
  }
  
  validate(): this {
    // 验证数据
    return this;
  }
}

// 可以链式调用
new Chain<string>().process("data").validate();
这个模式在构建流畅 API 时简直太好用了！我记得第一次看到这种用法时眼前一亮。

this 类型的实战应用 🛠️
来看个实际应用场景，假设我们在开发一个表单验证库：

returns
Validator
+validate() : this
+required() : this
+email() : this
+min(length: number) : this
+max(length: number) : this
+result() : ValidationResult
ValidationResult
+isValid: boolean
+errors: string[]

实现代码：

typescript
复制代码
class Validator {
  private value: string;
  private errors: string[] = [];
  
  constructor(value: string) {
    this.value = value;
  }
  
  required(): this {
    if (!this.value) {
      this.errors.push('此字段为必填项');
    }
    return this;
  }
  
  email(): this {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(this.value)) {
      this.errors.push('请输入有效的邮箱地址');
    }
    return this;
  }
  
  min(length: number): this {
    if (this.value.length < length) {
      this.errors.push(`长度不能小于${length}个字符`);
    }
    return this;
  }
  
  result() {
    return {
      isValid: this.errors.length === 0,
      errors: this.errors
    };
  }
}

// 使用示例
const emailValidator = new Validator('user@example.com');
const result = emailValidator.required().email().min(5).result();
console.log(result); // { isValid: true, errors: [] }
这种链式调用的实现依赖于每个方法都返回 this，使得接口非常流畅和直观。

noImplicitThis 配置 ⚙️
别忘了在 tsconfig.json 中启用 noImplicitThis: true，这会强制你显式指定 this 的类型，避免意外：

json
复制代码
{
  "compilerOptions": {
    "noImplicitThis": true
  }
}
启用后，TypeScript 会在 this 的类型不明确时提示错误，帮你避免各种莫名其妙的 bug。相信我，这能省下你不少调试时间！

TypeScript 中 this 的正确使用确实需要一定的经验积累，但一旦掌握，会让你的代码更加健壮和可维护。希望这些要点能帮你在面试中脱颖而出！



:::
## TypeScript中的访问修饰符有哪些？
::: details

TypeScript中有四种主要访问修饰符：

public（默认）：在任何地方都可访问
private：仅在声明类内部可访问
protected：在声明类及其子类中可访问
readonly：属性只能在声明时或构造函数中赋值
还有两个特殊修饰符：

static：定义类静态成员，通过类名直接访问
参数属性修饰符（如constructor(private name: string)）：简化属性声明和初始化
详细解析📚
访问修饰符是TypeScript提供的一种强大特性，它让你能够更好地控制代码的封装性。说实话，刚开始学的时候我也经常搞混，下面我来详细解释一下：

各修饰符的使用场景与区别 🔄
typescript
复制代码
class Person {
    public name: string;         // 公开属性，默认值，可省略public关键字
    private age: number;         // 私有属性，只能在Person类内部使用
    protected address: string;   // 受保护属性，可在Person及其子类中使用
    readonly id: number;         // 只读属性，初始化后不可修改
    static country: string = "中国"; // 静态属性，通过Person.country访问
    
    constructor(name: string, age: number, address: string, id: number) {
        this.name = name;
        this.age = age;
        this.address = address;
        this.id = id; // 只读属性可以在构造函数中初始化
    }
    
    // 简写形式：参数属性（同时声明并初始化类成员）
    // constructor(public name: string, private age: number, protected address: string) {}
}
修饰符对比表 📊
修饰符	类内部访问	子类访问	类外部访问	特点
public	✅	✅	✅	默认修饰符，完全开放
private	✅	❌	❌	强封装，严格保护
protected	✅	✅	❌	适合需要继承的场景
readonly	✅	✅	✅	只读不可改，初始化后锁定
访问修饰符使用流程图 🔄
所有地方都能访问

仅类内部访问

类和子类访问

不允许修改

开始设计类

确定属性访问范围

使用public

使用private

使用protected

使用readonly

设计方法和构造函数

完成类设计


实战案例：用户信息管理 🛠️
typescript
复制代码
class User {
    // 唯一标识，不可修改
    readonly id: number;
    // 对外可见的用户名
    public username: string;
    // 私密信息，仅类内可见
    private password: string;
    // 可在子类中使用的信息
    protected email: string;
    // 所有用户共享的信息
    static platform: string = "我的面试题库";
    
    constructor(id: number, username: string, password: string, email: string) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.email = email;
    }
    
    public login(): boolean {
        // 校验密码逻辑
        return this.validatePassword(this.password);
    }
    
    private validatePassword(inputPassword: string): boolean {
        // 密码验证逻辑，私有方法
        return inputPassword === this.password;
    }
    
    protected notifyUser(): void {
        // 通知用户，子类可覆写
        console.log(`已向 ${this.email} 发送通知`);
    }
}

// 子类
class AdminUser extends User {
    constructor(id: number, username: string, password: string, email: string) {
        super(id, username, password, email);
    }
    
    public sendSystemMessage(): void {
        // 可以访问protected成员
        this.email; // ✅ 可以访问
        // this.password; // ❌ 无法访问private成员
        this.notifyUser(); // ✅ 可以访问protected方法
    }
}

// 使用
const user = new User(1, "张三", "password123", "zhangsan@example.com");
console.log(user.username); // ✅ 可以访问public成员
// console.log(user.password); // ❌ 无法访问private成员
// console.log(user.email); // ❌ 无法访问protected成员
console.log(User.platform); // ✅ 可以访问static成员
// user.id = 2; // ❌ 无法修改readonly成员
在我日常开发中，这些访问修饰符真的帮了大忙！private 让我能好好保护那些不想被外部碰的核心逻辑，protected 在做框架或基类时特别有用，让子类能拿到一些共享的东西。

记住，选择合适的访问修饰符不仅是为了代码安全，也是为了让你的API设计更加清晰明了。当你在设计一个类时，先思考每个属性方法应该对外暴露到什么程度，这样能让你的代码更加健壮和专业！

:::
## 可选参数、默认参数和剩余参数如何定义？
::: details


:::
## 可选参数、默认参数和剩余参数如何定义？
::: details


:::
## 可选参数、默认参数和剩余参数如何定义？
::: details


:::
## 可选参数、默认参数和剩余参数如何定义？
::: details


:::
## 可选参数、默认参数和剩余参数如何定义？
::: details


:::
## 可选参数、默认参数和剩余参数如何定义？
::: details


:::
## 可选参数、默认参数和剩余参数如何定义？
::: details
