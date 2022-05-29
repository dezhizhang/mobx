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