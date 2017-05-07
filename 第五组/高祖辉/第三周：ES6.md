## ES6
### class基本语法
	1、ES6提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。
```
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
typeof Point // "function"
Point === Point.prototype.constructor // true
上面代码定义了一个“类”，可以看到里面有一个constructor方法，这就是构造方法，而this关键字则代表实例对象。也就是说，ES5的构造函数Point，对应ES6的Point类的构造方法。
上面代码表明，类的数据类型就是函数，类本身就指向构造函数。
```
	2、使用的时候，也是直接对类使用new命令，跟构造函数的用法完全一致。
	构造函数的prototype属性，在ES6的“类”上面继续存在。事实上，类的所有方法都定义在类的prototype属性上面。
```
class Point {
  constructor(){
    // ...
  }
  toString(){
    // ...
  }
  toValue(){
    // ...
  }
}
// 等同于
Point.prototype = {
  toString(){},
  toValue(){}
};
```
	3、由于类的方法都定义在prototype对象上面，所以类的新方法可以添加在prototype对象上面。Object.assign方法可以很方便地一次向类添加多个方法。
```
class Point {
  constructor(){
    // ...
  }
}
Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});
```
	类的内部所有定义的方法，都是不可枚举的（non-enumerable）。
```
class Point {
  constructor(x, y) {
    // ...
  }
  toString() {
    // ...
  }
}
Object.keys(Point.prototype)//Object.keys将可枚举属性名放在一个数组中
// []
Object.getOwnPropertyNames(Point.prototype)
// ["constructor","toString"]
```
	类的属性名，可以采用表达式。
```
let methodName = "getArea";
class Square{
  constructor(length) {
    // ...
  }
  [methodName]() {
    // ...
  }
}
```
#### constructor方法
	1、constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加。
	2、constructor方法默认返回实例对象（即this），但是可以指定返回另外一个对象。从而导致实例对象不是类的实例
#### 类的实例对象
	1、类的构造函数，不使用new是没法调用的，会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。
	2、与ES5一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。
	3、与ES5一样，类的所有实例共享一个原型对象，都是Point.prototype，__proto__属性是相等的。可以通过__proto__属性为Class添加方法
#### 不存在变量提升
	Class不存在变量提升（hoist），这一点与ES5完全不同，必须保证子类在父类之后定义。
#### class表达式
```
const MyClass = class Me {
  getClassName() {
    return Me.name;
  }
};
let inst = new MyClass();
inst.getClassName() // Me
Me.name // ReferenceError: Me is not defined
这个类的名字是MyClass而不是Me，Me只在Class的内部代码可用，指代当前类。
Me只在Class内部有定义。
```
	如果类的内部没用到的话，可以省略Me，也就是可以写成下面的形式。const MyClass = class { /* ... */ };
#### class的继承
>- Class之间可以通过extends关键字实现继承。class ColorPoint extends Point {}，定义了一个ColorPoint类，该类通过extends关键字，继承了Point类的所有属性和方法。但是由于没有部署任何代码，所以这两个类完全一样，等于复制了一个Point类。
```
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }
  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}
1、constructor方法和toString方法之中，都出现了super关键字，它在这里表示父类的构造函数，用来新建父类的this对象。
2、子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。
```
>- 1、ES5的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。ES6的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。
>- 2、如果子类没有定义constructor方法，这个方法会被默认添加，代码如下。也就是说，不管有没有显式定义，任何一个子类都有constructor方法。
```
constructor(...args) {
  super(...args);
}
```
>- 3、在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错。这是因为子类实例的构建，是基于对父类实例加工，只有super方法才能返回父类实例。
```
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
}
class ColorPoint extends Point {
  constructor(x, y, color) {
    this.color = color; // ReferenceError
    super(x, y);
    this.color = color; // 正确
  }
}
```
#### 类的prototype属性和__proto__属性
	Class作为构造函数的语法糖，同时有prototype属性和__proto__属性，因此同时存在两条继承链。
	(1)子类的__proto__属性，表示构造函数的继承，总是指向父类。
	(2)子类prototype属性的__proto__属性，表示方法的继承，总是指向父类的prototype属性。
```
class A {
}
class B extends A {
}
B.__proto__ === A // true
B.prototype.__proto__ === A.prototype // true
```
```
class A {
}
class B {
}
// B的实例继承A的实例
Object.setPrototypeOf(B.prototype, A.prototype);
const b = new B();

// B的实例继承A的静态属性
Object.setPrototypeOf(B, A);
const b = new B();
```
```
>- Object.setPrototypeOf方法的实现:
Object.setPrototypeOf = function (obj, proto) {
  obj.__proto__ = proto;
  return obj;
}
于是就有了下面的：
Object.setPrototypeOf(B.prototype, A.prototype);
// 等同于
B.prototype.__proto__ = A.prototype;

Object.setPrototypeOf(B, A);
// 等同于
B.__proto__ = A;
作为一个对象，子类（B）的原型（__proto__属性）是父类（A）；作为一个构造函数，子类（B）的原型（prototype属性）是父类的实例。

Object.create(A.prototype);
// 等同于
B.prototype.__proto__ = A.prototype;
```
#### extends的继承目标
	class B extends A{}，只要是一个有prototype属性的函数，就能被B继承。由于函数都有prototype属性（除了Function.prototype函数），因此A可以是任意函数。

```
（1）子类继承Object类。
class A extends Object {
}

A.__proto__ === Object // true
A.prototype.__proto__ === Object.prototype // true
A其实就是构造函数Object的复制，A的实例就是Object的实例

(2)不存在任何继承。
class A {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true

A作为一个基类（即不存在任何继承），就是一个普通函数，所以直接继承Funciton.prototype。但是，A调用后返回一个空对象（即Object实例），所以A.prototype.__proto__指向构造函数（Object）的prototype属性。

(3)子类继承null。
class A extends null {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === undefined // true

A也是一个普通函数，所以直接继承Funciton.prototype。但是，A调用后返回的对象不继承任何方法，所以它的__proto__指向Function.prototype，即实质上执行了下面的代码。
class C extends null {
  constructor() { return Object.create(null); }
}
Object.create(A.prototype)=function(){
	Function Fn(){}
	Fn.prototype=A.prototype;
	return new Fn;
}
```
#### Object.getPrototypeOf()
	Object.getPrototypeOf方法可以用来从子类上获取父类。Object.getPrototypeOf(ColorPoint) === Point  // true 因此，可以使用这个方法判断，一个类是否继承了另一个类。
	







### hasOwnProperty
>- 1、判断一个属性是定义在对象本身而不是继承自原型链，我们需要使用从` Object.prototype` 继承而来的 hasOwnProperty 方法。
>- 2、hasOwnProperty 方法是 Javascript 中唯一一个处理对象属性而不会往上遍历原型链的。
>- 3、Javascript 并未将 hasOwnProperty 设为敏感词，这意味着你可以拥有一个命名为 hasOwnProperty 的属性。这个时候你无法再使用本身的 hasOwnProperty 方法来判断属性，所以你需要使用外部的 hasOwnProperty 方法来进行判断。
>- 4、({}).hasOwnProperty.call(foo, 'bar')或者Object.prototype.hasOwnProperty.call(foo, 'bar')
### 可枚举属性
>-   在JavaScript中，对象的属性分为可枚举和不可枚举之分，它们是由属性的enumerable值决定的。可枚举性决定了这个属性能否被for…in查找遍历到。js中内置属性是遍历不到的。
>- ES5中提供了一个方法，用于遍历所有属性（不论是否是可枚举的）
```
Object.defineProperty(b,'age',{
value:18,
enumerable:false
});
Object.getOwnPropertyNames(b)；这样就得到了所有的属性
> ```
>- 定义Object对象的prototypeIsEnumerable()方法可以判断此对象是否包含某个属性，并且这个属性是否可枚举。如果判断的属性存在于Object对象的原型内，不管它是否可枚举都会返回false。