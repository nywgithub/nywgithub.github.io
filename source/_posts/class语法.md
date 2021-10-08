---
title: class语法
date: 2021-09-28 14:11:20
tags:
---

- **常规写法**
```javascript
class MyClass {
  prop = value; // 属性

  constructor(...) { // 构造器
    // ...
  }

  method(...) {} // method

  get something(...) {} // getter 方法
  set something(...) {} // setter 方法

  [Symbol.iterator]() {} // 有计算名称（computed name）的方法（此处为 symbol）
  // ...
}
```

- **继承**
extends关键字
```javascript
class parent{
    constructor(name){
        this.name = name
    }
    sayHi(){
        console.log('hi')
    }
}

class user extends parent {
    constructor(name,age){
        //继承父类constructor
        super()
        this.age = age
    }

    sayHi(){
        //如果需要在父类基础上新增功能
        super.sayHi()
        alert('hi user')

        //如果完全重写
        alert('hi user')
    }
}
```

- **静态属性和静态方法**
```javascript
class User {
  //静态方法用于实现属于该类但不属于该类任何特定对象的函数。
  static staticMethod() {
    alert(this === User);
  }
  static name = 'nyw'
}

User.staticMethod(); // true
```
静态属性和方法是可被继承的。

- **instanceof**
语法
```javascript
 obj instanceof Class
```javascript
