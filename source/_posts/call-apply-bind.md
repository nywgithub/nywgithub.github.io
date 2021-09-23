---
title: 'call,apply和bind'
date: 2021-09-23 21:01:37
tags:
---

- call,apply改变函数的this指向,重新定义函数的执行环境，并直接执行函数
    call:func.call(context, arg1, arg2, ...),多个参数依次排列
    apply:func.apply(context, arguments)，多个参数写成数组的展开形式
    context是上下文环境，函数的this将指向context
    如果call和apply的第一个参数是null，this指向window

- bind不会直接执行函数，会返回一个改变this指向后的boundfounction
- 用法
    1. call和apply是为了动态改变this而出现的，当一个object没有某个方法，但是其他的有，我们可以借助call或apply用其它对象的方法来操作。
    ``` 
        ;(function(){
            function cat(){
            }
            cat.prototype={
                food:"fish",     
                say: function(){
                    alert("I love "+this.food);
                }
            }
            var blackCat = new cat;
            blackCat.say();
        })()
    ```
    如果此时有一个whitedog = {food:"bone"}
    也需要调用say()方法，可以用call和apply实现：
    blackCat.say.call(whiteDog)。

    2. Array.prototype.slice.call(arguments)
    用的比较多的，通过document.getElementsByTagName选择的dom 节点是一种类似array的array。它不能应用Array下的push,pop等方法。我们可以通过：
    ```    
        var domNodes =  Array.prototype.slice.call(document.getElementsByTagName("*"));
    ```
    这样domNodes就可以应用Array下的所有方法了。

    3. 实现js继承
    
    ```
        //父类
        function Person(name, height) {
            this.sayInfo = function() {
                return "姓名：" + name + ", 身高：" + height + ", 体重：" + this.weight;
            }
        }
        //子类
        function Chinese(name, height, weight) {
            Person.call(this, name, height);
            this.weight = weight;
            
            this.nation = function() {
                console.log("我是中国人");
            }
        }
        //子类
        function America(name, height, weight) {
            Person.apply(this, [name, height]);
            this.weight = weight;
        }

        let chiness = new Chinese("成龙", "178cm", "60kg");
        console.log(chiness.sayInfo());    //姓名：成龙, 身高：178cm, 体重：60kg
        let america = new America("jack", "180cm", "55kg");
        console.log(america.sayInfo());    //姓名：jack, 身高：180cm, 体重：55kg
    ```