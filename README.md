# js--bind
js的内置方法 bind 硬绑定  -->软绑定



   js的修改this的还有call，apply 这里不说它们
   
     bind 实现原理 (这里写的只不过分装是一个简单的bind实现)
     
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
      
      注意：bind() 也可以实现？柯里化

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
      
      
      上面这些都是硬绑定？不是很灵活，看看下面咋们分装的软绑定
      
      
          var objs={
             name:'jimes'
         }

          Function.prototype.sofBind=function(obj){
              var _seft=this;
              var curried=[].slice.call(arguments,1)
              //return curried
               var bound=function(){
                   return _seft.apply(
                       (!this||this===(window||global)?obj:this),
                       curried.concat.apply(curried,arguments)
                       )
               }
             curried.prototype=Object.create(_seft.prototype);  
         return bound;
          }
          
          
         function test(age,sex){
              console.log(this.name+":"+age+":"+sex) //jimes:12:男
         }

        var mYbind=test.sofBind(objs,12)
          mYbind("男")

      
      
      
      
      
      
      
      
        
        
        
        
        
        
        
        
        
        
        
