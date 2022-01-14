#### 泛型
```ts
function indentity<T>(value: T):T{
  return value
}
```
#### 泛型约束
```ts
interface sizeable{
  size: number
}
function trace<T extends sizeable>(value: T) : T{
  console.log(value.size)
  return value
}
```