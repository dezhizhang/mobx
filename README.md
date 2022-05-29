# mobx
```js
@testable
class Person{

}

function testable(target:Person) {
  target.testable = true;
}

console.log(Person.testable)
```
# 装饰器
```js
function logger(target:any,key:string,descriptor:any) {
  let oldValue = descriptor.value;
  descriptor.value = function() {
    console.log(`${key}函数${Array.from(arguments)}`)
    return oldValue.apply(this,arguments);
  }
}


class Calculator {
  @logger
  add(a: number, b: number) {
    return a + b
  }
}

const c1 = new Calculator();
console.log(c1.add(1, 2));
```
### proxy代理
```js
let obj = {
  name:'小明',
  age:22,
}

const p1 = new Proxy(obj,{
  get:(target,key:string) => {
    console.log(`get ${key}`)
    return Reflect.get(target,key);
  },
  set:(target,key:string,value:any) => {
    console.log(`set ${key}:${value}`);
    return Reflect.set(target,key,value);
  }
});

console.log(p1.name,p1.age);

p1.age = 10;
```