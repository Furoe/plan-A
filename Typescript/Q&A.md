### Q&A1
#### Q1
```ts
type User = {
  id: number;
  kind: string;
}

function makeCustomer<T extends User>(u:T):T{
  return {
    id: u.id,
    kind: 'customer'
  }
}
```
#### A1
```ts
// example1
type User = {
  id: number;
  kind: string
}
function makeCustomer<T extends User>(u:T):T{
  return {
    ...u,
    id: u.id,
    kind: 'customer'
  }
}

// example2
function makeCustomer<T extends User>(u:T){
  return{
    id: u.id,
    kind: 'customer'
  }
}

// 思路：第一种是将u所拥有的额外属性补充完毕，第二种是让ts自己去推断返回类型，还有其它的解决方案，例如直接将返回类型设为
// User，或者return加上类型断言
```