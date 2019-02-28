## JavaScript继承
 许多 OO 语言都支持两种继承方式：接口继承和实现继承。接口继承只继承方 法签名，而实现继承则继承实际的方法。如前所述，由于函数没有签名，在 ECMAScript 中无法实现接口继承。ECMAScript 只支持实现继承，而且其实现继承主要是依靠原型 链来实现的。
首先必须得理解原型链: ECMAScript 中描述了原型链的概念，并将原型链作为实现继承的主要方法。其基本思想是利用原 型让一个引用类型继承另一个引用类型的属性和方法。
简单回顾一下构造函数、原型和实例的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指 针，而实例都包含一个指向原型对象的内部指针。那么，假如我们让原型对象等于另一 个类型的实例，结果会怎么样呢？显然，此时的原型对象将包含一个指向另一个原型的 指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原 型又是另一个类型的实例，那么上述关系依然然成立，如此层层递进，就构成了实例与原 型的链条。这就是所谓原型链的基本概念。
以一段代码为例：

    function Father() {  
      this.hobby = ["run", "basketball"];  
      this.job = "software engineer"  
    }  
      
    Father.prototype.address = "shanghai";  
    var Dad = new Father();  
      
      
    Son.prototype = Dad;  
    var son1 = new Son();  
    var son2 = new Son();
![enter image description here](https://github.com/kawaii7/JavaScript/blob/master/image/%E5%8E%9F%E5%9E%8B%E9%93%BE1.png)![enter image description here](https://github.com/kawaii7/JavaScript/blob/master/image/%E5%8E%9F%E5%9E%8B%E9%93%BE2.png)![enter image description here](https://github.com/kawaii7/JavaScript/blob/master/image/%E5%8E%9F%E5%9E%8B%E9%93%BE.jpg)

**原型链继承的问题:把父类的实例赋值给子类的原型这种原型链继承会导致所有子类型的实例共享属性**

    function Father() {  
      this.hobby = ["run", "basketball"];  
      this.job = "software engineer"  
    }  
      
    Father.prototype.address = "shanghai";  
      
    function Son() {  
    }  
      
    Son.prototype = new Father();  
    var son1 = new Son();  
    var son2 = new Son();  
      
    console.log(son1.hobby); //["run", "basketball"]  
    console.log(son2.hobby); //["run", "basketball"]  
      
    son2.hobby.push("drawing");  
    console.log(son1.hobby); //["run", "basketball", "drawing"]
**借用构造函数:在子类型构造函数的内部调用父类型构造函数。
问题：借用构造函数继承父类型构造函数里的方法都在构造函数中定 义, 因此函数复用就无从谈起了,而且父类型原型中的方法对子类型是不可见的**

    function Father(hobby) {  
      this.hobby = hobby;  
    }  
      
    Father.prototype.address = "shanghai";  
      
    function Son() {  
      Father.call(this, ["run", "basketball"])//可以传递参数  
    }  
      
    Son.prototype = new Father();  
    var son1 = new Son();  
    var son2 = new Son();  
    console.log(son1.hobby); //["run", "basketball"]  
    console.log(son2.hobby); //["run", "basketball"]  
    son2.hobby.push("drawing");  
    console.log(son1.hobby); //["run", "basketball"]  
    console.log(son2.hobby); //["run", "basketball", "drawing"]
