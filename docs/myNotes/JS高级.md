# JavaScript高级



## 1 基础总结深入

### 1.1数据类型

![image-20220310192235045](JS%E9%AB%98%E7%BA%A7.assets/image-20220310192235045.png)

#### 1.1.1 分类和判断

* 基本(值)类型

  * Number ----- 任意数值 -------- typeof
  * String ----- 任意字符串 ------ typeof
  * Boolean ---- true/false ----- typeof
  * undefined --- undefined ----- typeof/===
  * null -------- null ---------- ===

* ```javascript
  // typeof: 返回的是数据类型的字符串表达形式
  //1. 基本类型
  var a
      console.log(a, typeof a, a === undefined) // undefined 'undefined' true
      console.log(a === typeof a) // false
  
      a = 3
      console.log(typeof a === 'number') //true
      a = 'atguigu'
      console.log(typeof a === 'string') //string是小写 true
      a = true
      console.log(typeof a === 'boolean') // true
  
      a = null
      console.log(a === null) // true
      console.log(typeof a) // 'object'
  
          
  ```

  总结：

  - typeof：

    可以区别: 数值, 字符串, 布尔值, undefined, function。

    不能区别: null与对象, 一般对象与数组。

  - instanceof：

    专门用来判断对象数据的类型: Object, Array与Function

    * ===

      可以判断: undefined和null

* 对象(引用)类型

  * Object -----任意对象-------- typeof/instanceof
  * Array ------ 一种特别的对象（数值下标，内部数据是有序的）-------instanceof
  * Function ---- 一种特别的对象（可以执行）-------- typeof

- ```javascript
  //2. 对象类型
      var b1 = {
        b2: [2, 'abc', console.log],
        b3: function () {
          console.log('b3()')
        }
      }
      console.log(b1 instanceof Object, typeof b1) // true 'object'
      console.log(b1.b2 instanceof Array, typeof b1.b2) // true 'object'
      console.log(b1.b3 instanceof Function, b1.b3 instanceof Object, typeof b1.b3) // true true 'function'
  
      console.log(typeof b1.b2[2]) // 'function'，既然是函数就可以调用
      console.log(b1.b2[2]('abc')) // 'abc' undefined
  
  
  ```

#### 1.1.2 相关问题

1. undefined与null的区别?

     * undefined代表定义未赋值
     * null代表赋值了, 只是值为null
2. 什么时候给变量赋值为null呢?

     * var a = null //a将指向一个对象, 但对象此时还没有确定
     * a = null //让a指向的对象成为垃圾对象
3. 严格区别变量类型与数据类型?

     * js的变量本身是没有类型的, 变量的类型实际上是变量内存中数据的类型

     * 数据类型:
       * 基本类型: 保存基本类型数据的变量
       * 对象类型: 保存对象地址值的变量

     * 变量类型（变量内存值的类型）
       * 基本类型：保存的就是基本类型的数据
       * 引用类型：保存的就是地址值
```html
<body>
  <script type="text/javascript">
    //实例对象
    //类型对象
    function Person(name, age) { //构造函数  类型（构造函数也是函数，函数是对象）
      this.name = name
      this.age = age
    }
    var p = new Person() //根据类型创建的实例对象

    // Person('jack', 12) //语法上合法，但是一般不这么做，因为Person是用来当作构造函数的

    // 1. undefined与null的区别?
    var a1
    var a2 = null
    console.log(a1, a2) //undefined  null

    // 2. 什么时候给变量赋值为null呢?
    //初始
    var a3 = null
    //中间
    var name = 'Tom'
    var age = 12
    a3 = {
      name: name,
      age: age
    }
    //结束
    a3 = null  //让a3指向的对象成为垃圾对象（被垃圾回收器回收）
      
    var c = function () { //c里面存的是地址值

    }
    console.log(typeof c); //'function'
  </script>
</body>
```



### 1.2 数据变量与内存

![image-20220310203910412](JS%E9%AB%98%E7%BA%A7.assets/image-20220310203910412.png)

#### 1.2.1 概念及关系

1. 什么是数据?

     * 存储于内存中代表特定信息的'东东', 本质就是0101二进制
     * 具有可读和可传递的基本特性
     * 万物(一切)皆数据, 函数也是数据
     * 程序中所有操作的目标: 数据
       * 算术运算
       * 逻辑运算
       * 赋值
       * 调用函数传参
       ...

2. 什么是内存?

     * 内存条通电后产生的存储空间(临时的)
     * 产生和死亡: 内存条(集成电路板)==>通电==>产生一定容量的存储空间==>存储各种数据==>断电==>内存全部消失
     * 内存的空间是临时的, 而硬盘的空间是持久的
     * 一块内存包含2个数据
       * 内部存储的数据(一般数据/地址数据)
       * 内存地址值数据
     * 内存分类
       * 栈: 全局变量, 局部变量 (空间较小)
       * 堆: 对象 (空间较大)
3. 什么是变量?

     * 值可以变化的量, 由变量名与变量值组成
     * 一个变量对应一块小内存, 变量名用来查找到内存, 变量值就是内存中保存的内容
4. 内存,数据, 变量三者之间的关系

     * 内存是一个容器, 用来存储程序运行需要操作的数据

     * 变量是内存的标识, 我们通过变量找到对应的内存, 进而操作(读/写)内存中的数据

#### 1.2.2 相关问题

- 问题: var a = xxx, a内存中到底保存的是什么?

  xxx是一个基本数据,保存的就是这个数据；

  xxx是一个对象，保存的是对象的地址值；

  xxx是一个变量，保存的是xxx的内容（可能是基本数据，也可能是地址值）

- 关于引用变量赋值问题

   2个引用变量指向同一个对象, 通过一个引用变量修改对象内部数据, 另一个引用变量也看得见

   2个引用变量指向同一个对象,让一个引用变量指向另一个对象, 另一个引用变量还是指向原来的对象

  ```html
  <script type="text/javascript">
  
    //1. 2个引用变量指向同一个对象, 通过一个引用变量修改对象内部数据, 另一个引用变量也看得见
    var obj1 = {}
    var obj2 = obj1
    obj2.name = 'Tom'
    console.log(obj1.name)  //Tom
    function f1(obj) {
      obj.age = 12
    }
    f1(obj2)  
    console.log(obj1.age)  //12
  
    //2. 2个引用变量指向同一个对象,让一个引用变量指向另一个对象, 另一个引用变量还是指向原来的对象
    var obj3 = {name: 'Tom'}
    var obj4 = obj3
    obj3 = {name: 'JACK'}
    console.log(obj4.name)  //Tom
    function f2(obj) {
      obj = {name: 'Bob'}
    }
    f2(obj4)
    console.log(obj4.name)  //Tom
  
  </script>
  ```

- 问题: 在js调用函数时传递变量参数时, 是值传递还是引用传递

  理解1： 只有值传递, 没有引用传递, 传递的都是变量的值, 只是这个值可能是基本数据, 也可能是地址(引用)数据。

  理解2： 如果后一种看成是引用传递, 那就值传递和引用传递都可以有。

- 问题: JS引擎如何管理内存?

    1. 内存生命周期
         1). 分配需要的内存，得到它的使用权
         2). 存储数据，可以反复进行操作
         3). 不需要时将其释放/归还

    2. 释放内存

       局部变量：函数执行完自动释放

       存储对象的堆空间内存: 当内存没有引用指向时, 对象成为垃圾对象, 垃圾回收器后面就会回收释放此内存

  ```html
  <script type="text/javascript">
      var a = 3
      var obj = {}
      obj = undefined // 没有释放空间
  
      function fn() {
        var a = 3
        var b = {}
      }
      fn() // a是自动释放,b所指向的对象是在后面的某个时刻由垃圾回收器回收释放空间
    </script>
  ```

  

### 1.3 对象

![image-20220310213801653](JS%E9%AB%98%E7%BA%A7.assets/image-20220310213801653.png)

#### 1.3.1 对象概念

1. 什么是对象?

     * 代表现实中的某个事物, 是该事物在编程中的抽象
     * 多个数据的集合体(封装体)
     * 用于保存多个数据的容器
2. 为什么要用对象?
     * 便于对多个数据进行统一管理
3. 对象的组成

     * 属性
       * 代表现实事物的状态数据
       * 由属性名和属性值组成
       * 属性名都是字符串类型, 属性值是任意类型
     * 方法
       * 代表现实事物的行为数据
       * 是特别的属性==>属性值是函数
4. 如何访问对象内部数据?

     * .属性名: 编码简单, 但有时不能用

     * \['属性名']: 编码麻烦, 但通用

   ```html
   <script type="text/javascript">
     // 创建对象
     var p = {
       name: 'Tom',
       age: 12,
       setName: function (name) {
         this.name = name
       },
       setAge: function (age) {
         this.age = age
       }
     }
   
     // 访问对象内部数据
     console.log(p.name, p['age'])
     p.setName('Jack')
     p['age'](23)
     console.log(p['name'], p.age)
   
   </script>
   ```

   

#### 13.2 相关问题

- 问题: 什么时候必须使用['属性名']的方式?

  属性名不是合法的标识名；(包含特殊字符：- 空格)

  变量名不确定；

  ```html
  <script type="text/javascript">
    // 创建对象
    var p = {}
  
  /*情形一: 属性名不是合法的标识名*/
    /*需求: 添加一个属性: content-type: text/json */
    //  p.content-type = 'text/json' //不正确
    p['content-type'] = 'text/json'
  
  /*情形二: 变量名不确定*/
    var propName = 'myAge'
    var value = 12
    // p.propName = value  //不正确
    p[prop] = value
    console.log(p['content-type'], p[prop])
  </script>
  
  ```

  ![image-20220310215045683](JS%E9%AB%98%E7%BA%A7.assets/image-20220310215045683.png)

### 1.4 函数

![image-20220310215125464](JS%E9%AB%98%E7%BA%A7.assets/image-20220310215125464.png)

#### 1.4.1函数概念相关

1. 什么是函数?

     * 具有特定功能的n条语句的封装体
     * 只有函数是可执行的, 其它类型的数据是不可执行的
     * 函数也是对象
2. 为什么要用函数?

     * 提高代码复用
     * 便于阅读和交流
3. 如何定义函数?

     * 函数声明
     * 表达式
4. 如何调用(执行)函数?

     * test()

     * new test()

     * obj.test()

     * test.call/apply(obj)   

```html
<script type="text/javascript">

  function f1 () { // 函数声明
    console.log('f1()')
  }
  var f2 = function () { // 表达式
    console.log('f2()')
  }
  
   var obj = {}
   function test2() {
     this.xxx = 'chengzi'
     console.log(6666666);
   }
    // obj.test2() //不能直接调用，根本就没有
   test2.call(obj) //obj.test2()  可以让一个函数成为指定任意对象的方法进行调用
   console.log(obj.xxx);

  
  /*
   函数也是对象
   */
  function fn() {

  }
  console.log(fn instanceof Object) // 是Object类型的实例
  console.log(fn.prototype) // 内部有属性
  console.log(fn.call) // 内部有方法
  fn.t1 = 'atguigu' // 可以添加属性
  fn.t2 = function () { // 可以添加方法
    console.log('t2() '+this.t1)
  }
  fn.t2()
</script>
```

#### 1.4.2 回调函数

1. 什么函数才是回调函数?

     * 你定义的
     * 你没有直接调用
     * 但最终它执行了(在特定条件或时刻)
2. 常见的回调函数?

     * DOM事件函数：（this是发生事件的dom元素）
     * 定时器函数：（this是window）
     *  ajax回调函数(与后台交互)
     * 生命周期回调函数(后面学)

```html
 <script type="text/javascript">
    //1. DOM事件函数
    var btn = document.getElementById('btn')
    btn.onclick = function () { //dom事件回调函数
      alert(this.innerHTML)
    }

    //2. 定时器函数
    //超时定时器
    setTimeout(function () {
      alert('到点了')
    }, 2000)
    //循环定时器
    setInterval(function () {
      alert('到点啦!')
    }, 2000)
  </script>
```



#### 1.4.3 IIFE

1. 理解

     * 全称: Immediately-Invoked Function Expression 立即调用函数表达式
     * 别名: 匿名函数自调用
2. 作用

     * 隐藏内部实现

     * 不污染外部命名空间
     * 用它来编码js模块

```html
<script type="text/javascript">
    (function () { //匿名函数自调用
      var a = 3
      console.log(a + 3); //6
    })()
    var a = 4
    console.log(a); //4


    (function () {
      var a = 1

      function test() {
        console.log(++a)
      }
      window.$ = function () { //向外暴露一个全局函数
        return {
          test: test
        }
      }
    })()

    $().test() //$是一个函数；$执行后返回的是一个对象

  </script>
```



#### 1.4.4 函数中的this

1. this是什么?

     * 所有函数内部都有一个变量this
     * 任何函数本质上都是通过某个对象来调用的，如果没有直接指定就是window

     * this代表调用函数的当前对象
     * 在定义函数时, this还没有确定, 只有在执行时才动态确定(绑定)的
2. 如何确定this的值?

     * test()：window

     * obj.test()：obj

     * new test()：新创建的对象

     * test.call(obj)：obj

```html
<script type="text/javascript">
    function Person(color) {
      console.log(this)
      this.color = color;
      this.getColor = function () {
        console.log(this)
        return this.color;
      };
      this.setColor = function (color) {
        console.log(this)
        this.color = color;
      };
    }

    Person("red"); //this是谁? window

    var p = new Person("yello"); //this是谁?  p

    p.getColor(); //this是谁?  p

    var obj = {};
    p.setColor.call(obj, "black"); //this是谁? obj

    var test = p.setColor;
    test(); //this是谁? window

    function fun1() {
      function fun2() {
        console.log(this);
      }

      fun2(); //this是谁? window
    }
    fun1();
  </script>
```



## 2 函数高级

### 2.1 原型与原型链

![image-20220311095924091](JS%E9%AB%98%E7%BA%A7.assets/image-20220311095924091.png)

前提：要明白的概念。

四个概念：

- js分为函数对象和普通对象，每个对象都有\__proto__属性，但是**只有函数对象才有prototype属性**。
- Object、Function都是js内置的函数，类似的还有我们常用到的Array、RegExp、Data、Boolean、Number、String.
- 属性\__proto\_\_是一个对象，他有两个属性，constructor 和\__proto\_\_。
- 原型对象prototype有一个默认的constructor属性，用于记录实例是由哪个构造函数创建。

两个准则：

```javascript
1. Person.prototype.constructor == Person // **准则1：原型对象（即Person.prototype）的constructor指向构造函数本身**
2. person01.__proto__ == Person.prototype // **准则2：实例（即person01）的__proto__和原型对象指向同一个地方**
```



#### 2.1.1 原型（prototype）

1. 函数的prototype属性

     * 每个函数都有一个prototype属性, 它默认指向一个Object空对象(即称为: 原型对象)
     * 原型对象中有一个属性constructor, 它指向函数对象
     * 原型对象就相当于一个公共区域，所有同一类的实例对象都可以访问到这个原型对象，我们可以将对象中共有的内容，统一设置到对象中。
     * 当我们访问对象的一个属性或者方法时，它会先在对象自身中寻找，如果有则直接使用，如果没有则会去原型对象中寻找，如果找到则直接使用。
     * 以后创建构造函数时，可以将这些对象共有的属性和方法，同意添加到构造函数的原型对象中。这样不用分别为每一个对象添加，也不会影响到全局作用域，就可以使每个对象都具有这些属性和方法了。

2. 给原型对象添加属性(一般都是方法)
     * 作用: 函数的所有实例对象自动拥有原型中的属性(方法)

```html
<script type="text/javascript">
    // 每个函数都有一个prototype属性, 它默认指向一个对象(即称为: 原型对象)
    console.log(Date.prototype, typeof Date.prototype)

    function fn() {

    }


    fn.prototype.test = function () {
      console.log('test()');
    }

    console.log(fn.prototype, typeof fn.prototype) //默认指向一个Object空对象（即称为原型对象）
    // 原型对象中有一个属性constructor, 它指向函数对象
    console.log(Date.prototype.constructor === Date)
    console.log(fn.prototype.constructor === fn)


    // 2. 给原型对象添加属性(一般都是方法)，实例对象可以访问
    function F() {

    }
    F.prototype.age = 12 //添加属性
    F.prototype.setAge = function (age) { // 添加方法
      this.age = age
    }
    // 创建函数的实例对象
    var f = new F()
    console.log(f.age) //12
    f.setAge(23)
    console.log(f.age) //23
  </script>
```

#### 2.1.2 显式原型与隐式原型

1. 每个函数function都有一个prototype，即显式原型

2. 每个实例对象都有一个\__proto__，可称为隐式原型

3. 对象的隐式原型的值为其对应构造函数的显式原型的值

     

5. 总结:

     * 函数的prototype属性: 在定义函数时自动添加的, 默认值是一个空Object对象

     * 对象的\__proto__属性: 创建对象时自动添加的, 默认值为构造函数的prototype属性值

     * 程序员能直接操作显式原型, 但不能直接操作隐式原型(ES6之前)

![image-20220313163604967](JS%E9%AB%98%E7%BA%A7.assets/image-20220313163604967.png)

#### 2.1.3 原型链

![image-20220313163827618](JS%E9%AB%98%E7%BA%A7.assets/image-20220313163827618.png)

1. 原型链(图解)

     * 访问一个对象的属性时，
       * 先在自身属性中查找，找到返回
       * 如果没有, 再沿着__proto__这条链向上查找, 找到返回
       * 如果最终没找到, 返回undefined
     * 别名: 隐式原型链
     * 作用: 查找对象的属性(方法)
2. 构造函数/原型/实体对象的关系(图解)

   ![image-20220313164016125](JS%E9%AB%98%E7%BA%A7.assets/image-20220313164016125.png)

3. 构造函数/原型/实体对象的关系2(图解)

   ![image-20220313204113448](JS%E9%AB%98%E7%BA%A7.assets/image-20220313204113448.png)

4. 代码图解

![image-20220313163155031](JS%E9%AB%98%E7%BA%A7.assets/image-20220313163155031.png)

```html
<script type="text/javascript">
  function Fn() {
    this.test1 = function () {
      console.log('test1()')
    }
  }
// 函数的显式原型对象指向的对象默认是空Object实例对象（但是Object不满足）
    console.log(Fn.prototype instanceof Object); //true
    console.log(Object.prototype instanceof Object); //false
    console.log(Function.prototype instanceof Object); //true

    // 所有函数都是Function的实例（包括Function），Function是它自身的实例
    console.log(Function.__proto__ === Function.prototype); //true


    // Object的原型对象是原型链尽头
    console.log(Object.prototype.__proto__ === null); //true
  Fn.prototype.test2 = function () {
    console.log('test2()')
  }
  var fn = new Fn()

  fn.test1()  
  fn.test2()
  console.log(fn.toString())
  fn.test3()
</script>
```

5. 原型链属性问题

   读取对象的属性值时: 会自动到原型链中查找。

   设置对象的属性值时: 不会查找原型链, 如果当前对象中没有此属性, 直接添加此属性并设置其值。

   方法一般定义在原型中, 属性一般通过构造函数定义在对象本身上。

   ```html
   <script type="text/javascript">
       function Person(name, age) {
         this.name = name;
         this.age = age;
       }
       Person.prototype.setName = function (name) {
         this.name = name;
       }
       Person.prototype.sex = '男';
   
       var p1 = new Person('Tom', 12)
       p1.setName('Jack')
       console.log(p1.name, p1.age, p1.sex) //Jack  12 男
       p1.sex = '女'
       console.log(p1.name, p1.age, p1.sex) //Jack  12 女
   
       var p2 = new Person('Bob', 23)
       console.log(p2.name, p2.age, p2.sex) //Bob 23 男
     </script>
   ```

   

#### 2.1.4 探索instanceof

![image-20220313204331910](JS%E9%AB%98%E7%BA%A7.assets/image-20220313204331910.png)

1. instanceof是如何判断的?

   表达式: A instanceof B

   如果B函数的显式原型对象(prototype)在A对象的原型链(\__proto__)上, 返回true, 否则返回false。

2. Function是通过new自己产生的实例。

```javascript
  //案例1
    function Foo() {}
    var f1 = new Foo();
    console.log(f1 instanceof Foo); //true
    console.log(f1 instanceof Object); //true

    //案例2
    console.log(Object instanceof Function) //true
    console.log(Object instanceof Object) //true
    console.log(Function instanceof Object) //true
    console.log(Function instanceof Function) //true

    function Foo() {}
    console.log(Object instanceof Foo);   //false
```



#### 2.1.5 面试题

```javascript
 /*
  测试题1
   */
    var A = function () {

    }
    A.prototype.n = 1

    var b = new A()

    A.prototype = {
      n: 2,
      m: 3
    }

    var c = new A()
    console.log(b.n, b.m, c.n, c.m) //1,undefined,2,3


    /*
     测试题2
     */
    var F = function () {

    };
    Object.prototype.a = function () {
      console.log('a()')
    };
    Function.prototype.b = function () {
      console.log('b()')
    };
    var f = new F();
    f.a() //a()
    f.b() //报错
    F.a()  //a()
    F.b()  //b()
```



### 2.2 执行上下文与执行上下文栈

![image-20220314210217497](JS%E9%AB%98%E7%BA%A7.assets/image-20220314210217497.png)

#### 2.2.1 变量提升与函数提升

1. 变量声明提升

     * 在JS中，代码执行时是分两步走的，第一步：解析，第二步：一步一步的执行。那么变量提升就是变量声明会被提升到作用域的最顶上去，也就是该变量不管在作用域哪个地方声名的，都会提升到作用域的最顶上去。
     * 通过var定义(声明)的变量, 在定义语句之前就可以访问到
     * 值: undefined
2. 函数声明提升

     * 函数声名式，会将函数的声名和定义一起提升到作用域的最顶上去。
     * 通过function声明的函数, 在之前就可以直接调用
     * 值: 函数定义(对象)

```javascript
/*
   面试题: 输出什么?
   */
  var a = 4
  function fn () {
    console.log(a)
    var a = 5
  }
  fn()  //undifined


  /*变量提升*/
  console.log(a1) //可以访问, 但值是undefined
  /*函数提升*/
  a2() // 可以直接调用

  var a1 = 3
  function a2() {
    console.log('a2()')
  }
```

- 变量提升的例子(https://www.jb51.net/article/140720.htm)

  ```javascript
  
      console.log(a); //undefined
      var a = 'hello world'
      console.log(a); //hello world
  
      // 相当于以下写法
      // var a;
      // console.log(a); //undefined
      // a = 'hello world';
      // console.log(a); //hello world
  ```

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314113807290.png" alt="image-20220314113807290" style="zoom: 50%;" />

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314113823034.png" alt="image-20220314113823034" style="zoom:50%;" />

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314113843125.png" alt="image-20220314113843125" style="zoom:50%;" />

- 函数提升的例子

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314114157930.png" alt="image-20220314114157930" style="zoom:50%;" />

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314114222963.png" alt="image-20220314114222963" style="zoom: 50%;" />

  注意:函数声明式，会将函数的声明和定义一起提升到作用域的最顶上去。

  如果是这种写法:函数表达式声明的函数

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314114305339.png" alt="image-20220314114305339" style="zoom:33%;" />

  <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314114436325.png" alt="image-20220314114436325" style="zoom:50%;" />

总结：所有的声名都会提升到作用域的最顶上去；同一个变量只会声名一次，其他的会被忽略掉；函数声明的优先级高于变量声明的优先级，并且函数声名和函数定义的部分一起被提升。

#### 2.2.2 函数提升和变量提升的优先级

函数提升优先级高于变量提升，且不会被同名变量声明时覆盖，但是会被同名变量赋值后覆盖。

```JavaScript
     console.log(a) // ƒ a(){}  变量a赋值前打印的都会是函数a
     var a=1;
     function a(){}
     console.log(a) // 1    变量a赋值后打印的都会是变量a的值
相当于以下代码：
     function a(){}  // 函数声明提升 a-> f a (){}
     var a;        // 变量提升
     console.log(a)  // 此时变量a只是声明没有赋值所以不会覆盖函数a --> 输出函数a  f a (){}
     a=1;     //变量赋值
     console.log(a)  // 此时变量a赋值了 --> 输出变量a的值 1

```

```javascript
     a();  // 2
     var a = function(){  // 看成是一个函数赋值给变量a
        console.log(1)
     }
     a(); // 1
     function a(){
        console.log(2)
     }
     a(); // 1

```



#### 2.2.3 执行上下文

执行上下文总共有三种类型：

- **全局执行上下文：** 这是默认的、最基础的执行上下文。不在任何函数中的代码都位于全局执行上下文中。它做了两件事：1. 创建一个全局对象，在浏览器中这个全局对象就是 window 对象。2. 将 `this` 指针指向这个全局对象。一个程序中只能存在一个全局执行上下文。
- **函数执行上下文：** 每次调用函数时，都会为该函数创建一个新的执行上下文。每个函数都拥有自己的执行上下文，但是只有在函数被调用的时候才会被创建。一个程序中可以存在任意数量的函数执行上下文。每当一个新的执行上下文被创建，它都会按照特定的顺序执行一系列步骤，具体过程将在本文后面讨论。
- **Eval 函数执行上下文：** 运行在 `eval` 函数中的代码也获得了自己的执行上下文，但由于 Javascript 开发人员不常用 eval 函数，所以在这里不再讨论。

#### 2.2.4 执行上下文栈

1. 在全局代码执行前, JS引擎就会创建一个栈来存储管理所有的执行上下文对象

2. 在全局执行上下文(window)确定后, 将其添加到栈中(压栈)

3. 在函数执行上下文创建后, 将其添加到栈中(压栈)

4. 在当前函数执行完后,将栈顶的对象移除(出栈)

5. 当所有的代码执行完后, 栈中只剩下window

   ```javascript
   <script type="text/javascript">
                               //1. 进入全局执行上下文
     var a = 10
     var bar = function (x) {
       var b = 5
       foo(x + b)              //3. 进入foo执行上下文
     }
     var foo = function (y) {
       var c = 5
       console.log(a + c + y)
     }
     bar(10)                    //2. 进入bar函数执行上下文
   </script>
   ```

   ```html
   <body>
     <!--
   1. 依次输出什么?
   2. 整个过程中产生了几个执行上下文?5个(一个window和四个函数)
   -->
     <script type="text/javascript">
       console.log('global begin: ' + i) //global begin undefined
       var i = 1
       foo(1); //foo() begin:1  foo() begin:2  foo() begin:3  foo() end:3 foo() end:2 foo() end:1
       function foo(i) {
         if (i == 4) {
           return;
         }
         console.log('foo() begin:' + i);
         foo(i + 1);
         console.log('foo() end:' + i);
       }
       console.log('global end: ' + i) //global end: 1
     </script>
   ```

   

#### 2.2.5 面试题

```html
<body>
  <script type="text/javascript">
    /*
  测试题1: 先执行变量提升，在执行函数提升
  */
    function a() {}
    var a;
    console.log(typeof a) //function


    /*
    测试题2: 变量预处理, in操作符
     */
    if (!(b in window)) {
      var b = 1;
    }
    console.log(b) //undefined

    /*
    测试题3: 预处理, 顺序执行
     */
    var c = 1

    function c(c) {
      console.log(c)
    }
    c(2) //报错

    /* 相当于以下代码：
    var c;
    function c(c) {
      console.log(c)
    }
    c=1
    c(2)  //c不是函数了
    */
  </script>
</body>

```

### 2.3 作用域与作用域链

![image-20220314210313511](JS%E9%AB%98%E7%BA%A7.assets/image-20220314210313511.png)

#### 2.3.1 作用域

1. 理解

     * 就是一块"地盘", 一个代码段所在的区域
     * 它是静态的(相对于上下文对象), 在编写代码时就确定了
2. 分类

     * 全局作用域
     * 函数作用域
     * 没有块作用域(ES6有了)
3. 作用

     * 隔离变量，不同作用域下同名变量不会有冲突

   ![image-20220314210005839](JS%E9%AB%98%E7%BA%A7.assets/image-20220314210005839.png)

#### 2.3.2 作用域与执行上下文

1. 区别1

     * 全局作用域之外，每个函数都会创建自己的作用域，作用域在函数定义时就已经确定了。而不是在函数调用时
     * 全局执行上下文环境是在全局作用域确定之后, js代码马上执行之前创建
     * 函数执行上下文环境是在调用函数时, 函数体代码执行之前创建
2. 区别2

     * 作用域是静态的, 只要函数定义好了就一直存在, 且不会再变化
     * 上下文环境是动态的, 调用函数时创建, 函数调用结束时上下文环境就会被释放
3. 联系

     * 上下文环境(对象)是从属于所在的作用域

     * 全局上下文环境==>全局作用域

     * 函数上下文环境==>对应的函数使用域

![image-20220314210803507](JS%E9%AB%98%E7%BA%A7.assets/image-20220314210803507.png)

#### 2.3.3 作用域链

1. 理解

     * 多个上下级关系的作用域形成的链, 它的方向是从下向上的(从内到外)
     * 查找变量时就是沿着作用域链来查找的
2. 查找一个变量的查找规则

     * 在当前作用域下的执行上下文中查找对应的属性, 如果有直接返回, 否则进入2

     * 在上一级作用域的执行上下文中查找对应的属性, 如果有直接返回, 否则进入3

     * 再次执行2的相同操作, 直到全局作用域, 如果还找不到就抛出找不到的异常

```JavaScript
var a = 2;

    function fn1() {
      var b = 3;

      function fn2() {
        var c = 4;
        console.log(c); // 4
        console.log(b); //3
        console.log(a); //2
        console.log(d); //报错d is not defined
      }

      fn2();
    }
    fn1();
```



#### 2.3.4 面试题

```javascript
 /*
   问题: 结果输出多少?
   */
    var x = 10;

    function fn() {
      console.log(x);
    }

    function show(f) {
      var x = 20;
      f();
    }
    show(fn); //输出结果是10
```

![image-20220314211620901](JS%E9%AB%98%E7%BA%A7.assets/image-20220314211620901.png)

```javascript
 /*
   说说它们的输出情况
   */

    var fn = function () {
      console.log(fn)
    }
    fn()  //正常输出函数

    var obj = {
      fn2: function () {
        console.log(fn2)//要找应该是this.fn2
      }
    }
    obj.fn2()  //报错
```

![image-20220314211907295](JS%E9%AB%98%E7%BA%A7.assets/image-20220314211907295.png)

### 2.4 闭包

![image-20220314212242913](JS%E9%AB%98%E7%BA%A7.assets/image-20220314212242913.png)

#### 2.4.1 引入

```javascript
<body>

  <button>测试1</button>
  <button>测试2</button>
  <button>测试3</button>
  <!--
需求: 点击某个按钮, 提示"点击的是第n个按钮"
-->
  <script type="text/javascript">
    var btns = document.getElementsByTagName('button')
    /* //有问题
    for(var i=0,length=btns.length;i<length;i++) {  //btns是一个伪数组
      var btn = btns[i]
      btn.onclick = function () {
        alert('第'+(i+1)+'个')
      }
    }*/

    //解决一: 保存下标
    // for (var i = 0, length = btns.length; i < length; i++) {
    //   var btn = btns[i]
    //   btn.index = i
    //   btn.onclick = function () {
    //     alert('第' + (this.index + 1) + '个')
    //   }
    // }

    //解决办法: 利用闭包
    for (var i = 0, length = btns.length; i < length; i++) {
      (function (i) {
        var btn = btns[i]
        btn.onclick = function () {
          alert('第' + (i + 1) + '个')
        }
      })(i)
    }
  </script>
</body>
```

#### 2.4.2 闭包的理解

1. 如何产生闭包?
     * 当一个嵌套的内部(子)函数引用了嵌套的外部(父)函数的变量(函数)时, 就产生了闭包。
2. 闭包到底是什么?

   <img src="JS%E9%AB%98%E7%BA%A7.assets/image-20220314222852093.png" alt="image-20220314222852093" style="zoom:33%;" />

     * 使用chrome调试查看
     * 理解一: 闭包是嵌套的内部函数(绝大部分人)
     * 理解二: 是包含被引用变量(函数)的对象(极少数人)
     * 注意: 闭包存在于嵌套的内部函数中
3. 产生闭包的条件?

     * 函数嵌套

     * 内部函数引用了外部函数的数据(变量/函数)

```html
 <script type="text/javascript">
    function fn1() {
      var a = 3

      function fn2() { //执行函数定义就会产生闭包（不用调用内部函数）
        console.log(a)
      }
      
      fn2();
    }
    fn1()
  </script>
  <!-- 最新版chrome示例代码好像不会出现闭包对象了，整个fn2都没被加载 -->
```

#### 2.4.3 常见的闭包

1. 将函数作为另一个函数的返回值

2. 将函数作为实参传递给另一个函数调用

   ```html
     <script type="text/javascript">
       1. 将函数作为另一个函数的返回值
       function fn1() {
         var a = 2
   
         function fn2() {
           a++
           console.log(a)
         }
   
         return fn2
       }
       var f = fn1()
       f() // 3
       f() // 4
   
       // 2. 将函数作为实参传递给另一个函数调用
       function showMsgDelay(msg, time) {
         setTimeout(function () {
           console.log(msg)
         }, time)
       }
       showMsgDelay('hello', 1000)
     
     </script>
   ```
   
   

#### 2.4.4 闭包的作用

1. 使用函数内部的变量在函数执行完后, 仍然存活在内存中(延长了局部变量的生命周期)

2. 让函数外部可以操作(读写)到函数内部的数据(变量/函数)

问题:

1. 函数执行完后, 函数内部声明的局部变量是否还存在?一般是不存在的，存在于闭包中的变量才可能存在。

2. 在函数外部能直接访问函数内部的局部变量吗?不能，但是通过闭包让外部操作它。

   ```javascript
     function fun1() {
         var a = 3;
   
         function fun2() {
           a++; //引用外部函数的变量--->产生闭包
           console.log(a);
         }
   
         function fun3() { //fun3在函数执行完之后就释放了，不是闭包
           a--;
           console.log(a);
         }
         return fun2;
       }
       var f = fun1(); //由于f引用着内部的函数-->内部函数以及闭包都没有成为垃圾对象
   
       f(); //4  //间接操作了函数内部的局部变量
       f(); //5
   ```

#### 2.4.5 闭包的生命周期

1. 产生: 在嵌套内部函数定义执行完时就产生了(不是在调用)

2. 死亡: 在嵌套的内部函数成为垃圾对象时

   ```javascript
    function fun1() {
         //此处闭包已经产生（函数提升，内部函数对象已经创建了）
         var a = 3;
   
         function fun2() {
           a++;
           console.log(a);
         }
   
         return fun2;
       }
       var f = fun1();
   
       f(); //4
       f(); //5
       f = null //此时闭包对象死亡(包含闭包的函数对象成为了垃圾对象)
   ```

   

#### 2.4.6 闭包的应用：自定义JS模块

闭包的应用2 : 定义JS模块
  * 具有特定功能的js文件
  * 将所有的数据和功能都封装在一个函数内部(私有的)
  * 只向外暴露一个包信n个方法的对象或函数
  * 模块的使用者, 只需要通过模块暴露的对象调用方法来实现对应的功能

```javascript
/**
 * 自定义模块1
 */
function coolModule() {
  //私有的数据
  var msg = 'atguigu'
  var names = ['I', 'Love', 'you']

  //私有的操作数据的函数
  function doSomething() {
    console.log(msg.toUpperCase())
  }
  function doOtherthing() {
    console.log(names.join(' '))
  }

  //向外暴露包含多个方法的对象
  return {
    doSomething: doSomething,
    doOtherthing: doOtherthing
  }
}
----------------------------------------------------------------------------
<script type="text/javascript" src="05_coolModule.js"></script>
<script type="text/javascript">
  var module = coolModule()
  module.doSomething()
  module.doOtherthing()
</script>
</body>
</html>
```

```javascript
/**
 * 自定义模块2
 */
(function (window) {
  //私有的数据
  var msg = 'atguigu'
  var names = ['I', 'Love', 'you']
  //操作数据的函数
  function a() {
    console.log(msg.toUpperCase())
  }
  function b() {
    console.log(names.join(' '))
  }

  window.coolModule2 =  {
    doSomething: a,
    doOtherthing: b
  }
})(window)
----------------------------------------------------------------------------
<script type="text/javascript" src="05_coolModule2.js"></script>
<script type="text/javascript">
  coolModule2.doSomething()
  coolModule2.doOtherthing()
</script>
</body>
</html>
```



#### 2.4.7 闭包的缺点及解决

1. 缺点

     * 函数执行完后, 函数内的局部变量没有释放, 占用内存时间会变长
     * 容易造成内存泄露
2. 解决

     * 能不用闭包就不用

     * 及时释放

```javascript
   function fn1() {
      var a = 2;

      function fn2() {
        a++;
        console.log(a);
      }

      return fn2;
    }
    var f = fn1();

    f(); // 3
    f(); // 4

    f = null // 让内部函数成为垃圾对象-->回收闭包
```

#### 2.4.8 内存溢出与内存泄漏

1. 内存溢出

     * 一种程序运行出现的错误
     * 当程序运行需要的内存超过了剩余的内存时, 就出抛出内存溢出的错误
2. 内存泄露

     * 占用的内存没有及时释放

     * 内存泄露积累多了就容易导致内存溢出

     * 常见的内存泄露:
       * 意外的全局变量
       * 没有及时清理的计时器或回调函数
       * 闭包

```html
<script type="text/javascript">
    // 1. 内存溢出
    var obj = {}
    for (var i = 0; i < 100000; i++) {
      obj[i] = new Array(10000000)
    }
    console.log('------')

    // 2. 内存泄露
    // 意外的全局变量
    function fn() {
      a = [] //不小心没有var定义
    }
    fn()
    // 没有及时清理的计时器
    setInterval(function () {
      console.log('----')
    }, 1000)

    ---------------------------------------------------------
    //清理定时器的方法
    /* var intervalId = setInterval(function () {
      console.log('----')
    }, 1000)
    clearInterval(intervalId) */
  </script>
```



#### 2.4.9 面试题

```html
<script type="text/javascript">
    /*
   说说它们的输出情况
   */

    //代码片段一（这个没有闭包）
    var name = "The Window";
    var object = {
      name: "My Object",
      getNameFunc: function () {
        return function () {
          return this.name;
        };
      }
    };
    console.log(object.getNameFunc()()); //The Window

    //代码片段二（这个有闭包）
    var name2 = "The Window";
    var object2 = {
      name2: "My Object",
      getNameFunc: function () {
        var that = this;
        return function () {
          return that.name2;
        };
      }
    };
    console.log(object2.getNameFunc()()); //My Object
  </script>
```

```javascript
  /*
   说说它们的输出情况
   */

    function fun(n, o) {
      console.log(o)
      return {
        fun: function (m) {
          return fun(m, n)
        }
      }
    }
    var a = fun(0)
    a.fun(1)
    a.fun(2)
    a.fun(3) //undefined,0,0,0

    console.log('----------------------');

    var b = fun(0).fun(1).fun(2).fun(3) //undefined,0,1,2

    var c = fun(0).fun(1)
    c.fun(2)
    c.fun(3) //undefined,0,1,1
```

### 2.5 call和apply

call()和apply()

- 这两个方法都是函数对象的方法，需要通过**函数对象**来调用
-  这两个函数调用call()和apply()都会调用函数执行
-  在调用call()和apply()可以将一个对象指定为第一个参数
-  此时这个对象会将成为函数执行时的this

区别：

- call()方法可以将实参在对象之后依次传递

- apply()方法需要将实参封装到一个数组中统一传递

this的情况：

​    1.以函数形式调用时，this永远指向的都是window

​    2.以方法的形式调用时，this是调用方法的对象

​    3.以构造函数调用时，this是新创建的那个对象

​    4.使用call和apply调用时，this是指定的那个对象

```javascript
     function fun(a, b) {
            // alert('这是fun函数！')
            // alert(this)
            // alert(this.name)
            console.log("a=" + a);
            console.log("b=" + b);
        }
        var obj = {
            name: 'obj',
            sayName: function () {
                alert(this.name)
            }
        }
        var obj2 = {
            name: 'obj2'
        }


        // fun.call(obj, 2, 3)
        // fun.apply(obj, 2, 3) //报错
        fun.apply(obj, [2, 3])
        // fun();
        // fun.apply()
        // fun.call()   //通过函数对象调用，所以不可以写fun().call()

        // fun(); //object Window
        // fun.call(obj) //object Object
        // fun.apply(obj)
        // fun.apply(obj2) //obj2
        // obj.sayName.apply(obj2) //obj2
```



## 3 对象高级

### 3.1 对象创建模式

![image-20220315163517049](JS%E9%AB%98%E7%BA%A7.assets/image-20220315163517049.png)

#### 3.1.1 Object构造函数模式

方式一: Object构造函数模式

 套路: 先创建空Object对象, 再动态添加属性/方法

 适用场景: 起始时不确定对象内部数据

 问题: 语句太多

```javascript
 /*
  一个人: name:"Tom", age: 12
   */
  var p = new Object()
  //p = {}
  p.name = 'Tom'
  p.age = 12
  p.setName = function (name) {
    this.name = name
  }
  p.setaAge = function (age) {
    this.age = age
  }

  console.log(p)
```



#### 3.1.2 对象字面量模式

方式二: 对象字面量模式

套路: 使用{}创建对象, 同时指定属性/方法

适用场景: 起始时对象内部数据是确定的

问题: 如果创建多个对象, 有重复代码

```javascript
 var p = {
    name: 'Tom',
    age: 23,
    setName: function (name) {
      this.name = name
    }
  }
  console.log(p.name, p.age)
  p.setName('JACK')
  console.log(p.name, p.age)

  var p2 = {
    name: 'BOB',
    age: 24,
    setName: function (name) {
      this.name = name
    }
  }
```



#### 3.1.3 工厂模式

方式三: 工厂模式

套路: 通过工厂函数动态创建对象并返回

适用场景: 需要创建多个对象

问题: 对象没有一个具体的类型, 都是Object类型

```javascript
// 工厂函数: 返回一个需要的数据的函数
  function createPerson(name, age) {
    var p = {
      name: name,
      age: age,
      setName: function (name) {
        this.name = name
      }
    }
    return p
  }

  var p1 = createPerson('Tom', 12)
  var p2 = createPerson('JAck', 13)
  console.log(p1)
  console.log(p2)
```



#### 3.1.4 自定义构造函数模式

方式四: 自定义构造函数模式

套路: 自定义构造函数, 通过new创建对象

适用场景: 需要创建多个类型确定的对象

问题: 每个对象都有相同的数据, 浪费内存

```javascript
<script type="text/javascript">

  function Person(name, age) {
    this.name = name
    this.age = age
    this.setName = function (name) {
      this.name = name
    }
  }

  var p1 = new Person('Tom', 12)
  var p2 = new Person('Tom2', 13)
  console.log(p1, p1 instanceof Person)
```

#### 3.1.5 函数构造+原型的组合模式

方式六: 构造函数+原型的组合模式

套路: 自定义构造函数, 属性在函数中初始化, 方法添加到原型上

适用场景: 需要创建多个类型确定的对象

```javascript
 function Person(name, age) {
      this.name = name
      this.age = age
    }
    Person.prototype.setName = function (name) {
      this.name = name
    }
    var p1 = new Person('Tom', 12)
    var p2 = new Person('JAck', 23)
    p1.setName('TOM3')
    console.log(p1) //

    Person.prototype.setAge = function (age) {
      this.age = age
    }
    p1.setAge(23)
    console.log(p1.age) //23

    Person.prototype = {}
    p1.setAge(34)  
    console.log(p1)  //正常输出，年龄是34
    var p3 = new Person('BOB', 12) 
    p3.setAge(12)  //报错 p3.setAge is not a function
```

### 3.2 继承模式

![image-20220315163540825](JS%E9%AB%98%E7%BA%A7.assets/image-20220315163540825.png)

#### 3.2.1 原型链继承

```html
<body>
  <!--
方式1: 原型链继承
  1. 套路
    1. 定义父类型构造函数
    2. 给父类型的原型添加方法
    3. 定义子类型的构造函数
    4. 创建父类型的对象赋值给子类型的原型
    5. 将子类型原型的构造属性设置为子类型
    6. 给子类型原型添加方法
    7. 创建子类型的对象: 可以调用父类型的方法
  2. 关键
    1. 子类型的原型为父类型的一个实例对象
-->
  <script type="text/javascript">
    function Supper() { //父类型
      this.superProp = 'The super prop'
    }
    //原型的数据所有的实例对象都可见
    Supper.prototype.showSupperProp = function () {
      console.log(this.superProp)
    }

    function Sub() { //子类型
      this.subProp = 'The sub prop'
    }


    // 子类的原型为父类的实例
    Sub.prototype = new Supper()
    // 修正Sub.prototype.constructor为Sub本身
    Sub.prototype.constructor = Sub

    Sub.prototype.showSubProp = function () {
      console.log(this.subProp)
    }

    // 创建子类型的实例
    var sub = new Sub()
    // 调用父类型的方法
    sub.showSubProp()
    // 调用子类型的方法
    sub.showSupperProp()
  </script>
</body>
```

![image-20220315203316879](JS%E9%AB%98%E7%BA%A7.assets/image-20220315203316879.png)

#### 3.2.2 借用构造函数继承

```html
<body>
<!--
方式2: 借用构造函数继承(假的)
1. 套路:
  1. 定义父类型构造函数
  2. 定义子类型构造函数
  3. 在子类型构造函数中调用父类型构造
2. 关键:
  1. 在子类型构造函数中通用call()调用父类型构造函数
-->
<script type="text/javascript">

  function Person(name, age) {
    this.name = name
    this.age = age
  }

  function Student(name, age, price) {
    Person.call(this, name, age)   // 相当于：this.Person(name, age)
    this.price = price
  }

  var s = new Student('Tom', 20, 12000)
  console.log(s.name, s.age, s.price)
</script>
</body>
```

#### 3.2.3 组合继承

```html
<body>
<!--
方式3: 原型链+借用构造函数的组合继承
1. 利用原型链实现对父类型对象的方法继承
2. 利用call()借用父类型构建函数初始化相同属性
-->
<script type="text/javascript">

  function Person(name, age) {
    this.name = name
    this.age = age
  }
  Person.prototype.setName = function (name) {
    this.name = name
  }

  function Student(name, age, price) {
    Person.call(this, name, age) //为了得到父类型的属性
    this.price = price
  }
  Student.prototype = new Person()  //为了得到父类型的方法
  Student.prototype.constructor = Student  //修正constructor属性
  Student.prototype.setPrice = function (price) {
    this.price = price
  }

  var s = new Student('Tom', 12, 10000)
  s.setPrice(11000)
  s.setName('Bob')
  console.log(s)
  console.log(s.constructor)

</script>
</body>
```



## 4 线程机制与事件机制

### 4.1 进程与线程

![image-20220315210217250](JS%E9%AB%98%E7%BA%A7.assets/image-20220315210217250.png)

#### 4.1.1 进程和线程

1. 进程：程序的一次执行, 它占有一片独有的内存空间

2. 线程： CPU的基本调度单位, 是程序执行的一个完整流程

3. 进程与线程

     * 一个进程中一般至少有一个运行的线程: 主线程
     * 一个进程中也可以同时运行多个线程, 我们会说程序是多线程运行的
     * 一个进程内的数据可以供其中的多个线程直接共享
     * 多个进程之间的数据是不能直接共享的

4. 浏览器运行是单进程还是多进程?

     * 有的是单进程
       * firefox
       * 老版IE
     * 有的是多进程
       * chrome
       * 新版IE
5. 如何查看浏览器是否是多进程运行的呢?
     * 任务管理器==>进程
6. 浏览器运行是单线程还是多线程?
     * 都是多线程运行的

#### 4.1.2 图解

![image-20220315210606645](JS%E9%AB%98%E7%BA%A7.assets/image-20220315210606645.png)

#### 4.1.2 相关知识

![image-20220315210624002](JS%E9%AB%98%E7%BA%A7.assets/image-20220315210624002.png)

#### 4.1.3 相关问题

![image-20220315210654311](JS%E9%AB%98%E7%BA%A7.assets/image-20220315210654311.png)

### 4.2 浏览器内核

![image-20220315210811508](JS%E9%AB%98%E7%BA%A7.assets/image-20220315210811508.png)

1. 什么是浏览器内核?
     * 支持浏览器运行的最核心的程序
2. 不同的浏览器可能不太一样

     * Chrome, Safari: webkit
     * firefox: Gecko
     * IE: Trident
     * 360,搜狗等国内浏览器: Trident + webkit
3. 内核由很多模块组成

     * html,css文档解析模块 : 负责页面文本的解析

     * dom/css模块 : 负责dom/css在内存中的相关处理

     * 布局和渲染模块 : 负责页面的布局和效果的绘制

     * 布局和渲染模块 : 负责页面的布局和效果的绘制


     * 定时器模块 : 负责定时器的管理
    
     * 网络请求模块 : 负责服务器请求(常规/Ajax)
    
     * 事件响应模块 : 负责事件的管理
### 4.3 定时器引发的思考

```html
<body>

  <button id="btn">启动定时器</button>

  <!--
1. 定时器真是定时执行的吗?
  * 定时器并不能保证真正定时执行
  * 一般会延迟一丁点(可以接受), 也有可能延迟很长时间(不能接受)
2. 定时器回调函数是在分线程执行的吗?
  * 在主线程执行的, js是单线程的
3. 定时器是如何实现的?
  * 事件循环模型(后面讲)
-->
  <script type="text/javascript">
    document.getElementById('btn').onclick = function () {
      var start = Date.now()
      console.log('启动定时器')
      setTimeout(function () {
        console.log('定时器执行了: ', Date.now() - start)
      }, 200)

      // 定时器启动之后做一个长时间的工作
      for (var i = 0; i < 1000000000; i++) {

      }
      console.log('完成长时间工作', Date.now() - start)
    }
  </script>
</body>
```



### 4.4 JS是单线执行的

```html
<body>
  <!--
1. 如何证明js执行是单线程的?
  * setTimeout()的回调函数是在主线程执行的
  * 定时器回调函数只有在运行栈中的代码全部执行完后才有可能执行
2. 为什么js要用单线程模式, 而不用多线程模式?
  * JavaScript的单线程，与它的用途有关。
  * 作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。
  * 这决定了它只能是单线程，否则会带来很复杂的同步问题

3. 代码的分类:
  * 初始化代码
  * 回调代码
4. js引擎执行代码的基本流程
  * 先执行初始化代码: 包含一些特别的代码  回调函数（异步代码）
    * 设置定时器
    * 绑定监听
    * 发送ajax请求
  * 后面在某个时刻才会执行回调代码
-->
  <script type="text/javascript">
    setTimeout(function () {   //初始化代码，里面有回调代码
      console.log('timeout 2')
      alert('222222222222')
    }, 2000)

    setTimeout(function () {
      console.log('timeout 1')
      alert('111111111111')
    }, 1000)
    console.log('alert之前');
    alert('提示...') //暂停当前主线程的执行,同时暂停计时，点击确定后，恢复程序执行和计时
    console.log('alert之后')
  </script>
</body>
```



### 4.5 浏览器的事件循环（轮询）模型

![image-20220315213322628](JS%E9%AB%98%E7%BA%A7.assets/image-20220315213322628.png)

#### 4.5.1 模型原理图

![image-20220315213407872](JS%E9%AB%98%E7%BA%A7.assets/image-20220315213407872.png)

```html
<body>
  <button id="btn">测试</button>
  <!--
1. 所有代码分类
  * 初始化执行代码(同步代码): 包含绑定dom事件监听, 设置定时器, 发送ajax请求的代码
  * 回调执行代码(异步代码): 处理回调逻辑
2. js引擎执行代码的基本流程:
  * 初始化代码===>回调代码
3. 模型的2个重要组成部分:
  * 事件管理模块
  * 回调队列
4. 模型的运转流程
  * 执行初始化代码, 将事件回调函数交给对应模块管理
  * 当事件发生时, 管理模块会将回调函数及其数据添加到回调列队中
  * 只有当初始化代码执行完后(可能要一定时间), 才会遍历读取回调队列中的回调函数执行
-->
  <script type="text/javascript">
    function fn1() {
      console.log('fn1()')
    }
    fn1()

    document.getElementById('btn').onclick = function () {
      console.log('处理点击事件')
    }

    setTimeout(function () {
      console.log('到点了')
    }, 2000)

    function fn2() {
      console.log('fn2()')
    }
    fn2()
  </script>
</body>
```

#### 4.5.2 相关重要概念

![image-20220315214917975](JS%E9%AB%98%E7%BA%A7.assets/image-20220315214917975.png)

### 4.6 H5 Web Workers（多线程）

![image-20220315215145136](JS%E9%AB%98%E7%BA%A7.assets/image-20220315215145136.png)

#### 4.6.1 使用

```html
<body>
  <!--
1. H5规范提供了js分线程的实现, 取名为: Web Workers
2. 相关API
  * Worker: 构造函数, 加载分线程执行的js文件
  * Worker.prototype.onmessage: 用于接收另一个线程的回调函数
  * Worker.prototype.postMessage: 向另一个线程发送消息
3. 不足
  * worker内代码不能操作DOM(更新UI)
  * 不能跨域加载JS
  * 不是每个浏览器都支持这个新特性
-->
  <!-- 2022 谷歌和edge浏览器不支持本地worker 解决方法 放置服务器 -->
  <input type="text" id="number">
  <button id="btn">计算</button>
  <script type="text/javascript">
    function fibonacci(n) { //递归调用
      return n <= 2 ? 1 : fibonacci(n - 1) + fibonacci(n - 2)
    }

    // console.log(fibonacci(7));
    var input = document.getElementById('number')
    document.getElementById('btn').onclick = function () {
      var number = input.value

      var worker = new worker('worker.js')
      //绑定接收消息的监听
      worker.onmessage = function (event) {
        console.log('主线程接收返回的数据' + event.data);
        alert(event.data)
      }
      //向分线程发送消息
      worker.postMessage(number)
      console.log('主线程向分线程发送数据：' + number);


    }
    console.log(this); //window
  </script>
</body>
```

```javascript
function fibonacci(n) { //递归调用
    return n <= 2 ? 1 : fibonacci(n - 1) + fibonacci(n - 2)
}
console.log(this);  //不是window
var onmessage = function (event) {
    var number = event.data
    console.log('分线程接收到主线程发送的数据：' + number);
    //计算
    var result = fibonacci(number)
    worker.postMessage(number)
    console.log('主线程向分线程发送数据：' + number);
    // alert(resule)  //不能用，因为alert是window的方法，在分线程不能调用
    //分线程中的全局对象不再是window，所以在分线程中不可能在更新页面
}
```

#### 4.6.2 图解

![image-20220315225529578](JS%E9%AB%98%E7%BA%A7.assets/image-20220315225529578.png)

#### 4.6.3 不足

![image-20220315225722457](JS%E9%AB%98%E7%BA%A7.assets/image-20220315225722457.png)
