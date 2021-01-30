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
#
#
