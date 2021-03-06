### Boolean
```typescript
let isDone: boolean = false;
```
### Number
```typescript
let decimal: number = 1;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```
### String
```typescript
let color: string = 'blue';

let age: number = 37;
let sentence: string = `He is ${age} years old`;
```
### Array
```typescript
let list: number[] = [1, 2, 3];
let list1: Array<number> = [1, 2, 3];
```
### Tuple
```typescript
let x: [string, number];
x = ['1', 1]; // ok
x = [1, '1']; // error
```
### Enum
```typescript
enum Color {
  Red,
  Green,
  Blue
}

let c: Color = Color.Green;
```
### unknown
```typescript
let notSure: unknown = 4;
notSure = "maybe a string insetead";
notSure = false;
```
### Any
`any`和`unknown`的区别在于，`any`既是`top type`，又是`bottom type`，而`unknown`只是`top type`。
```typescript
declare function getValue(key: string): any;
const str: string = getValue('myString');
```
### Void
```typescript
function warnUser(): void {
  console.log("This is my warning message")
}

let unusable: void = undefined;
// Ok if `--strictNullChecks` is not given
unusable = null;
```
### null和undefined
在`typescript`中，`null`和`undefined`有它们自己的类型。同时，`null`和`undefined`默认是其它类型的子类，也就是说它们可以赋给其它类型。但是在`strictNullChecks`模式下，它们仅能赋给`unknown`和`any`。
```typescript
let u: undefined = undefined;
let n: null = null;
```
### Never
抛出异常或者永不为真。`never`类型是任何类型的子类，可以赋值给任意类型。但是不是任何类型的子类，甚至`any`都不能赋值给`never`。
```typescript
function error(message: string): never {
  throw new Error(message)
}

function fail() {
  return error("Something failed")
}

function infiniteLoop(): never {
  while(true){}
}
```
### Object
不包含原始类型。(not include number、string、boolean、bigint、symbol、null、undefined)
### type assertions（类型断言）
两种格式
```typescript
let someValue: unknown = "this is a string";
let strLen: number = (someValue as string).length;

let someValue: unknown = "this is a string";
let strLen: number = (<string>someValue).length;
```