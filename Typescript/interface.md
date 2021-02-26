### interface
接口时一种具有结构的子类。
```typescript
interface LabeledValue {
  label: string;
}

function printLabel(labeledObj: LabeledValue) {
  console.log(labeledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" }
printLabel(myObj)
```
#### Optional Properties
接口不是所有属性都是必须的。
```typescript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): {color: string, area: number} {
  let newSquare = {color: "white", area: 100}
  if(config.color){
    newSquare.color = config.color;
  }
  if(config.width){
    newSquare.area = config.width * config.width;
  }

  return newSquare;
}

let mySquare = createSquare({color: "black"});
```
#### Readonly properties
某些属性只能在创建时进行修改。
```typescript
interface Point {
  readonly x: number;
  readonly y: number;
}

let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error
```
##### ReadonlyArray
```typescript
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;

ro[0] = 12; // error
ro.push(5); // error
ro.length = 100; /// error
a = ro; // error
```
只读数组类型不能修改，也不能直接赋值给一般的数组，但是可以使用类型断言。
```typescript
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
a = ro as number[];
```
#### Function Types
```typescript
interface SearchFunc {
  (source: string, subString: string): boolean;
}

let mySearch: SearchFunc = function(src: string, sub: string): boolean {
  let result = src.search(sub);
  return result > -1;
}
```
#### Indexable Types
```typescript
interface stringArray {
  [index: number]: string;
}

let myArray: stringArray;
myArray = ["Bob", "Fred"];
let myStr: string = myArray[0];
```
#### Class Types
```typescript
interface ClockInterface {
  currentTime: Date;
  setTime(d: Date): void;
}

class Clock implements ClockInterface {
  currentTime: Date = new Date();
  setTime(d: Date) {
    this.currentTime = d;
  }
  constructor(h: number, m: number) {}
}
```
####