#### JavaScript如何创建对象？
    ```html
    // 字面量创建对象
    var o1 = {name = "o1"};
    var o2 = new Object({name : "o2"});
    ------------------------------------------
    // 构造函数创建对象
    var M = function () {
        this.name = "o3";
    }
    var o3 = new M();
    ------------------------------------------
    // Object.create创建对象
    var p = {name : 'o4'};
    var o4 = Object.create(p);

    ```
#### 原型、构造函数、实例、原型链的关系
    1. JavaScript中的继承是通过原型链体现的
    2. 每个实例都有一个__pto__属性，指向构造函数的prototype
    3. 访问一个对象的属性时，先在基本属性中查找，如果没有，在沿着__proto__这条链向上查找
    > 可通过hasOwnProperty方法来判断一个属性是否从原型链中继承而来
#### instanceof的原理是怎样的？
    instanceof是原型链继承中的重要环节，对instanceof的理解有利于理解原型链继承的机制
    以A instanceof B 为例
        1. instanceof的普通用法，检测B.prototype是否存在于参数A的原型链上
        2. 继承中判断实例是否属于他的父类
    简单理解就是沿着A的__proto__跟B的prototype寻找，如果能找到同一引用，返回true，否则返回false
    以下是一些示例
    ```js
        // 由于函数也是对象，对象是函数创建的，所以有：
        fn.__proto__ === Function.prototype
        Object.__proto__ === Function.prototype
        ------------------------------------------
        // Function是自身创建的，所以有：
        Function.__proto__ === Function.prototype
        ------------------------------------------
        // Function.prototype也是对象，所以有：
        Function.prototype.__proto__ === Object.prototype
        ------------------------------------------
        function Person() {}
        console.log(Object instanceof Object);     //true

        //第一个Object的原型链：Object=>Object.__proto__ => Function.prototype=>Function.prototype.__proto__=>Object.prototype
        //第二个Object的原型：Object=> Object.prototype

        console.log(Function instanceof Function); //true
        //第一个Function的原型链：Function=>Function.__proto__ => Function.prototype
        //第二个Function的原型：Function=>Function.prototype

        console.log(Function instanceof Object);   //true
        //Function=>
        //Function.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
        //Object => Object.prototype

        console.log(Person instanceof Function);      //true
        //Person=>Person.__proto__=>Function.prototype
        //Function=>Function.prototype

        console.log(String instanceof String);   //false
        //第一个String的原型链：String=>
        //String.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
        //第二个String的原型链：String=>String.prototype

        console.log(Boolean instanceof Boolean); //false
        //第一个Boolean的原型链：
        Boolean=>Boolean.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
        //第二个Boolean的原型链：Boolean=>Boolean.prototype

        console.log(Person instanceof Person); //false
        //第一个Person的原型链：
        Person=>Person.__proto__=>Function.prototype=>Function.prototype.__proto__=>Object.prototype
        //第二个Person的原型链：Person=>Person.prototype

    ```
#### new 运算符的实现机制
   ```js
        var new2 = function (func) {
            var o = Object.create(func.prototype);
            var k = func.call(o);
            if (typeof k === 'object') {
                return k;
            } else {
                return o;
            }
        }

   ```
   1. 创建一个新对象，继承自func.prototype
   2. 执行构造函数，this会指向新创建的对象
   3. 如果构造函数返回一个对象，则该对象便是new出来的结果，如果构造函数没有返回对象，那么new出来的结果为步骤1创建的对象。