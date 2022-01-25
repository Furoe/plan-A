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
#### Partial
将第一层转换成可选
```ts
type Partial<T> = {
  [P in keyof T]+?: T[P];
}

interface UserInfo = {
  id: string;
  name: string;
}

type NewUserInfo = Partial<UserInfo>;
// type NewUserInfo = {
//   id?: string;
//   name?: string;
// }

// 深层转换
type DeepPartial<T> = {
  [ U in keyof T]?: T[U] extends object ? DeepPartial<T[U]> : T[U];
}
```
#### Required
将属性转换成必填
```ts
type Required<T> = {
  [U in keyof T]-?: T[U];
}
```
#### Readonly
```ts
type Readonly<T> = readonly [U in keyof T]: T[U];

```
#### Pick
从某个类型中挑选一些属性
```ts
type Pick<T, K extends keyof T> = [P in K]: T[P];

```
#### Record
将K中所有属性值转为T
```ts
type Record<K extends keyof any, T> = [P in K]: T;
```
#### Exclude
将某个类型中属于另一个类型的属性移除
```ts
type Exclude<T, U> = T extends U ? never : T;

// examples
type T0 = Exclude<'a' | 'b' | 'c', 'a'>; // 'b' | 'c'
type T1 = Exclude<string | number | (() => void), Function>; // string | number
```
#### Extract
从T中提取U
```ts
type Extract<T, U> = T extends U ? T : never;

// examples
type T0 = Extract<'a' | 'b' | 'c', 'a' | 'f'>; // 'a'
```
#### Omit
排除T中K属性
```ts
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
```
#### NonNullable
过滤类型中的null和undefined
```ts
type NonNullable<T> = T extends null | undefined ? never : T;
```