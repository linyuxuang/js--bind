# js--bind
js的内置方法 bind 硬绑定



   js的修改this的还有call，apply 这里不说它们
   
     bind 实现原理
     
       var objs={
          name:'jimes'
      }
      function test(age){
          console.log(this)  // {name: "jimes"}  test函数被绑定到objs对象里面
          console.log(this.name+":"+age) //jimes:35
      }
          function bind(fun,obj){
            return function(){
                return fun.apply(obj,arguments) 
            }
          }  
       var bar=bind(test,objs);
       bar(35)

   
      咋们用js自己分装的bind() 试试？
      
      注意：bind() 也可以实现？柯利华

       function fun1(age){
           console.log(this.name+":"+age) //jimes:89
       }


        var mybind=fun1.bind(objs,89)

          mybind()
        思考？ 
      
        
       function fun1(age,sex){
           console.log(this.name+":"+age+":"+sex) //jimes:89:女
       }
        var mybind=fun1.bind(objs,89)
        mybind("女")  
      
      
      
      
      
      
      
      
      
      
      
        
        
        
        
        
        
        
        
        
        
        
