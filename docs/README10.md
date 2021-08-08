# 《js对象的分类》
## 构造函数
1. 是用来构造对象的函数。
2. 会预先存好对象的原型，原型的原型是根对象。
3. new的时候会将对象--proto--指向原型
### new X()自动做了四件事
1. 自动创建空对象。
2. 自动为空对象关联原型，原型地址指定为X.prototype。
3. 自动将对象作为this关键字，运行构造函数。
4. 自动return this
### 构造函数X
1. X函数本身负责给对象本身添加属性。
2. X.prototype对象负责保存对象的其他属性。
### 大小写
1. 所有构造函数，首字母一定要大写。
2. 所有呗构造出来的对象，首字母小写。
### 词性
1. new后面的函数使用名词形式(new Person(),new Object())
2. 其他函数，一般用动词(createSquare(),createElement())
~~~
function Square(width){
    this.width=width
}
Square.prototype.getArea=function(){
    return this.width*this.width
}
let square=new Square(6)
~~~
~~~
class Square(){
    constructor(width){
        this.width=width
    }
    getArea(){
        return this.width*this.width 
    }
}
let square=new Square
~~~
#
对象是需要分类的
1. 有很多对象拥有一样的属性和行为
2. 需要把它们分为同一类
3. 但是还有很多对象拥有其他属性和行为
4. 所有需要不同的分类
5. 类是针对对于对象的分类，有无数种
6. 常见的有Array，Function，Date，RegExp
# 数组对象
## 自身属性
1. '0','1','3',length
2. 属性名没有数字只有字符串
## 共用属性
1. 'push'(往数组里添加)
2. 'pop'(把加的东西弹出来)
3. 'shift'(删除数组的第一个属性)
4. 'unshift'(从头部添加属性)
5. 'join'(把xxx，连接或变字符串)
## 定义
1. 元素的数据类型可以不同。
2. 内存不一定时连续的。
3. 不能通过数字下标获取元素，而是通过字符串。
4. 数组可以有任何key。
## 创建
1. let arr=[1,2,3]
2. let arr=new Array(1,2,3)
3. let arr=new Array(3)--长度为3
## 转化
1. let arr='1,2,3'.split(',')
2. let arr='123'.split('')
3. Array.from('123')--可以把伪数组变成数组
## 增删改查
### 合并两个数组，得到一个新的数组
1. arr1.concat(arr2)
### 截取一个数组的一部分
1. arr.splice(1)//从第二个元素开始截取
2. arr.splice(o)//经常用来复制数组
### 删除元素头部元素
arr.shift()--arr被修改，并返回被删元素
### 删除尾部元素
arr.pop()--arr被修改，并弹出元素
### 删除中间元素
1. arr.splice(index,1)--1表示次数，删除下标为index的元素
2. arr.splice(index,1,'x')--删除，并在删除位置添加'x'
### 查看所有key
~~~
for(let i=0;i<arr.length;i++){
    console.log(i)
}
~~~
### 查看所有key和value
~~~
for(let i=0;i<arr.length;i++){
    console.log(`${i}:${arr[i]}`)
}
~~~
### 另一种方式forEach
#### 查看key和value
~~~
arr.forEach(function(xxx，yyy)){
    console.log(`${yyy}:${xxx}`)
}
~~~
### for和forEach
1. forEach没有break这个功能，没办法结束。
2. 一个是块级作用域，forEach是个函数。
### 查看单个元素
arr[0]
### 查看元素的下标
arr.indexOf()
### 使用条件查看元素
~~~
arr.find(function(item){return item%2===0})
找到除于2余数为0的数字
~~~
~~~
arr findIndex(function(item){return item%2===0})
找到那个除于2余数为0的数字的下标
~~~
### 在尾部添加元素
arr.push()--修改arr，返回新的长度
### 在头部添加元素
arr.unshift()--修改arr，返回新的长度
### 在中间添加元素
arr.splice(index,0,item)
### 反转顺序数组中元素的顺序
arr.reverse()
~~~
let a='abcde'
a.split('')
a.split('').reverse()
a.split('').reverse().join('')
a='edcba'
~~~
### 自定义排序
1. arr.sort()--默认从小到大排的
2. 让它从大到小
~~~
arr.sort(function(a,b){
    if(a>b){
        return -1
    }else if(a===b){
        return 0
    }else{
        return 1
    }
})
arr.sort((a,b)=>b-a)
~~~
## 数组的变换
### map('n'变'n')
想要每个元素的平方：arr.map((item)=>item*item)
### filter('n'变少)
只要偶数：arr.filter((item)=>item%2===0)
### reduce('n'变别的东西)
想要数组的和：arr.reduce((sum,item)=>{return sum+item},0)
### 用reduce可以实现map和filter
想要每个元素的平方:arr.reduce((result,item)=>{return result.concat(item*item),[])
只要偶数:arr.reduce((result,item)=>result.concat(item%2===1? []:item),[]))
# 
## js函数
### 定义一个函数
1. 具名函数
   ~~~
   function 函数名(形式参数1，形式参数2){
       语句
       return 返回值
   }
   ~~~
2. 匿名函数(也是函数表达式)
   ~~~
   let a=function(x,y){return x+y}
   这时的fn(x,y)的作用域只在这个函数里，不在a里
   ~~~
3. 箭头函数
   ~~~
   let f1=x=>x*x
   let f2=(x,y)=>x+y
   如果有两句语句是就要加花括号了
   let f3=(x,y)=>{
       console.log('hi')
       return x+y
   }
4. 构造函数
   ~~~
   let f=new Function('x','y','return x+y')
   ~~~
### 函数的要素
1. 调用时机
2. 作用域
3. 闭包
4. 形式参数
5. 返回值
6. 调用栈
7. 函数的提升
8. arguments
9. this
### 调用时机
1. 时机不同，结果就不同
### 作用域
1. 每个函数都会默认创建一个作用域
   ~~~
   比如：
   function fn(){
       let a=1
   }
   console.log(a)//a不存在，因为a只在作用域里{}
2. 局部变量和全局变量
   ~~~
   1.在顶级作用域声明但是变量是全局变量
   2.window的属性是全局变量，不管在那个作用域也是全局变量
   ~~~
3. 如果多个作用域有同名的变量，那么查找a的声明时，就向上取近的作用域，这是就近原则
### 闭包(js的函数会就近寻找最近的变量)
1. 如果一个函数用到了外部的变量，那么这个函数和这个变量就叫做闭包
### 形式参数
1. 形式参数的意思就是非实际的参数
2. 形式参数可多可少
### 返回值
1. 返回函数的值，并终止函数的运行
2. 每个函数都有返回值，如果没写return，返回值就是undefined
3. 函数执行完了才会返回，只有函数有返回值
### 调用栈
1. js引擎在调用一个函数前，需要把函数所在的环境push到一个数组里，这个数组就叫调用栈
2. 在等函数执行完了，机会把环境弹(pop)出来，然后return到之前的环境，继续执行后续的代码
3. 由于每次(压栈)进入一个函数都得记录下来回到那，所以要把回到的地址写到栈里，等把函数执行完了就弹栈
4. 使用递归函数可能会把栈压满
### 函数提升
1. 不管你把函数的声明放到哪，函数都会跑到第一行
### arguments
1. 其实时包含函数调用时所有参数的伪数组
### this
~~~
let person={
    name:'lizi',
    sayHi(){
        console.log(`你好我叫`+person.name)
    }
}
1.我们可以用直接保存了对象地址的变量来获取'name',叫引用

这是有两个问题
  let sayHi=()=>console.log(`年后我叫`+person.name)
  let person={
      name:'lizi',
      'sayHi':sayHi
  }
  1. 这样person如果改了名，sayHi函数就会报错
  2. sayHi函数出现在另一个文件，person在另一个文件
   
  class Person={
      constructor(name){
          this.name=name
      }
      sayHi(){
          console.log(???)
      }
  }
  1.这只是类，还没创建对象，不能获取对象用

  有一种方法可以解决这个问题就是加一个参数
    class Person={
      constructor(name){
          this.name=name
      }
      sayHi(){
          console.log(person)
      }
  }

  所以在js中用this获取那个未知的对象
  let person={
    name:'lizi',
    sayHi(){
        console.log(`你好我叫`+this.name)
    }
}
这时person.sayHi()就相当于person.sayHi(person),然后person被传给this了(person是地址)
js通过额外的this做到:person.sayHi()会把person自动传给sayHi，sayHi可以通过this引用person的对象地址
~~~
### 立即执行函数
~~~
！function(){
    var a=1
    console.log(a)
}
~~~
  
  