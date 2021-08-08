# 《JS函数的执行时机》
## 为什么如下代码会打印 6 个 6
~~~
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
~~~
因为setTimeout的意思是做完手头上的事情后，立即做一件事情，所以setTimeout会等for循环执行完后在执行console.log(i)。for循环执行完时i===6，setTimeout又设置了6遍，所以会打出6个6
## 如何让上面代码打印 0、1、2、3、4、5 的方法
把let i=0放在()里
~~~
for(let i=0;i<6;i++){
    setTimeout(()=>{
        console.log(i)
    },0)
}