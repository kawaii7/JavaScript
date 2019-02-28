# JavaScriptt预编译

JavaScript执行分为三步  
第一步语法分析,通篇扫描,检查有没有语法错误  

第二步预编译(执行前一刻)  
预编译第一步形成一个 AO 对象(执行期上下文)  执行期上下文存储了由函数产生的一系列东西,第一步生成 AO,第二步找函数 里面的变量声明和形参,把函数声明的变量名作为 AO 对象的属性名,值为undefined  

第三步,形参实参相统一,把实参赋到形参里面去,第四步,找函数声明,  把函数名作为 AO 对象属性名,AO 对象的值就是函数体,把之前的覆盖  
   

     function test(a) {  
          var a = 123;  
          var b = 234;  
          
          function a() {  
         }  
          console.log(a)//123  
        }  
          
        test(1)
        
    第一步生成 AO  
    AO{ //第一步生成 AO  
    //第二步  
    a:undefined,  
    b:undefined,  
    //第三步  
    a:1,  
    b:undefined,  
    第四步  
    a:function a() {}, //把之前的覆盖  
    b:undefined,  
    }  
    第三步函数执行  
    函数执行过程中的所有变量赋值到 AO 里面去  
    AO{  
    a:123  
    b:234  
    }
