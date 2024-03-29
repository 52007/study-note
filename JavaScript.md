# JavaScript

## JavaScript变量提升

- JavaScript 中，函数及变量的声明都将被提升到函数的最顶部。

- JavaScript 中，变量可以在使用后声明，也就是变量可以先使用再声明。

  ```javascript
  a = 1
  console.log(a)
  var a
  ```

  上面的代码等同于下面的代码：

  ```JavaScript
  var a
  a = 1
  console.log(a)
  ```

  

- JavaScript 只有声明的变量会提升，初始化的不会。

  ```JavaScript
  var x = 1
  var y = 2
  console.log(x, y)//1 2
  ```

  ```JavaScript
  var x = 1
  console.log(x, y)//1 undefine
  var y = 2
  ```

  



## 正则表达式

**正则表达式（ Regular Expression ）**是用于匹配字符串中字符组合的模式。

- 在 JavaScript中，正则表达式也是对象。
- 正则表达式通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词(**替换**)，或从字符串中获取我们想要的特定部分(**提取**)等 。
- 一个正则表达式可以由简单的字符构成，比如 /abc/，也可以是简单字符和特殊字符的组合，比如 /ab*c/ 。其中特殊字符也被称为**元字符**，在正则表达式中是具有特殊意义的专用符号，如 ^ 、$ 、+ 等。
- 正则表达式里面不需要加引号 不管是数字型还是字符串型
- 正则表达式学习网址： https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions
- 正则表达式测试网址：http://tool.oschina.net/regex

### 创建正则表达式

1. 通过 RegExp 对象的构造函数创建：

   ```
   var 变量名 = new RegExp(/表达式/);
   ```

2. 通过字面量创建

   ```javascript
   var 变量名 = /表达式/;
   ```



### test 测试正则表达式

test() 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串。

- 语法：

```javascript
regexpObj.test(str);
```

- 说明：

  1. regexpObj 是我们写的正则表达式

  2. str 我们要测试的文本

  3. 上面的代码作用就是检测str文本是否符合我们写的正则表达式规范.

 **/abc/ ：只要包含abc字符串则true**

```javascript
var rg = /abc/;
console.log(rg.test('abc')); //true
console.log(rg.test('aabcd')); //true
console.log(rg.test('abcd')); //true
```



### 正则表达式中的特殊字符

#### 边界符

正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符：

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| ^      | 表示匹配行首的文本（以谁开始） |
| $      | 表示匹配行尾的文本（以谁结束） |

```javascript
var rg = /^abc/; //abc开头true
console.log(rg.test('abc')); //true
console.log(rg.test('aabcd')); //false
console.log(rg.test('abcd')); //true
```

**如果 ^ 和 $ 在一起，表示必须是精确匹配**：

```javascript
var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
console.log(reg1.test('abc')); // true
console.log(reg1.test('abcd')); // false
console.log(reg1.test('aabcd')); // false
console.log(reg1.test('abcabc')); // false
```



#### 字符类

1. **[]** 方括号：字符类表示有一系列字符**可供选择**，只要匹配其中**一个**就可以了。所有可供选择的字符都放在**方括号[]**内。

   ```javascript
   /[abc]/.test('andy')     // true 
   ```

   后面的字符串只要包含 abc 中任意一个字符，都返回 true 。

2. **[-]**  方括号内部 **范围符 -** 

   ```javascript
      /^[a-z]$/.test('c');     // true
   ```

   方括号内部加上 - 表示范围，这里表示 a 到 z 26个英文字母都可以，A-Z 表示 A 到 Z 26个大写英文字母都可以，0-9 表示 0 到 9 的数字都可以。

3. **[^]** 方括号内部 **取反符 ^**   

   ```javascript
      /[^abc]/.test('andy')     // false
   ```

   方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false。

4. 字符组合

   ```javascript
   /[a-z1-9]/.test('andy')     // true
   ```

   方括号内部可以使用**字符组合**，这里表示包含 a 到 z 的26个英文字母和 1 到 9 的数字都可以。



#### 量词符

量词符用来**设定某个模式出现的次数。**

| 量词  | 说明                    |
| ----- | ----------------------- |
| *     | 重复零次或更多次        |
| +     | 重复一次或更多次（>=1） |
| ?     | 重复一次或零次          |
| {n}   | 重复n次                 |
| {n,}  | 重复n次或更多次（>=n）  |
| {n,m} | 重复n到m次              |



#### 用户名验证案例

- 功能需求:

1. 如果用户名输入合法, 则后面提示信息为 :  用户名合法,并且颜色为绿色

2. 如果用户名输入不合法, 则后面提示信息为:  用户名不符合规范, 并且颜色为绿色

- 代码：

  ```html
  <!DOCTYPE html>
  <html>
  	<head>
  		<meta charset="utf-8">
  		<title></title>
  		<style>
  			.tips{
  				color: #ccc;
  			}
  			.right{
  				color: green;
  			}
  			.wrong{
  				color: red;
  			}
  		</style>
  	</head>
  	<body>
  		<input type="text" class="biaodan"><span class="tips">请输入用户名</span>
  		<script>
  			var biaodan = document.querySelector(".biaodan");
  			var tips = document.querySelector(".tips");
  			var reg = /^[a-zA-Z0-9_-]{6,16}$/;
  			biaodan.onblur = function(){
  				if(reg.test(this.value)){
  					tips.className = "right";
  					tips.innerHTML = '用户名格式正确';
  				}else{
  					tips.className = "wrong";
  					tips.innerHTML = '用户名格式不正确';
  				}
  			}
  		</script>
  	</body>
  </html>
  ```

  

#### 括号总结

1. 中括号[]

   表示字符集合，匹配括号中的任意字符

   ```javascript
   var reg = /^[abc]$/; //  表示 a||b||c
   ```

2. 大括号{}

   量词符，表示重复次数

   ```javascript
   var reg = /^abc{3}$/;
   ```

   注意上面代码中是让c重复三次，而不是abc重复三次。

3. 小括号()

   表示优先级

   ```javascript
   var reg = /^(abc){3}$/; // 它是让abc重复三次
   ```



### 预定义类

| 预定义类 | 说明                                                       |
| -------- | ---------------------------------------------------------- |
| \d       | 匹配0-9之间的任一数字，相当于[0-9]                         |
| \D       | 匹配所有0-9以外的字符，相当[ ^0-9]                         |
| \w       | 匹配任意的字母、数字和下划线，相当于[A-Za-z0-9_]           |
| \W       | 除所有字母、数字和下划线以外的字符，相当于[ ^A-Za-z0-9_]   |
| \s       | 匹配空格（包括换行符、制表符、空格等），相当于[\t\r\n\v\f] |
| \S       | 匹配非空格的字符，相当于[ ^\t\r\n\v\f]                     |

几种常见的验证正则表达式：

1. 

```
1. 手机号码:     /^1[3|4|5|7|8][0-9]{9}$/
2. QQ: /[1-9][0-9]{4,}/ (腾讯QQ号从10000开始)
3. 昵称是中文:     /^[\u4e00-\u9fa5]{2,8}$/
```



2. 

```javascript
// 座机号码验证:  全国座机号码  两种格式:   010-12345678  或者  0530-1234567
// 正则里面的或者 符号  |  
var reg = /^\d{3}-\d{8}|\d{4}-\d{7}$/;
```





























# JavaScript面向对象(JavaScript Object Oriented Programming)

## 一、两大编程思想

### 1.1 面向过程(POP)

​	**面向过程**就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

- **举例**：将大象放入冰箱，面向过程的做法是：打开冰箱，装进大象，关上冰箱。

- **优点**：性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。

- **缺点**：没有面向对象易维护、易复用、易扩展

### 1.2 面向对象(OOP)

​	**面向对象**是把事务分解成为一个个对象，然后由对象之间分工与合作。

- **举例**：将大象放入冰箱，先找出对象——大象、冰箱，再找出对象的功能：

1. 对象一——大象：
   - 进去
2. 对象二——冰箱：
   - 打开
   - 关闭
3. 使用大象和冰箱的功能

- **优点**：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护 

- **缺点**：性能比面向过程低



## 二、面向对象编程

什么是OOP？

Object Oriented Programming，就是面向对象的编程，还有OOD（面向对象的设计），OOA（面向对象的分析）。

面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。

### 2.1 三大特性和五大原则

#### 2.1.1 三大特性

1. 封装

   - 所谓封装，也就是把客观事物封装成抽象的**类**，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行**信息隐藏**。

   - 封装是面向对象的特征之一，是对象和类概念的主要特性。 简单的说，一个类就是一个封装了数据以及操作这些数据的代码的逻辑实体。

   - 在一个对象内部，某些代码或某些数据可以是私有的，不能被外界访问。通过这种方式，对象对内部数据提供了不同级别的保护，以防止程序中无关的部分意外的改变或错误的使用了对象的私有部分。

2. 继承：
   - 所谓继承是指可以让某个类型的对象获得另一个类型的对象的属性的方法。它支持按级分类的概念。
   - 继承是指这样一种能力：**它可以使用现有类的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展**。 
   - 通过继承创建的新类称为“子类”或“派生类”，被继承的类称为“基类”、“父类”或“超类”。
   - 继承的过程，就是从一般到特殊的过程。
   - 要实现继承，可以通过“继承”（Inheritance）和“组合”（Composition）来实现。继承概念的实现方式有二类：实现继承与接口继承。实现继承是指直接使用基类的属性和方法而无需额外编码的能力；接口继承是指仅使用属性和方法的名称、但是子类必须提供实现的能力；

3. 多态：
   - 所谓多态就是指一个类实例的**相同方法**在**不同情形**有**不同表现形式**。
   - 多态机制使具有不同内部结构的对象可以共享相同的外部接口。这意味着，虽然针对不同对象的具体操作不同，但通过一个公共的类，它们（那些操作）可以通过相同的方式予以调用。

#### 2.1.2 五大基本原则 

1. 单一职责原则SRP(Single Responsibility Principle)
   是指一个类的功能要单一，不能包罗万象。如同一个人一样，分配的工作不能太多，否则一天到晚虽然忙忙碌碌的，但效率却高不起来。

2. 开放封闭原则OCP(Open－Close Principle) 
   一个模块在扩展性方面应该是开放的而在更改性方面应该是封闭的。比如：一个网络模块，原来只服务端功能，而现在要加入客户端功能，那么应当在不用修改服务端功能代码的前提下，就能够增加客户端功能的实现代码，这要求在设计之初，就应当将服务端和客户端分开，公共部分抽象出来。
   
3. 替换原则(the Liskov Substitution Principle LSP) 
   子类应当可以替换父类并出现在父类能够出现的任何地方。比如：公司搞年度晚会，所有员工可以参加抽奖，那么不管是老员工还是新员工，也不管是总部员工还是外派员工，都应当可以参加抽奖，否则这公司就不和谐了。
   
4. 依赖原则(the Dependency Inversion Principle DIP) 具体依赖抽象，上层依赖下层。假设B是较A低的模块，但B需要使用到A的功能，这个时候，B不应当直接使用A中的具体类： 而应当由B定义一抽象接口，并由A来实现这个抽象接口，B只使用这个抽象接口：这样就达到了依赖倒置的目的，B也解除了对A的依赖，反过来是A依赖于B定义的抽象接口。通过上层模块难以避免依赖下层模块，假如B也直接依赖A的实现，那么就可能造成循环依赖。一个常见的问题就是编译A模块时需要直接包含到B模块的cpp文件，而编译B时同样要直接包含到A的cpp文件。
   
5. 接口分离原则(the Interface Segregation Principle ISP) 
   模块间要通过抽象接口隔离开，而不是通过具体的类强耦合起来



### 2.2 面向对象的思维特点

1. 抽取（抽象）对象共用的属性和行为组织(封装)成一个类(模板)

2. 对类进行实例化, 获取类的对象

面向对象编程我们考虑的是有哪些对象，按照面向对象的思维特点,不断的创建对象,使用对象,指挥对象做事情。

### 2.3 对象

在 JavaScript 中，对象是**一组无序的相关属性和方法的集合，万物皆对象**，例如字符串、数值、数组、函数等。这即是说，对象是由属性和方法组成的：

- 属性：事物的**特征，**在对象中用**属性**来表示（常用名词）

- 方法：事物的**行为，**在对象中用**方法**来表示（常用动词）

## 三、类与对象

### 3.1 类的创建

```javascript
class Star{
    
}
var ldh = new Star();
```

1. 类抽象了对象的公共部分，它泛指某一大类；
2. 通过class关键字创建类，类名我们还是习惯性定义**首字母大写**；
3. 生成实例时 **new** 不能省略，类必须使用 **new** **实例化对象**；
4. **在 ES6 中类没有变量提升**，所以必须先定义类，才能通过类实例化对象.

### 3.2 类中的构造函数constructor

```javascript
// 创建一个明星类
class Star{
	constructor(name,age){
		this.name = name;
		this.age = age;
	}
}
// 利用类创建对象
var ldh = new Star("刘德华","18");
```

1. constructor() 方法是类的**构造函数（默认方法）**，**用于传递参数，返回实例对象；**
2. constructor 函数 只要 **new 生成实例时,就会自动调用这个函数**, 如果我们不写这个函数,类也会自动生成这个函数；
3. 注意语法规范,：
   - 创建类，类名后面不要加小括号；
   - 生成实例 类名后面加小括号；
   - 构造函数不需要加function；

### 3.3 类添加方法

```javascript
class Person {
  constructor(name,age) {   // constructor 构造器或者构造函数
      this.name = name;
      this.age = age;
    }
   say() {
      console.log(this.name + '你好');
   }
   sing() {
      console.log("我会唱歌");
   }
}    
```

1. **类里面所有的函数不需要写function；**
2. **多个函数方法之间不需要添加逗号分隔；**

### 3.4 类的继承

#### 3.4.1 extends关键字

子类可以继承父类的一些属性和方法。

```javascript
class Father {
      constructor(surname) {
        this.surname= surname;
      }
      say() {
        console.log('你的姓是' + this.surname);

       }
}
class Son extends Father{  // 这样子类就继承了父类的属性和方法

}
var damao= new Son('刘');
damao.say();  
```

#### 3.4.2 super关键字

super 关键字用于访问和调用对象父类上的函数。

- 子类在构造函数中使用super，必须放在this声明前面（**必须先调用父类的构造方法，再使用子类的构造方法**）；
- 可以调用父类的**构造函数**，也可以调用父类的**普通函数**：

##### super调用父类的构造函数

```javascript
 class Father {
    constructor(surname) {
        this.surname = surname;
     }
    saySurname() {
      console.log('我的姓是' + this.surname);
    }
}
// 子类继承父类的属性和方法
class Son extends Father { 
    constructor(surname, fristname) {
         super(surname);   // 调用父类的constructor(surname),必须写在子类的this声明之前
         this.fristname = fristname;
     }
    sayFristname() {
         console.log("我的名字是：" + this.fristname);

    }
}
var damao = new Son('刘', "德华");
damao.saySurname();//我的姓是刘
damao.sayFristname();//我的名字是：德华   

```

##### super调用父类的普通函数

```javascript
class Father {
     say() {
         return '我是爸爸';
     }
 }

class Son extends Father { // 这样子类就继承了父类的属性和方法
     say() {
          //super调用父类的方法say
          return super.say() + '的儿子';
     }
}
var damao = new Son();
console.log(damao.say());    
```

#### 3.4.3 类继承中的就近原则

- 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的；

- 如果子类里面没有,就去查找父类有没有这个方法,如果有,就执行父类的这个方法；

如上例代码中，damao对象是优先调用了类Son中的say()方法。

### 3.5 类中this的指向问题

- 构造函数中的this指向的是构建的实例；

- 类中添加的方法中的this指向的是调用的对象；
- **类里面的共有的属性和方法一定要加this使用.**

```html
<body>
    <button>点击</button>
    <script>
        var that;//定义全局变量
        var _that;
        class Star {
            constructor(uname, age) {
                // constructor 里面的this 指向的是 创建的实例对象
                that = this;
                console.log(this);//ldh

                this.uname = uname;
                this.age = age;
                // this.sing();
                this.btn = document.querySelector('button');
                this.btn.onclick = this.sing;//btn这个按钮调用了sing这个函数，因此此时sing()里面的this指向的是btn这个按钮
            }
            sing() {
                console.log(this);//btn

                console.log(that.uname); // that里面存储的是constructor里面的this，输出结果为“刘德华”
            }
            dance() {
                // 这个dance里面的this 指向的是实例对象 ldh 因为ldh 调用了这个函数
                _that = this;
                console.log(this);

            }
        }

        var ldh = new Star('刘德华');
        console.log(that === ldh);//true
        ldh.dance();//ldh
        console.log(_that === ldh);//true
    </script>
</body>
```



## 四、创建对象的各种方法

### 4.1 原始模式

```JavaScript
//1.原始模式，对象字面量方式
var person = {
    name: 'Jack',
    age: 18,
    sayName: function() {
		alert(this.name);
    }
};

//2.原始模式，Object构造函数方式
var person = new Object();
person.name = 'Jack';
person.age = 18;
person.sayName = function () {
    alert(this.name);
};
```



### 4.2 工厂模式

看上面的原始模式，显然，当我们要创建批量的person1、person2……时，每次都要敲很多代码，资深copypaster都吃不消！然后就有了批量生产的工厂模式：

```javascript
function factoryPerson(name, age) {
    var person = new Object();
    person.name = name;
    person.age = age;
    person.sayName = function() {
        alert(this.name)
    };
    return person;
}
var person1 = factoryPerson('李琳琦', 18);
console.log(person1 instanceof Object);//ture
console.log(typeof(person1));//Object
```

工厂模式就是批量化生产，简单调用就可以进入造人模式。指定姓名年龄就可以造一堆小宝宝，解放双手。**但是由于是工厂暗箱操作的，所以你不能识别这个对象到底是什么类型（instanceof 测试为 Object）**，另外每次造人时都要创建一个独立的temp对象，代码臃肿。



### 4.3 构造函数

在 ES6之前， JS 中并没用引入类的概念，对象不是基于类创建的，而是用一种称为**构造函数**的特殊函数来定义对象和它们的特征。

```JavaScript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayName = function() {
    alert(this.name);
  };
}

var person1 = new Person('Linqi',18)
console.log(person1 instanceof Object)//true
console.log(person1 instanceof Person)//true
console.log(typeof(person1));//Object

Person('Linqi', 18)
console.log(window.name);//Linqi
```
**构造函数**是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与 **new** 一起使用。我们可以把对象中一些**公共的属性和方法**抽取出来，然后封装到这个函数里面。

在 JS 中，使用构造函数时要注意以下两点：

1. 构造函数用于创建某一类对象，其首字母要大写

2. 构造函数要和 new 一起使用才有意义

#### 4.3.1 new关键字

**new** 在执行时会做四件事情：

1. 在内存中创建一个新的空对象。

2. 让 this 指向这个新的对象。

3. 执行构造函数里面的代码，给这个新对象添加属性和方法。

4. 返回这个新对象（所以构造函数里面不需要 return ）。

#### 4.3.2 静态成员与实例成员

构造函数中的属性和方法我们称为成员, 成员可以添加。

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayName = function() {
    alert(this.name);
  };
}

var person1 = new Person('Linqi',18)
console.log(Person.age)//undefine，不可以用构造函数访问实例成员

Person.sex = 'fale'//定义静态成员
console.log(Person.sex)//fale，可以用构造函数访问静态成员
console.log(person1.sex)//undefine，不可以用实例访问静态成员
```

1. **实例成员：**

- **实例成员就是构造函数内部通过this添加的成员**，如上例代码中 name、age、sayName就是实例成员。

- 实例成员只能通过实例化的对象来访问；

2. **静态成员：**

- 静态成员是在构造函数本身上添加的成员，如上例代码中的sex就是静态成员；

- 静态成员只能通过构造函数来访问；



### 4.4 构造函数+原型

```JavaScript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayName = function() {
  this.sayName = function() {
    alert(this.name);
  };
}
var person1 = new Person('Linqi', 18)

Person.prototype.hobbies = ['sleep', 'weibo']

console.log(person1)
// age: 18
// name: "Linqi"
// __proto__:{
//   hobbies: (2) ["sleep", "weibo"]
//   sayName: ƒ ()
//   constructor: ƒ Person(name, age)
//   __proto__: Object
// }


console.log(person1.__proto__)
// hobbies: (2) ["sleep", "weibo"]
// sayName: ƒ ()
// constructor: ƒ Person(name, age)
// __proto__: Object
```

做法是将需要独立的属性方法放入构造函数中，而可以**共享的部分则放入原型**中，这样做可以最大限度节省内存而又保留对象实例的独立性。



## 五、原型链

![原型链](./images/javascript/原型链.png)

### 5.1 构造函数原型 prototype

构造函数方法很好用，但是存在浪费内存的问题。

如上例代码中两个不同的对象ldh和zxy调用sayName()方法，指向的是不同的地址。

![浪费内存的构造函数](D:\52007前端学习\前端笔记\images\javascript\浪费内存的构造函数.png)

因此，我们可以把像sayName这样的**公共方法**定义在构造函数的原型对象prototype上，构造函数通过原型分配的函数是所有对象所**共享的**。

```javascript
Star.prototype.sing = function() {
	console.log('我会唱歌');
}
```

- 什么是**构造函数的原型**？

  JavaScript规定，**每一个构造函数都有一个prototype属性**，**prototype就是一个对象**，我们也称为**原型对象**，**这个对象的所有属性和方法，都会被构造函数所拥有**。

- 原型的作用是什么？

  共享方法。

### 5.2 对象原型 \__proto__

所有对象都会有一个属性 \__proto\_\_指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数prototype原型对象的属性和方法，就是因为对象有\_\_proto__原型的存在。

- 对象原型\__proto__和构造函数原型对象prototype是等价的；

  ```javascript
  console.log(ldh.__proto__ === Star.prototype);//true
  ```

- \__proto__对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，**不可以使用这个属性**，它只是内部指向原型对象 prototype；

- 方法的查找规则：

  - 方法的查找规则: 首先先看ldh 对象身上是否有 sing 方法,如果有就执行这个对象上的sing；
  - 如果没有sing 这个方法,因为有\__proto__ 的存在，就去构造函数原型对象prototype身上去查找sing这个方法

### 5.3 constructor

对象原型（ \__proto__）和构造函数（prototype）原型对象里面都有一个属性 constructor 属性 ，constructor 我们称为构造函数，因为它指回构造函数本身。

**constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数：**

一般情况下，对象的方法都在构造函数的原型对象中设置。我们可以通过下面的方式给原型对象prototype设置方法：

```javascript
Star.prototype.sing = function(){
	console.log("唱歌");
}
Star.prototype.dance = function(){
	console.log("跳舞");
}
```

然而，如果像这样有多个对象的方法，我们可以给原型对象采取对象形式赋值的方式来设置方法：

```javascript
Star.prototype = {
	sing: function(){
		console.log("唱歌");
	},
	dance: function(){
		console.log("跳舞");
	}
}
```

但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor  就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。看下面的例子：

```javascript
Star.prototype = {
	constructor: Star,//添加一个 constructor 指向原来的构造函数
	sing: function(){
		console.log("唱歌");
	},
	dance: function(){
		console.log("跳舞");
	}
}
```

### 5.4 JavaScript 的成员查找机制(规则)

1. 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
2. 如果没有就查找它的原型（也就是 \__proto__指向的 prototype 原型对象）。
3. 如果还没有就查找原型对象的原型（Object的原型对象）。
4. 依此类推一直找到 Object 为止（null）。
5. \__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。

```javascript
function Star(uname, age) {
	this.uname = uname;
	this.age = age;
}
Star.prototype.sing = function() {
	console.log('我会唱歌');
}
Star.prototype.sex = '女';

var ldh = new Star('刘德华', 18);
ldh.sex = '男';
console.log(ldh.sex);//男
```

### 5.5 原型对象this指向

- 构造函数中的this 指向我们实例对象；
- 原型对象里面放的是方法，这个方法中 this 指向的是这个方法的调用者，也就是这个实例对象；

### 5.6 扩展内置对象

可以通过原型对象，对原来的内置对象扩展自定义的方法。比如给数组增加自定义求和的功能。

```javascript
Array.prototype.sum = function() {
	var sum = 0;
	for (var i = 0; i < this.length; i++) {
		sum += this[i];
	}
	return sum;
};

var arr=[1,2,3];
console.log(arr.sum());//6
var arr1 = new Array(11,22,33);
console.log(arr1.sum());//66
```

**注意：数组和字符串内置对象不能给原型对象覆盖操作：Array.prototype = {} ，只能是 Array.prototype.xxx = function(){} 的方式。**



## 六、组合继承

ES6之前并没有给我们提供 extends 继承。我们可以通过**构造函数+原型对象**模拟实现继承，被称为**组合继承**。

### 6.1 借用构造函数继承父类型属性

#### 6.1.1 call方法

功能：调用这个函数, 并且修改函数运行时的 this 指向   

语法：fun.call(thisArg, arg1, arg2, ...) 

- thisArg：当前调用函数 this 的指向对象；
- arg1，arg2：传递的其他参数。

#### 6.1.2 核心原理

通过 call() 把父类型的 this 指向子类型的 this ，这样就可以实现**子类型继承父类型的属性**。   

```javascript
// 借用父构造函数继承属性
// 1. 父构造函数
function Father(uname, age) {
	// this 指向父构造函数的对象实例
	this.uname = uname;
	this.age = age;
}
// 2 .子构造函数 
function Son(uname, age, score) {
	// this 指向子构造函数的对象实例
	Father.call(this, uname, age);
	this.score = score;
}
var son = new Son('刘德华', 18, 100);
console.log(son);
```



### 6.2 借用原型对象继承父类型方法

上面通过构造函数继承了父类型的属性，那么父类型的方法能否也通过构造函数继承过来呢？

一般情况下，对象的方法都在构造函数的**原型对象prototype**中设置，通过构造函数无法继承父类方法。  

- 错误的实现方法：Son.prototype = Father.prototype

```javascript
function Father(name, age) {
  this.name = name
  this.age = age
}
Father.prototype.say = function() {
  console.log('说话')
}
function Son(name, age) {
  Father.call(this, name, age)
}
Son.prototype = Father.prototype//不可以这么设置
Son.prototype.exam = function() {
  console.log('我还要考试')
}
console.log(Father.prototype)//此时打印出的Father的原型对象中也出现了exam方法
```

这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化。如上栗中我给子构造函数 Son 的原型对象添加一个方法 exam，此时父构造函数 Father 的原型对象也会添加这个方法，怎么我做爸爸的也要考试了！？

- 正确的实现方法：

```javascript
Son.prototype = new Father();
```

**原理**：通过 new Father() 创建了一个Father构造函数的实例，让Son的原型对象指向这个实例。而Father实例对象中又有对象原型\__proto__指向Father原型对象。因为父类实例化之后另外开辟空间，就不会影响原来父类原型对象。此时就实现了Son继承Father原型对象中添加的方法。

![借用原型对象继承父类型方法](D:\52007前端学习\前端笔记\images\javascript\借用原型对象继承父类型方法.png)

**注意，如果利用对象的形式修改了原型对象,需要利用constructor 指回原来的构造函数：**

```javascript
Son.prototype.constructor = Son;
```

综上所述上栗的代码应修改为：

```JavaScript
//父构造函数
function Father(name, age) {
  this.name = name
  this.age = age
}
//为父构造函数原型对象添加方法say
Father.prototype.say = function() {
  console.log('说话')
}
//子构造函数
function Son(name, age) {
  Father.call(this, name, age)
}
// Son.prototype = Father.prototype//不可以这么设置
Son.prototype = new Father()//将子构造函数的原型对象指向父构造函数的一个实例
Son.prototype.constructor = Son//将子构造函数的原型对象的constructor指回Son

//为子构造函数原型对象添加方法exam
Son.prototype.exam = function() {
  console.log('我还要考试')
}

console.log(Son.prototype)
console.log(Father.prototype)//此时打印出的Father的原型对象中不会exam方法
var son = new Son('刘德华的儿子', 10)//创建子构造函数的实例
son.say()//son可以调用父构造函数原型对象中的方法
```



### 6.3 类的本质

1. class本质还是function；
2. 类的所有方法都定义在类的prototype属性上；
3. 类创建的实例,里面也有\__proto__ 指向类的prototype原型对象；

4. 所以ES6的类它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已；
5. 所以ES6的类其实就是**语法糖**(语法糖就是一种便捷写法，简单理解, 有两种方法可以实现同样的功能, 但是一种写法更加清晰、方便，那么这个方法就是语法糖。)



## 七、函数进阶

### 7.1 函数的定义方式

1. 自定义函数（命名函数）

   ```javascript
   function fn() {};
   ```

2. 函数表达式（匿名函数）

   ```javascript
   var fun = function() {};
   ```

3. new Function('参数1','参数2', '函数体');

   ```javascript
   var f = new Function('a', 'b', 'console.log(a + b)');
   ```

- 第三种方式执行效率低，也不方便书写，因此较少使用

- 所有函数都是 Function 的实例(对象)  

- 函数也属于对象

### 7.2 函数的调用方式

1. 普通函数

   ```javascript
   function fn() {
   	console.log('人生的巅峰');
   }
   fn();   
   fn.call();
   ```
   
2. 对象的方法

   ```javascript
   var o = {
   	sayHi: function() {
   		console.log('人生的巅峰');
   	}
   }
   o.sayHi();
   ```

3. 构造函数

   ```javascript
   function Star() {};
   new Star();
   ```

4. 绑定事件函数

   ```javascript
   btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
   ```

5. 定时器函数

   ```JavaScript
   setInterval(function() {}, 1000);  //这个函数是定时器自动1秒钟调用一次
   ```

6. 立即执行函数

   ```JavaScript
   (function() {
   	console.log('人生的巅峰');
   })();
   ```



### 7.3 函数内this的指向

函数this的指向，是当我们调用函数的时候确定的。调用方式的不同决定了this 的指向不同。

| 调用方式     | this指向                                   |
| ------------ | ------------------------------------------ |
| 普通函数调用 | window                                     |
| 构造函数调用 | 实例对象，原型对象里面的方法也指向实例对象 |
| 对象方法调用 | 该方法所属对象                             |
| 事件绑定方法 | 绑定事件对象                               |
| 定时器函数   | window                                     |
| 立即执行函数 | window                                     |



### 7.4 改变函数内this的指向

JavaScript 为我们专门提供了一些函数方法来帮我们更优雅的处理函数内部 this 的指向问题，常用的有call()、 bind()、apply() 三种方法。

#### 7.4.1 call()

- 作用：call() 方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的 this 指向。

- 语法：

  ```
  fun.call(thisArg, arg1, arg2, ...)
  ```

- 说明：

  - thisArg：在 fun 函数运行时指定的 this 值

  - arg1，arg2：传递的其他参数

  - 返回值就是函数的返回值，因为它就是调用函数

  - 因此当我们想改变 this 指向，同时想调用这个函数的时候，可以使用 call，比如上面说过的继承



#### 7.4.2 apply()

- 作用：apply() 方法调用一个函数。简单理解为调用函数的方式，但是它可以改变函数的 this 指向。

- 语法：

  ```
  fun.apply(thisArg, [argsArray])
  ```

- 说明：

  - thisArg：在fun函数运行时指定的 this 值

  - argsArray：传递的值，必须包含在**数组**里面；

  - 返回值就是函数的返回值，因为它就是调用函数

  - 可以看出apply()和call()没有什么太大的不同， apply 主要跟数组有关系，比如使用 Math.max() 求数组的最大值

    ```javascript
    var max = Math.max.apply(Math, arr);
    var min = Math.min.apply(Math, arr);
    ```

    如：
    
    ```JavaScript
    var max = Math.max([1,2,3]);
    console.log(max)//null
    ```
    
    ```javascript
    var max = Math.max.apply(Math, [1,2,3]);
    console.log(max)//3
    ```
    
    

#### 7.4.3 bind()

- 作用：bind() 方法**不会调用函数**。但是能改变函数内部this 指向 。

- 语法：

  ```
  fun.bind(thisArg, arg1, arg2, ...) 
  ```

- 说明：

  - thisArg：在 fun 函数运行时指定的 this 值

  - arg1，arg2：传递的其他参数

  - 返回由指定的 this 值和初始化参数改造的**原函数拷贝**

  - 因此当我们只是想改变 this 指向，并且不想调用这个函数的时候，可以使用 bind

- 案例：实现点击一个按钮，3秒内不可再次点击的效果。

  ```javascript
  var btns = document.querySelectorAll('button')
  for(var i=0; i<btns.length; i++) {
      btns[i].onclick = function() {
          this.disabled = true
          setTimeout(function() {
              this.disabled = false
          }.bind(this),2000)//如果不指定this，那么this就是window，window当然没有disabled属性
      }
  }
  ```



### 7.5 高阶函数

**高阶函数**是对其他函数进行操作的函数，它**接收函数作为参数**或**将函数作为返回值输出**。

- 接受函数作为参数

  ```javascript
  function fn(a, b, callback) {
      console.log(a + b);
      callback && callback();
  }
  fn(1, 2, function() {
      console.log('我是最后调用的');
  });
  ```

- 将函数作为返回值输出

  ```javascript
  function fn(){
      return function() {}
  }
  fn();
  ```



### 7.6 闭包

#### 7.6.1 变量作用域

变量根据作用域的不同分为两种：**全局变量**和**局部变量**。

1. 函数内部可以使用全局变量。

2. 函数外部不可以使用局部变量。

3. 当函数执行完毕，本作用域内的局部变量会销毁。

#### 7.6.2 什么是闭包

闭包（closure）指**有权访问另一个函数作用域中变量的函数**。  -----  JavaScript 高级程序设计

创建闭包的常用方式，就是在一个函数内部创建另一个函数：

```javascript
 function fn1(){    
　　　　var num = 10;
　　　　function fn2(){
　　　　　　console.log(num); // 10
　　　　}
       fn2();
　}
  fn1();
```

#### 7.6.3 在chrome中调试闭包

1.  打开浏览器，按 F12 键启动 chrome 调试工具。

2.  设置断点。

3.  找到 **Scope** 选项（Scope 作用域的意思）。

4.  当我们重新刷新页面，会进入断点调试，Scope 里面会有两个参数（global 全局作用域、local 局部作用域）。

5.  当执行到 fn2() 时，Scope 里面会多一个 **Closure** 参数 ，这就表明产生了闭包。



#### 7.6.4 闭包的作用

闭包的主要作用: **延伸了变量的作用范围。**

```javascript
function fn(){
    var num=10;
    return function(){
        console.log(num);
    }
}
var f = fn();//这里相当于f=function(){console.log(num)}
f();//这里即调用了匿名函数
```


#### 7.6.5 闭包案例

##### 点击li输出索引号

在之前，我们是通过给li添加index属性来实现的：

```javascript
window.onload = function(){
	var lis = document.querySelectorAll("li");
	for (var i=0;i<lis.length;i++){
		lis[i].index = i;
		lis[i].onclick = function(){
			console.log(this.index);
		}
	}
};
```

现在，我们可以通过闭包来实现：

```javascript
window.onload = function(){
	var lis = document.querySelectorAll("li");
	for (var i=0;i<lis.length;i++){
		(function(i){
			lis[i].onclick = function(){
				console.log(i);
			}
		})(i);
	}
};
```

通过立即执行函数(function(){})() 传入参数i，每一次循环都会产生一个立即执行函数。



##### 定时器中的闭包

需求：3秒之后打印出li的所有内容

代码：

```javascript
window.onload = function(){
	var lis = document.querySelectorAll("li");
	for (var i=0;i<lis.length;i++){
		(function(i){
			setTimeout(function(){
				console.log(lis[i].innerHTML);
			},3000);
		})(i);
	}
};
```



##### 计算打车价格

需求：

1. 打车起步价13元(3公里内), 之后每多一公里增加5块钱.
2. 用户输入公里数就可以计算打车价格
3. 如果有拥堵情况,总价格多收取10块钱拥堵费

代码实现：

```javascript
var carPrice = (function(){
	//起步价
	var start = 13;
	//总价
	var total = 0;
	return {
		price: function(n){
			if (n<=3){
				total = start;
			} else {
				total = (n-3)*5 + start;
			}
			return total;
		},
		yd: function(flag){
			return flag ? total + 10 : total;
		}
	}
})();

console.log(carPrice.price(5));
console.log(carPrice.yd(true));

console.log(carPrice.price(2));
console.log(carPrice.yd(false));
```



### 7.7 递归函数

#### 7.7.1 什么是递归

- 如果一个函数**在内部可以调用其本身**，那么这个函数就是**递归函数**。

- 递归函数的作用和循环效果一样

- 由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件 

#### 7.7.2 递归求解问题

##### 求1~n的阶乘

```javascript
function fn(n){
	if(n == 1){
		return 1;
	} else {
		return n*fn(n-1);
	}
}
console.log(fn(3));
```



##### 求斐波那契数列

```javascript
//斐波那契数列:1 1 2 3 5 8 13 21 34 55 89
//n表示数列索引值
function fn(n){
	if( n == 1 || n == 2){
		return 1;
	}
	return fn(n-1) + fn(n-2);
}
console.log(fn(11));
```



##### 根据id返回对应的数据对象

```JavaScript
var data = [
  {
    id: 1,
    name: '家电',
    goods: [
      {
        id: 11,
        gname: '冰箱',
        goods: [
          {
            id: 111,
            ggname: '海尔'
          },
          {
            id: 112,
            ggname: '美的'
          }
        ]
      },
      {
        id: 12,
        gname: '洗衣机'
      }
    ]
  },
  {
    id: 2,
    name: '服饰'
  }
]

function getById(json, id) {
  var o ={}
  json.forEach(function(item) {
    if (item.id == id){
      o = item
    } else if (item.goods && item.goods.length > 0) {
      o = getById(item.goods, id)
    }
  })
  return o
}
console.log(getById(data, 1))
console.log(getById(data, 2))
console.log(getById(data, 11))
console.log(getById(data, 12))
console.log(getById(data, 111))
console.log(getById(data, 112))
```





## 八、ES5中常用的方法

ES5 中给我们新增了一些方法，可以很方便的操作数组或者字符串，这些方法主要包括：

- 数组方法

- 字符串方法

- 对象方法

### 8.1 数组方法

#### 8.1.1 创建数组的基本方式

1. 使用Array构造函数：

   ```js
   var arr = new Array()
   
   //表示创建length为3的数组
   var arr = new Array(3)
   
   //表示创建包含这几项的数组
   var arr = new Array('red','yellow','blue')
   ```

   

2. 字面量：

   ```js
   var arr = []
   ```

#### 8.1.2 检测数组

```js
if (value instanceof Array){
//instanceof的问题在于它假定只有一个全局执行环境，若网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而有不同版本的Array构造函数
}
```

```js
if (Array.isArray(value)){

}
```

#### 8.1.3 栈方法

**push**()：添加到末尾，返回修改后数组的长度

**pop**()：移除最后一项，返回移除的项

#### 8.1.4 队列方法

**shift**()：移除数组第一项，返回移除的项

结合使用shift() 和push()方法，可以像使用队列一样使用数组

**unshift**()：在数组的第一项添加任意个项，返回数组的长度

结合使用unshift()和pop()方法，可以从相反的方向来模拟队列

#### 8.1.5 排序方法

**reserve**()为反转数组

**sort**()：

1. 默认情况下，sort方法按照升序排列数组项，该方法会调用每个数组项的**toString**方法，然后比较得到的字符串，再确定如何排序。**即使数组中的每一项都是数值，sort方法得到的也是字符串。**

2. sort方法可以接受一个**比较函数**作为参数，比较函数返回两个参数，**如果第一个参数应该在第二个参数之前，返回负数；如果第一个参数应该在第二个参数之后，返回正数；如果两个参数相等，则返回0**；

   来看下面的这个例子：

   ```js
   function compare(value1, value2) {
       if (value1 < value2){
          return 1
       } else if (value1 > value2) {
          return -1
       } else {
          return 0
       }
   }
   var values = [0,1,5,10,15]
   values.sort(compare)
   console.log(values)//0,1,5,10,15
   ```

   我们也可以将compare函数写成这样：

   ```js
   function compare(value1,value2) {
   	return value1 - value2
   }
   ```

   注意，如果你想通过sort实现降序，那么你可以把compare函数写成这样：

   ```js
   function compare(value1, value2) {
   	return value2 - value1
   }
   ```

sort()和reserve()都返回排序之后的数组

#### 8.1.6 操作方法

**concat**()：不会影响原数组

```
var arr1 = [1,2,3]
var arr2 = arr1.concat(4,5,[6,7])
console.log(arr1)//1,2,3
console.log(arr2)1,2,3,4,5,6,7
```



**slice**()：

- 不会影响原数组
- 能够基于当前数组的一或多个项创建一个新的数组
- 可以接受一个参数，返回以该参数为索引到当前数组末尾的所有项
- 可以接受两个参数，返回起始到结束位置之间的项，但是不包括结束位置的项。

```js
var arr1 = [1,2,3,4,5]
var arr2 = arr1.slice(1)
var arr3 = arr1.slice(1,4)

console.log(arr1)//1,2,3,4,5
console.log(arr2)//2,3,4,5
console.log(arr3)//2,3,4
```



**splice**()：

splice方法的本质就是：第一个参数为起始位置，第二个参数为删除的项数，第三个参数为插入的项；

根据这个原理，splice可以实现三种功能：删除，插入，替换



#### 8.1.7 位置方法

**indexOf**()和**lastIndexOf**()

indexOf方法和lastIndexOf方法接受两个参数——要查找的项和表示查找起点位置的索引（可选）。其中，indexOf从数组的开头开始向后查找，而lastIndexOf从数组的结尾开始向前查找。

这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回-1。

```js
var arr = [1,2,3,4,5,4,3,2,1]

console.log(arr.indexOf(4))//3
console.log(arr.lastIndexOf(4))//5
console.log(arr.indexOf(4,4))//5
console.log(arr.lastIndexOf(4,4))//3
```

在比较第一个参数与数组中的每一项时，会使用全等操作符，也就是说，要求查找的项必须严格相等，就像使用===一样。看下面的例子：

```js
var person = {name:'李琳琦'}
var people = [{name:'李琳琦'}]

console.log(people.indexOf(person))//-1

var morePeople = [person]

console.log(morePeople.indexOf(person))//0
```





#### 8.1.8 迭代方法

##### forEach()

- 语法：

  ```javascript
  array.forEach(function(currentValue, index, arr))
  ```

- 说明：

  - currentValue：数组当前项的值

  - index：数组当前项的索引

  - arr：数组对象本身

- 举例：

  ```javascript
  // forEach 迭代(遍历) 数组
  var arr = [1, 2, 3];
  var sum = 0;
  arr.forEach(function(value, index, array) {
  	console.log('每个数组元素' + value);
  	console.log('每个数组元素的索引号' + index);
  	console.log('数组本身' + array);
  	sum += value;
  })
  console.log(sum);
  ```



##### some()

- 语法：

  ```javascript
  array.some(function(currentValue, index, arr))
  ```

- 说明：

  - some() 方法用于检测数组中的元素是否满足指定条件.   通俗点 查找数组中是否有满足条件的元素 

  - 注意它**返回值是布尔值**, 如果查找到这个元素, 就返回true ,  如果查找不到就返回false.

  - 如果找到第一个满足条件的元素,则终止循环. 不在继续查找.

  - currentValue: 数组当前项的值

  - index：数组当前项的索引

- 例子：

  ```javascript
  some 查找数组中是否有满足条件的元素 
  var arr = [10, 30, 4];
  var flag = arr.some(function(value) {
  	return value < 3;
  });
  console.log(flag);//false
  ```



##### forEach和some方法的区别：

1. **forEach：**

   ```javascript
   var arr = ['red', 'green', 'blue', 'pink'];
   // 1. forEach迭代 遍历
   arr.forEach(function(value) {
   	if (value == 'green') {
   		console.log('找到了该元素');
   		return true; // 在forEach 里面 return 不会终止迭代
   	}
   	console.log(11);
   })
   ```

​	看上面的这一段代码，输出结果为：11、找到了该元素、11（2次）

​	证明在forEach遍历中，一定要遍历完所有的元素，才可以终止迭代。

2. **some：**

   ```javascript
   arr.some(function(value) {
   	if (value == 'green') {
   		console.log('找到了该元素');
   		return true; //  在some 里面 遇到 return true 就是终止遍历 
   	}
   	console.log(11);
   
   });
   ```

   这段代码输出结果为：11、找到了该元素。

   在some 里面，**遇到 return true 就是终止遍历，迭代效率更高。**



##### filter()

- 语法：

  ```javascript
  array.filter(function(currentValue, index, arr))
  ```

- 说明：

  - filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素,主要用于筛选数组
  - **注意它直接返回一个新数组**
  - currentValue: 数组当前项的值
  - index：数组当前项的索引
  - arr：数组对象本身

- 注意：

  - filter中的回调函数有一个要求: 必须返回一个**boolean**值

  - true: **当返回true时, 函数内部会自动将这次回调的 currentValue 加入到新的数组中**

  - false: **当返回false时, 函数内部会过滤掉这次的 currentValue**

- 例子：

  ```javascript
  // filter 筛选数组
  var arr = [12, 66, 4, 88, 3, 7];
  var newArr = arr.filter(function(value, index) {
  	// return value >= 20;
  	return value % 2 === 0;
  });
  console.log(newArr);
  ```



##### map()

map() 方法也是创建一个数组，新数组中的元素是通过回调函数的返回值决定的。

如：

```javascript
const num = [1,2,3]
let newNum = num.map(function(currentValue) {
	return currentValue * 2
})
console.log(newNum)//[2,4,6]
```



#### reduce()

先来看reduce的一个例子：

```javascript
const num = [1,2,3]
let newNum = num.reduce(function(preValue, currentValue){
    return preValue + currentValue
},0)
```

reduce() 常用于对数组中所有的元素进行汇总，上述代码中 **preValue 指的是前一次遍历中的 return 值**，**可以设置它的初始值（如上述代码中初始值为0 ）**。

上述代码的含义就是对数组进行了求和（好好体会 ）



#### filter() map() reduce() 结合小案例

```javascript
const nums = [10, 20, 111, 222, 444, 40, 50]

let total = nums.filter(value => value < 100).map(value => value * 2).reduce((preValue, value) => preValue + value)

console.log(total);
```



#### 8.1.8 商品查询案例

（待完善）



### 8.2 字符串方法

#### 8.2.1 trim()

- 语法：

  ```javascript
  str.trim()
  ```

- 说明：

  - trim()  方法会从一个字符串的**两端**删除空白字符；
  - trim() 方法并不影响原字符串本身，它返回的是一个新的字符串。

- 举例：

  ```javascript
  var str = '   an  dy   ';
  var str1 = str.trim();
  console.log(str1);//an  dy
  console.log(str);//   an  dy   
  ```



### 8.3 对象方法

#### 8.3.1 Object.keys()

- 语法：

  ```javascript
  Object.keys(obj)
  ```

- 说明：

  - Object.keys() 用于获取对象自身所有的属性；
  - 效果类似for...in...；
  - 返回一个由属性名组成的数组。

- 举例：

  ```javascript
  var obj = {
  	id: 1,
  	pname: '小米',
  	price: 1999,
  	num: 2000
  };
  var arr = Object.keys(obj);//[id, pname, price, num]
  console.log(arr);
  arr.forEach(function(value) {
  	console.log(value);
  })
  ```

  

#### 8.3.2 Object.defineProperty()——Vue中常用

- 语法：

  ```javascript
  Object.defineProperty(obj, prop, descriptor)
  ```

- 说明：

  - Object.defineProperty() 定义对象中新属性或修改原有的属性。(了解)
  - obj：必需。目标对象 
  - prop：必需。需定义或修改的属性的名字
  - descriptor：必需。目标属性所拥有的特性
    - 以对象形式{ } 书写descriptor：
      - value: 设置属性的值  默认为undefined
      - writable: 值是否可以重写。true | false  默认为false
      - enumerable: 目标属性是否可以被枚举。true | false 默认为 false
      - configurable: 目标属性是否可以被删除或是否可以再次修改特性 true | false  默认为false

- 举例：

  假如有一个对象：

  ```javascript
  var obj = {
  	id: 1,
  	pname: '小米',
  	price: 1999
  };
  ```

  在以前我们添加或修改属性的方式如下：

  ```javascript
  obj.num = 1000;//添加
  obj.price = 99;//修改
  ```

  在ES5中的Object.defineProperty()方法中，可以这么修改：

  ```javascript
  Object.defineProperty(obj, 'num', {
  	value: 1000,
  	enumerable: true
  });
  console.log(obj);
  Object.defineProperty(obj, 'price', {
  	value: 9.9
  });
  ```

  descriptor中其他特性：

  ```javascript
  Object.defineProperty(obj, 'address', {
  	value: '中国山东蓝翔技校xx单元',
  	// 如果writable值为false 不允许修改这个属性值 默认值也是false
  	writable: true,
  	// enumerable 如果值为false 则不允许遍历, 默认的值是 false
  	enumerable: true,
  	// configurable 如果为false 则不允许删除这个属性，不允许再次修改第三参数中的特性，默认为false
  	configurable: true
  });
  ```

  

## 九、拷贝

- 浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用地址
- 深拷贝拷贝多层，每一级别的数据都会拷贝

### 9.1 浅拷贝

```js
let obj = {
  id: 1,
  name: '李琳琦',
  message: {
    age: 18
  }
}

let o = {}

// for in 实现浅拷贝
for (k in obj) {
  o[k] = obj[k]
}

//通过对象o修改深层属性值
o.message.age = 20
console.log(o)//age=20
console.log(obj)//age=20
```

- 浅拷贝可以通过for...in...的方式来实现

- 浅拷贝只是拷贝一层，更深层次的只是拷贝引用地址，因此通过其中任何一个对象修改深层属性的属性值时，每个对象的属性值都会被改变（注意，修改第一层的属性值是互不影响的）

  ![](./images/javascript/浅拷贝.png)

- 在**ES6**中，我们还可以通过另一种更加推荐的方式来实现浅拷贝：

  ```js
  let obj = {
    id: 1,
    name: '李琳琦',
    message: {
      age: 18
    }
  }
  let o = {}
  // Object.assign 实现浅拷贝
  Object.assign(o, obj)
  ```

  - **Object.assign**接受两个参数，一个是拷贝的对象，一个是被拷贝的对象
  - **Object.assign**的实现结果和for...in...的实现结果是一模一样的



### 9.2 深拷贝

- 深拷贝拷贝多层，每一级别的数据都会拷贝 

- 实现的思路是封装一个深拷贝的函数，通过if判断类型，递归调用函数

- 分别判断数组、对象、普通数据类型，注意数组的判断要放在对象的判断之前，因为数组也是对象

- 修改深层属性的属性值，原对象不会受影响

  ![](./images/javascript/深拷贝.png)

```js
// 深拷贝拷贝多层, 每一级别的数据都会拷贝.
var obj = {
    id: 1,
    name: 'andy',
    msg: {
        age: 18
    },
    color: ['pink', 'red']
};
var o = {};
// 封装函数 
function deepCopy(newobj, oldobj) {
    for (var k in oldobj) {
        // 判断我们的属性值属于哪种数据类型
        // 1. 获取属性值  oldobj[k]
        var item = oldobj[k];
        // 2. 判断这个值是否是数组
        if (item instanceof Array) {
            newobj[k] = [];
            deepCopy(newobj[k], item)
        } else if (item instanceof Object) {
            // 3. 判断这个值是否是对象
            newobj[k] = {};
            deepCopy(newobj[k], item)
        } else {
            // 4. 属于简单数据类型
            newobj[k] = item;
        }

    }
}
deepCopy(o, obj);
console.log(o);

o.msg.age = 20;
console.log(obj);
```





# 同步与异步

## 一、为什么JavaScript是单线程？

JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。那么，为什么JavaScript不能有多个线程呢？这样能提高效率啊。

JavaScript的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？

所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变。

为了利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程，但是子线程完全受主线程控制，且不得操作DOM。所以，这个新标准并没有改变JavaScript单线程的本质。

## 二、同步与异步任务

JavaScript 单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。

如果排队是因为计算量大，CPU忙不过来，倒也算了，但是很多时候CPU是闲着的，因为IO设备（输入输出设备）很慢（比如Ajax操作从网络读取数据），不得不等着结果出来，再往下执行。

JavaScript语言的设计者意识到，这时主线程完全可以不管IO设备，挂起处于等待中的任务，先运行排在后面的任务。等到IO设备返回了结果，再回过头，把挂起的任务继续执行下去。

于是，所有任务可以分成两种，一种是**同步任务（synchronous）**，另一种是**异步任务（asynchronous）**。同步任务指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；异步任务指的是，不进入主线程、而进入**"任务队列"（task queue）**的任务，只有"任务队列"通知主线程，某个异步任务可以执行了，该任务才会进入主线程执行。

具体来说，异步执行的运行机制如下。（同步执行也是如此，因为它可以被视为没有异步任务的异步执行。）

```
（1）所有同步任务都在主线程上执行，形成一个[执行栈]（execution context stack）。

（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。

（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。

（4）主线程不断重复上面的第三步。
```

只要主线程空了，就会去读取"任务队列"，这就是JavaScript的运行机制。这个过程会不断重复。

## 三、事件和回调函数

"任务队列"是一个事件的队列（也可以理解成消息的队列），IO设备完成一项任务，就在"任务队列"中添加一个事件，表示相关的异步任务可以进入"执行栈"了。主线程读取"任务队列"，就是读取里面有哪些事件。

"任务队列"中的事件，除了IO设备的事件以外，还包括一些用户产生的事件（比如鼠标点击、页面滚动等等）。只要指定过回调函数，这些事件发生时就会进入"任务队列"，等待主线程读取。

**所谓"回调函数"（callback），就是那些会被主线程挂起来的代码。异步任务必须指定回调函数，当主线程开始执行异步任务，就是执行对应的回调函数。**

"任务队列"是一个先进先出的数据结构，排在前面的事件，优先被主线程读取。主线程的读取过程基本上是自动的，只要执行栈一清空，"任务队列"上第一位的事件就自动进入主线程。但是，由于存在后文提到的"定时器"功能，主线程首先要检查一下执行时间，某些事件只有到了规定的时间，才能返回主线程。

## 四、Event Loop

主线程从"任务队列"中读取事件，这个过程是循环不断的，所以整个的这种运行机制又称为**Event Loop**（事件循环）。见下图：

![eventLoop](D:\52007前端学习\前端笔记\images\JavaScript\eventLoop.png)

上图中，主线程运行的时候，产生堆（heap）和栈（stack），栈中的代码调用各种外部API，它们在"任务队列"中加入各种事件（click，load，done）。只要栈中的代码执行完毕，主线程就会去读取"任务队列"，依次执行那些事件所对应的回调函数。

## 五、setTimeout案例分析

我们来看一个setTimeout案例：

```JavaScript
setTimeout(function(){
	console.log("setTimeout");
},3000);
console.log("哈哈代码");
```

在上面这段代码中，很容易想象到是先输出”哈哈代码“，再过3秒输出”setTimeout“。事实上也是如此。

这时候可能就会有人认为，这是因为setTimeout有3秒钟的延时，因此输出比“哈哈代码”要慢是正常的。

那么我们来对代码做一个简单的修改：

```javascript
setTimeout(function(){
	console.log("setTimeout");
},0);

for(var i=0;i<100000;i++){
	 i += i;
}
console.log("哈哈代码");
```

在这段代码中，我将定时器的时间改为0，并且在中间加入了一段较为耗时的for循环。

按照道理来讲，JavaScript是从上到下执行的，应该是先输出“setTimeout”，然后经过一段时间（for循环的时间）后输出“哈哈代码”才是。

但事与愿违，实际上的结果是：先隔一段时间（执行for循环），再输出“哈哈代码”，然后才是“setTimeout”。

这是为什么呢？

实际上，我们在上面提到的js同步异步的知识已经可以理解这个现象了。

我是这么理解的，setTimeout实际上在主线程中，只是将回调函数放入任务队列中，然后它就功成身退了。js主线程继续往下执行→for循环→“哈哈代码”。

在js主线程执行完全部的代码后，即空闲时，它会查看任务队列，有没有需要执行的任务。此时它就发现了一名“弃婴”，即setTimeout的回调函数，执行函数。另外，任务队列是队列，因此是先进先出的，先进来的任务，就先完成。

![同步异步setTimeout](D:\52007前端学习\前端笔记\images\javascript\同步异步setTimeout.png)

这样的机制在回调函数里面也是适用的，如下代码：

```javascript
setTimeout(function(){
	setTimeout(function(){
		console.log("setTimeout02");
	},3000);
	console.log("setTimeout");
},3000);

var str = "";
for(var i=0;i<1000000;i++){
	 str += i;
}
console.log("哈哈代码");
```

输出结果是：先隔一段时间（执行for循环）→哈哈代码→“setTimeout”→“setTimeout02”。

我们可以知道在setTimeout的回调函数里面，他也是按照这样的机制来执行代码的。





# ES6规范

ES 的全称是 ECMAScript , 它是由 ECMA 国际标准化组织,制定的一项脚本语言的标准化规范。

ES6 实际上是一个泛指，泛指  ES2015 及后续的版本。 

## 为什么使用ES6？

每一次标准的诞生都意味着语言的完善，功能的加强。JavaScript语言本身也有一些令人不满意的地方。

- 变量提升特性增加了程序运行时的不可预测性
- 语法过于松散，实现相同的功能，不同的人可能会写出不同的代码



## let关键字

- ES6中新增的用于**声明变量**的关键字

- let声明的变量只在所处于的块级有效
- 使用let关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性

```javascript
if (true){
	let a = 10;
}
console.log(a); //ReferenceError: a is not defined
```

- 特点：

  - 不存在变量提升

    ```javascript
    a = 1
    console.log(a)//ReferenceError: Cannot access 'a' before initialization
    let a
    ```

    

  - 暂时性死区

    ```javascript
    var tmp = 123;
    if(true){
    	tmp = 'abc';
    	let tmp;
    } //ReferenceError: Cannot access 'tmp' before initialization
    ```
  
- 经典面试题：

  **Q1：请问下面代码输出结果是什么？**

  ```javascript
   var arr = [];
   for (var i = 0; i < 2; i++) {
       arr[i] = function () {
           console.log(i); 
       }
   }
  
   arr[0](); //2
   arr[1](); //2
  ```

此题的关键点在于变量i是全局的，函数执行时输出的都是全局作用域下的i值。



  	**Q2 ：请问下面代码输出结果是什么？**

  ```javascript
   let arr = [];
   for (let i = 0; i < 2; i++) {
       arr[i] = function () {
           console.log(i); 
       }
   }
   arr[0](); //0
   arr[1](); //1
  ```

此题的关键点在于每次循环都会产生一个块级作用域，每个块级作用域中的变量都是不同的，函数执行时输出的是自己上一级（循环产生的块级作用域）作用域下的i值.



## const关键字

- 作用：声明常量，常量就是值（内存地址）不能变化的量。

- 特点：

  - 具有块级作用域

    ```javascript
    if(true){
    	const a = 10;
    }
    console.log(a); //ReferenceError: a is not defined
    ```

  - 声明常量时必须赋值

    ```javascript
    const PI; //SyntaxError: Missing initializer in const declaration
    ```

  - 常量赋值后，值（内存地址）不能修改

    ```javascript
    const PI = 3.14;
    PI = 10; //Assignment to constant variable.
    ```

    这里所说的值不能修改，其实指的是内存地址不能修改。我们来看下面这个数组的例子：

    ```javascript
    const arr = [100,200];
    arr[0] = 1;
    arr[1] = 2;
    console.log(arr); //[1,2]
    arr = [3,4]; //Assignment to constant variable.
    ```

    可见，我们可以修改数组里面的数值，但是不能修改数组的内存地址。
    
    **其实，在ES6中，常量的含义是指向的对象不能修改，但是可以改变对象内部的属性。**

### var、let、const 对比：

| **var**      | **let**        | **const**      |
| ------------ | -------------- | -------------- |
| 函数级作用域 | 块级作用域     | 块级作用域     |
| 变量提升     | 不存在变量提升 | 不存在变量提升 |
| 值可更改     | 值可更改       | 值不可更改     |



## 对象字面量的增强写法

### 属性的增强写法

- ES5中：

  ```javascript
  const name = "Kobe";
  const age = "18";
  const obj = {
  	name: name,
  	age: age
  }
  ```

  

- ES6中字面量增强写法：

  ```javascript
  const name = "Kobe";
  const age = "18";
  const obj = {
  	name,
  	age
  }
  ```

  

### 函数的增强写法

- ES5中：

  ```javascript
  const obj = {
  	run: function () {
  	
  	},
  	eat: function () {
  	
  	}
  }
  ```

  

- ES6中：

  ```javascript
  const obj = {
  	run () {
  	
  	},
  	eat () {
  	
  	}
  }
  ```

  



## 解构赋值

按照一定模式，从数组中或对象中提取值，将提取出来的值赋值给另外的变量。

### 数组解构

```javascript
let [a,b,c] = [1,2,3];
console.log(a); //1
console.log(b); //2
console.log(c); //3
```

如果解构不成功，变量的值为undefined：

```javascript
let [a] = [];
console.log(a); //undefined
let [b,c] = [1];
console.log(b); //1
console.log(c); //undefined
```



### 对象解构

```javascript
 let person = { name: 'zhangsan', age: 20 }; 
 let { name, age } = person;
 console.log(name); // 'zhangsan' 
 console.log(age); // 20
```



```javascript
let {name: myName, age: myAge} = person; // myName myAge 属于别名
 console.log(myName); // 'zhangsan' 
 console.log(myAge); // 20
```



## 箭头函数

ES6 中新增函数定义方式：箭头函数

```javascript
() => {} 
const fn = () => {}
```

其中，fn 是函数名，小括号内是形参，大括号内是函数体。

- 函数体中**只有一句代码**，**且代码的执行结果就是返回值**，可以省略大括号

  如下面两种写法都可以表示一个返回加法结果的函数：

  ```javascript
  function sum(num1, num2) { 
       return num1 + num2; 
   }
   const sum = (num1, num2) => num1 + num2; 
  ```

  

- 如果形参只有一个，可以省略小括号

  例如：

  ```javascript
   function fn (v) {
       return v;
   } 
   const fn = v => v;
  ```

  

### 箭头函数中的this

箭头函数不绑定this关键字，箭头函数中的this，指向的是函数定义位置的上下文this。即向外层作用域中, 一层层查找this, 直到有this的定义.

如：

```javascript
function fn (){
	console.log(this);
	return () => {
		console.log(this);
	}
}
const obj = { name:'zhangsan' };
const refn = fn.call(obj); //obj
refn(); //obj
```



### 箭头函数经典面试题

1. 

   ```javascript
   var age = 100;
   
   var obj = {
   	age: 20,
   	say: () => {
           console.log(this)//window
   		alert(this.age)//100
   	}
   }
   
   obj.say();
   ```

   上面这段代码的输出结果是100。
   
   我们说箭头函数不绑定this，因此在调用 say 属性中的箭头函数时如果不指定this，那么this指向window。而window中的age是100。



2. 

   ```javascript
   const obj = {
     aaa() {
         console.log(this)//obj
       setTimeout(function () {
         setTimeout(function () {
           console.log(this); // window
         })
   
         setTimeout(() => {
           console.log(this); // window
         })
       })
   
       setTimeout(() => {
         setTimeout(function () {
           console.log(this); // window
         })
   
         setTimeout(() => {
           console.log(this); // obj
         })
       })
     }
   }
   
   obj.aaa()
   ```




## 剩余参数

剩余参数语法允许我们将一个不定数量的参数表示为一个数组。

```javascript
function fn(a,...b){
	console.log(a); //1
	console.log(b); //[2,3,4]
}
fn(1,2,3,4);
```

剩余参数可以和解构配合使用：

```javascript
let students = ['张三','李四','王五'];
let [a,...b] = students;
console.log(a); //张三
console.log(b); //["李四", "王五"]
```



## ES6内置对象扩展

### 数组的扩展方法

#### ...扩展运算符

扩展运算符可以将数组或者对象转为**用逗号分隔的参数序列**。

```
let arr = [1,2,3];
console.log(...arr); // 1 2 3
```

- 应用1：数组拼接

```

let arr1 = [1,2,3];
let arr2 = [4,5,6];
let arr3 = [...arr1, ...arr2];
console.log(arr3); //[1,2,3,4,5,6]
```

  

- 应用2：将类数组转化为真正的数组

  ```javascript
  let oDivs = document.getElementsByTagName('div'); 
  oDivs = [...oDivs];
  ```

  

#### 构造函数方法：Array.from（）

- 将类数组或可遍历对象转换为真正的数组

  ```javascript
  let arrLike = {
  	'0': 'a',
  	'1': 'b',
  	'2': 'c',
  	length: 3
  }
  let arr = Array.from(arrLike);
  console.log(arr); //['a','b','c']
  ```

  

- 方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组

  ```javascript
  let arrLike = {
  	'0': '1',
  	'1': '2',
  	'2': '3',
  	length: 3
  }
  
  let arr = Array.from(arrLike, item => item*2 )
  console.log(arr); //[2,4,6]
  ```

  

#### 实例方法 find()

作用：用于找出**第一个**符合条件的数组成员，如果没有找到返回undefined

```javascript
let arr = [{
	id: 1,
	name: 'zhangsan'
},{
	id: 2,
	name: 'lisi'
}];
let target = arr.find( (item,index) => item.id == 2);
console.log(target.name); //lisi
```



#### 实例方法 findIndex()

用于找出**第一个**符合条件的数组成员的位置，如果没有找到返回-1

```javascript
let arr = [1,10,30,40];
let index = arr.findIndex( value => value > 20);
console.log(index); //2
```



#### 实例方法 includes()

表示某个数组是否包含给定的值，返回布尔值。

```javascript
[1, 2, 3].includes(2) // true 
[1, 2, 3].includes(4) // false
```



### string 的扩展方法

#### 模板字符串``

ES6新增的创建字符串的方式，使用反引号定义。

```javascript
let name = `zhangsan`;
```

1. 模板字符串中可以解析变量

```javascript
let name = '李琳琦';
let sayLove = `我喜欢${name}`;
console.log(sayLove); //我喜欢李琳琦
```

2. 模板字符串中可以换行

```javascript
let obj = {
	name: '张三',
	age: 20,
	sex: '男'
}
let html = `<div>
	<span>${obj.name}</span>
	<span>${obj.age}</span>
	<span>${obj.sex}</span>
</div>`;
console.log(html);
/* 
<div>
	<span>张三</span>
	<span>20</span>
	<span>男</span>
</div> 
 */
```

3. 在模板字符串中可以调用函数

```javascript
let sayHaha = () => '哈哈哈哈';
let result = `我太帅了${sayHaha()}`;
console.log(result); //我太帅了哈哈哈哈
```



#### startsWith() 和 endsWith()

- startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值

- endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值

```javascript
 let str = 'Hello world!';
 str.startsWith('Hello') // true 
 str.endsWith('!')       // true
```



#### repeat()

repeat方法表示将原字符串重复n次，返回一个新字符串。

```javascript
let name = '李琳琦';
console.log(name.repeat(3)); //李琳琦李琳琦李琳琦
```



## Set 数据结构

ES6 提供了新的数据结构  Set。它类似于数组，但是成员的值都是**唯一**的，没有重复的值。

### 实例化

- Set本身是一个构造函数，用来生成  Set 数据结构

  ```javascript
  const s = new Set();
  ```

- Set函数可以接受一个**数组**作为**参数**，用来**初始化**。

  ```javascript
  const set = new Set([1, 2, 3, 4, 4]);
  console.log(set); //[1,2,3,4]
  ```

### 实例方法

- add(value)：添加某个值，返回 Set 结构本身
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功
- has(value)：返回一个布尔值，表示该值是否为 Set 的成员
- clear()：清除所有成员，没有返回值

```javascript
const s = new Set([1,2,3,4]);
s.add(3).add(4).add(5);
console.log(s); //Set(5) {1, 2, 3, 4, 5}
console.log(s.delete(4)); //true
console.log(s.has(4)); //false
s.clear();
console.log(s); //Set(0) {}
```

### Set 遍历

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，**没有返回值**。

```javascript
s.forEach(value => console.log(value))
```



## Promise

### 传统异步处理的弊端

Promise 是异步编程的一种解决方案

什么时候我们会来处理异步事件呢？

一种很常见的场景应该就是网络请求了。

假如我们封装一个网络请求的函数，因为不能立即拿到结果，所以不能像简单的3+4=7一样将结果返回。所以往往我们会传入另外一个函数，在数据请求成功时，将数据通过传入的函数回调出去。

如果只是一个简单的网络请求，那么这种方案不会给我们带来很大的麻烦。但是，当网络请求非常复杂时，就会出现**回调地狱**。比如如下的一个场景(比较夸张的例子)：

```JavaScript
$.ajax('url1', function(data1) {
  $.ajax(data1['url2'], function(data2) {
    $.ajax(data2['url3'], function(data3) {
      $.ajax(data3['url4'], function(data4) {
        console.log(data4);
      })
    })
  })
})
```

在上面的例子中，

- 我们需要通过一个url1从服务器加载一个数据data1，data1中包含了下一个请求的url2

- 我们需要通过data1取出url2，从服务器加载数据data2，data2中包含了下一个请求的url3

- 我们需要通过data2取出url3，从服务器加载数据data3，data3中包含了下一个请求的url4

- 发送网络请求url4，获取最终的数据data4

这样的代码难看而且不容易维护，我们更加期望的是一种更加优雅的方式来进行这种异步操作。**Promise 就可以以一种非常优雅的方式来解决这个问题。**



### Promise 的基本使用

我们用一个定时器来模拟异步事件，假设下面的 data 是从网络上2秒后请求的数据，console.log 就是我们的处理方式：

```JavaScript
setTimeout(() => {
  let data = 'hahaha'
  console.log(data);
},2000)
```



这是我们过去的处理方式，我们将它换成 Promise 代码：

```JavaScript
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success')
    reject('error')
  },2000)
}).then(data => {
  console.log(data);
}).catch(data => {
  console.log(data);
})
```

这个例子会让我们感觉脱裤放屁，多此一举，但是在之后的学习和运用中会发现这种**链式编程**是很实用的。

- Promise 是类，需要用 **new** 来实例化

- Promise 的参数是一个**函数**(一般用箭头函数书写)，在这个函数中一般有两个**参数，resolve/reject**

- resolve 和 reject 也是函数，通常情况下，我们会根据请求数据的成功和失败来决定调用哪一个：

  - 如果是**成功**的，那么通常我们会调用**resolve(success)**，这个时候，我们后续的**then**会被回调。

  - 如果是**失败**的，那么通常我们会调用**reject(error)**，这个时候，我们后续的**catch**会被回调。 

这就是 Promise 的基本使用了。



### Promise 的三种状态

当我们开发中有异步操作时, 就可以给异步操作包装一个Promise

异步操作之后会有三种状态：

1. **pending**：**等待状态**，比如正在进行网络请求，或者定时器没有到时间。

2. **fulfilled**：**满足状态**，当我们主动回调了resolve时，就处于该状态，并且会回调.then()

3. **rejected**：**拒绝状态**，当我们主动回调了reject时，就处于该状态，并且会回调.catch()

![Promise的三种状态](D:\52007前端学习\前端笔记\images\javascript\Promise的三种状态.png)

### Promise 的链式调用

我们在看Promise的流程图时，发现**无论是then还是catch都可以返回一个Promise对象**。所以，我们的代码其实是可以进行**链式调用**的：

```JavaScript
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('li')
  },1000)
}).then(data => {
  console.log(data)//li
  return new Promise((resolve, reject) => {
    resolve(data + 'lin')
  })
}).then(data => {
  console.log(data);//lilin
  return Promise.resolve(data + 'qi')
}).then(data => {
  console.log(data)//lilinqi
  return Promise.reject(data + 'dashabi')
}).then(data => {
  console.log(data)//不会有打印
  return Promise.resolve(data + 'dashazhu')
}).catch(data => {
  console.log(data)//lilinqidashabi
  return Promise.resolve(data + '傻逼')
}).then(data => {
  console.log(data)//lilinqidashabi傻逼
})
```

在上面的第12行中，我们直接通过Promise包装了一下新的数据，将Promise对象返回了

- Promise.resovle()：将数据包装成Promise对象，并且在内部回调resolve()函数

- Promise.reject()：将数据包装成Promise对象，并且在内部回调reject()函数

除此之外，链式调用中如果我们希望数据直接包装成Promise.resolve，那么在**return**时我们可以直接返回数据：

```javascript
then(data => {
  //return Promise.resolve(data + 'dashazhu')
  return data + 'dashazhu'
}）
```

如果数据直接包装成Promise.reject，那么在**throw**中可以直接返回数据：

```JavaScript
catch(data => {
  //return Promise.reject(data + 'dashazhu')
  throw data + 'dashazhu'
}）
```

结果依然是一样的。



### Promise 中 all 的用法

我们来假设一种场景，当有两个网络请求同时发送请求时，我们不知道哪一个先返回了数据，一般来说我们需要在各自的函数中定义一个变量 isTrue1 和 isTrue2，然后用if判断当两个变量都为true时执行一些代码：

```JavaScript
let isResult1 = false
let isResult2 = false
$ajax({
  url: '',
  success: function () {
    console.log('结果1');
    isResult1 = true
    handleResult()
  }
})
// 请求二:
$ajax({
  url: '',
  success: function () {
    console.log('结果2');
    isResult2 = true
    handleResult()
  }
})

function handleResult() {
  if (isResult1 && isResult2) {
    //
  }
}
```

但是这样不仅麻烦，代码也不够优雅。

Promise 中提供了一个 all 属性，优雅地解决了这个问题：

```JavaScript
Promise.all([
  new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('True1')
    }, 1000)
  }),
  new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('True2')
    }, 2000);
  })
]).then(results => {
  console.log(results)//["True1", "True2"]
  console.log(results[0])//True1
  console.log(results[1])//True2
})
```

Promise.all() 中需要传入参数，参数是一个可以迭代的对象，比如数组。

在数组中我们可以 new 若干个Promise，并统一用then处理，此时then拿到的数据是一个数组，数组下标对应着all参数数组中的Promise对象。