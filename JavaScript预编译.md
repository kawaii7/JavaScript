# JavaScript预编译

JavaScript执行分为三步  
第一步语法分析,通篇扫描,检查有没有语法错误  

第二步预编译(执行前一刻)  
预编译第一步形成一个 AO 对象(执行期上下文)  执行期上下文存储了由函数产生的一系列东西,第一步生成 AO,第二步找函数 里面的变量声明和形参,把函数声明的变量名作为 AO 对象的属性名,值为undefined  

第三步,形参实参相统一,把实参赋到形参里面去
第四步,找函数声明,  把函数名作为 AO 对象属性名,AO 对象的值就是函数体,把之前的覆盖  

下面是一个例子:

    function fn(a) {  
      console.log(a);//a{..}  
      var a = 123;  
      console.log(a)//123  
      function a() {  
     }  
      console.log(a)//123  
      var b = function () {  
     }; 
      console.log(b)//(){..}  
    }  
      
    fn(1)
   
  **预编译发生在函数执行的前一刻**
**1.创建AO对象(Activation Object 执行期上下文)**

AO{

}

**2.找形参和变量声明,将变量和形参名作为AO属性名,值为undefined(就是变量声明提升的过程)**

AO{

a:undefined

b:undefined

}

**3.将实参值和形参统一**

AO{

a:1(值由undefined变成1)

b:undefined

}

**4.在函数体内找函数声明,值赋予函数体**

AO{

a:function a() {} (把之前的1覆盖掉)

b:undefined

}

***AO对象创建完成***

**执行函数...**

    function fn(a) {  
      console.log(a);//a{..}  *第一次拿a去AO里面拿*
      var a = 123;  		  *把AO对象的a改成123*
      console.log(a)//123  
      function a() {  
     }  
      console.log(a)//123  
      var b = function () {  *把AO里面b由undefined变成function(){}*
     }; 
      console.log(b)//(){..}  
    }  
      
    fn(1)
   
