---
title: js继承的6种方式
date: 2021-09-25 14:12:36
tags:
---
# 先定义一个公共父类
```javascript
function person(name){
    this.name = name
    this.sum = function(){
        console.log(this.name)
    }
}
```
- **原型链继承**
原理：让新实例的原型等于父类的实例
```javascript
person.prototype.age = 10
var p = new person()
//新类
function animal(){
    this.type = 'tiger'
}
animal.prototype = new person()
var cat = new animal()
console.log(cat.age) // 10
```
特点：
1、实例可继承的属性有：实例的构造函数的属性，父类构造函数属性，父类原型的属性。（新实例不会继承父类实例的属性！）
缺点：
1、新实例无法向父类构造函数传参。
2、继承单一。
3、所有新实例都会共享父类实例的属性。（原型上的属性是共享的，一个实例修改了原型属性，另一个实例的原型属性也会被修改！）

- **call和apply**
原理：用call，apply将父类构造函数引入子类函数
```javascript
function con(){
    person.call(this,"con")
    this.age = 12
}
var con1 = new con()
```
特点：
1、只继承了父类构造函数的属性，没有继承父类原型的属性。
2、解决了原型链继承缺点
3、可以继承多个构造函数属性（call多个）。
4、在子实例中可向父实例传参。
缺点：
1、只能继承父类构造函数的属性。
2、无法实现构造函数的复用。（每次用每次都要重新调用）
3、每个新实例都有父类构造函数的副本，臃肿。

- **组合继承（结合上面两种）（常用）**
```javascript
function plane(name){
    person.call(this,name)
}
plane.prototype = new person()
```
特点：
1、可以继承父类原型上的属性，可以传参，可复用。
2、每个新实例引入的构造函数属性是私有的。
缺点：
调用了两次父类构造函数（耗内存），子类的构造函数会代替原型上的那个父类构造函数。

- **原型式继承**
```javascript
function content(obj){
    function fn(){}
    fn.prototype = obj
    return new fn()
}
var personer = new person()
var personera = content(personer)
console.log(personera.age) //10
```
特点：类似于复制一个对象，用函数来包装。
缺点：
1、所有实例都会继承原型上的属性。
2、无法实现复用。（新实例属性都是后面添加的）
3、无法传入属性

- **寄生式继承**
```JavaScript
function content(obj){
    function fn(){}
    fn.prototype = obj
    return new fn()
}
var a = new person()
function subcontent(obj){
    var b = new person()
    b.name = "leo"
    return b
}
var c = subcontent(a)
console.log(c.name) //leo
```

- **寄生组合式继承**
```javascript
function content(obj){
    function fn(){}
    fn.prototype = obj
    return new fn()
}
var con = content(person.prototype)

function Sub(){
    person.call(this)
}
Sub.prototype  = con
con.constructor = Sub
var sub1 = new Sub()
console.log(sub1.age)
```
- **ES6class继承**
```javascript
//class 相当于es5中构造函数
//class中定义方法时，前后不能加function，全部定义在class的protopyte属性中
//class中定义的所有方法是不可枚举的
//class中只能定义方法，不能定义对象，变量等
//class和方法内默认都是严格模式
//es5中constructor为隐式属性
class People{
  constructor(name='wang',age='27'){
    this.name = name;
    this.age = age;
  }
  eat(){
    console.log(`${this.name} ${this.age} eat food`)
  }
}
//继承父类
class Woman extends People{ 
   constructor(name = 'ren',age = '27'){ 
     //继承父类属性
     super(name, age); 
   } 
    eat(){ 
     //继承父类方法
      super.eat() 
    } 
} 
let wonmanObj=new Woman('xiaoxiami'); 
wonmanObj.eat();
```
