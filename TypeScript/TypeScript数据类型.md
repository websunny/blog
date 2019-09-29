# TypeScript数据类型

***

> 为了让程序有价值，我们需要能够处理最简单的数据单元：数字，字符串，结构体，布尔值等。 TypeScript支持与JavaScript几乎相同的数据类型，此外还提供了实用的枚举类型方便我们使用。

## 基础类型

### 布尔值

最基本的数据类型就是简单的true/false值，在JavaScript和TypeScript里叫做`boolean`（其它语言中也一样）。

```ts
let _boolean: boolean = false;
```

### 数值

使用 `number`定义数值类型：

```ts
let _number: number = 110
```

### 字符串

使用 `string`定义字符串类型：

```ts
let _string: string = 'Mr.shu'
```

当然也支持模版字符串

```ts
let name: string = 'Tom'
let Hello: string =`hello, my name is ${name}`
```

### 空值

JavaScript 没有空值的概念，而在TypeScript中我们一般用来表示没有任何返回值的函数

```ts
function alertName(): void {
    alert('My name is Tom')
}
```

声明一个 `void`类型的变量没有什么用，因为你只能将它赋值为 `undefined`和 `null`：

```ts
let unusable: void = undefined
```

### Null 和 Undefined

TypeScript里，`undefined`和`null`两者各自有自己的类型分别叫做`undefined`和`null`。 和 `void`相似，它们的本身的类型用处不是很大：

```ts
let u: undefined = undefined
let n: null = null
```

### 任意值

如果是 `any`类型，则允许被赋值为任意类型。

```ts
let myFavoriteNumber: any = 'seven'
myFavoriteNumber = 7
```

在任意值上访问任何属性或者方法都是允许的：

```ts
let anyThing: any = 'hello';
console.log(anyThing.myName);
```

变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型

```ts
let _any
_any = 1
_any = 'any'
```

上述的例子其实涉及到了TypeScript的一大特点类型推断，如果没有明确的指定类型，那么 TypeScript 会依照类型推论（Type Inference）的规则推断出一个类型。

## 联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种。

```ts
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

联合类型使用 `|`分隔每个类型。

这里的 `let myFavoriteNumber: string | number`的含义是，允许 `myFavoriteNumber`的类型是 `string`或者 `number`，但是不能是其他类型。

## 对象类型

```ts
let person :object = { name:'Tom', age:18 }
```

我们可以使用object来定义对象类型，但在实际编码中对于上述例子，我们通常使用接口（interface）来定义对象类型

### 什么是接口

>在面向对象语言中，接口（Interfaces）是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类（classes）去实现（implement）。
>
>TypeScript 中的接口是一个非常灵活的概念，除了可用于对类的一部分行为进行抽象以外，也常用于对「对象的形状（Shape）」进行描述。

```ts
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
};
```

对于上述接口，下面两个例子中的多属性或者少属性都是不被允许的。

```ts
let tom: Person = {
    name: 'Tom'
};
let tom: Person = {
    name: 'Tom'，
    age: 25，
    sex: 'male'
};
```

### 可选属性

有时我们希望不要完全匹配一个形状，那么可以用可选属性，使用？来表示，可选属性是可以缺少的

```ts
interface Person {
    name: string;
    age?: number;
}
let tom: Person = {
    name: 'Tom'
};
```

### 任意属性

有时候我们希望一个接口允许有任意的属性，可以使用如下方式：

```ts
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};
```

### 只读属性

有时候我们希望对象中的一些字段只能在创建的时候被赋值，那么可以用 `readonly`定义只读属性：

```ts
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}
```

##数组类型

在 TypeScript 中，数组类型有多种定义方式，比较灵活。

### 「类型 + 方括号」表示法

数组中不允许出现其他类型的元素

```ts
let fibonacci: number[] = [1, 1, 2, 3, 5];
```

### 数组泛型

我们也可以使用数组泛型（Array Generic） `Array<elemType>`来表示数组：

```ts
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

## 函数的类型

一个函数有输入和输出，要在 TypeScript 中对其进行约束，需要把输入和输出都考虑到，其中函数声明的类型定义较简单：

```ts
function sum(x: number, y: number): number {
    return x + y;
}
```

### 可选参数

与接口中的可选属性类似，我们用 `?`表示可选的参数：

```ts
function sum(x: number, y ?: number): number {
    if(y){
      return x + y;
    }
    return x
}
```

### 参数默认值

在 ES6 中，我们允许给函数的参数添加默认值，**TypeScript 会将添加了默认值的参数识别为可选参数**：

```ts
function sum(x: number, y : number = 2): number {
      return x + y;
}
```

### 剩余参数

ES6 中，可以使用 `...rest`的方式获取函数中的剩余参数（rest 参数）：

```ts
function push(array: any[], ...items: any[]) {
    items.forEach(function(item) {
        array.push(item);
    });
}

let a = [];
push(a, 1, 2, 3);
```

## 类型断言

当「类型推断」无法判定类型的时候，需要利用「类型断言」来告诉编译器对象的类型。

对于类型断言，推荐使用：as。而不是在对象前使用<>，这和 jsx 语法有冲突。

```ts
interface LogInfo {
  time: Date;
  info: string;
  level?: "log" | "error" | "warning";
}

const obj1: LogInfo = {
  time: new Date(),
  info: "obj1"
};

const obj2 = {};

const logInfo = process.env.NODE_ENV === "development" ? obj2 : obj1;

// console.log(logInfo.info) // error: 编译报错
console.log((logInfo as LogInfo).info); // 类型断言，指明接口类型为：LogInfo
```

### 元组

数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象。

元组起源于函数编程语言（如 F#），这些语言中会频繁使用元组。

定义一对值分别为 `string`和 `number`的元组：

```ts
let tom: [string, number] = ['Tom', 25];
```

### 枚举

枚举（Enum）类型用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。

枚举使用 `enum`关键字来定义：

```ts
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};
```

### 泛型

泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。

```ts
function createArray(length: number, value: any): Array<any> {
    let result = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}

createArray(3, 'x'); // ['x', 'x', 'x']
```

这段代码编译不会报错，但是一个显而易见的缺陷是，它并没有准确的定义返回值的类型：

`Array<any>`允许数组的每一项都为任意类型。但是我们预期的是，数组中每一项都应该是输入的 `value`的类型。

这时候，泛型就派上用场了：

```ts
function createArray<T>(length: number, value: T): Array<T> {
    let result: T[] = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}
createArray<string>(3, 'x'); // ['x', 'x', 'x']
```

上例中，我们在函数名后添加了 `<T>`，其中 `T`用来指代任意输入的类型，在后面的输入 `value: T`和输出 `Array<T>`中即可使用了。

#### 泛型约束

在函数内部使用泛型变量的时候，由于事先不知道它是哪种类型，所以不能随意的操作它的属性或方法：

```ts
function loggingIdentity<T>(arg: T): T {
    console.log(arg.length);
    return arg;
}
// index.ts(2,19): error TS2339: Property 'length' does not exist on type 'T'.
```

上例中，泛型 `T`不一定包含属性 `length`，所以编译的时候报错了。

这时，我们可以对泛型进行约束，只允许这个函数传入那些包含 `length`属性的变量。这就是泛型约束：

```ts
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);
    return arg;
}
```

上例中，我们使用了 `extends`约束了泛型 `T`必须符合接口 `Lengthwise`的形状，也就是必须包含 `length`属性。