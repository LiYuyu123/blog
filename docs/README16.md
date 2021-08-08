# 《浅析MVC》
## MVC 三个对象分别做什么，给出伪代码示例
1. M-model(数据模型)负责操作所有数据
 ~~~
 const m={
     data:{
         n:xxxx
     }
 }
 ~~~
 2. V-view(视图)负责所有UI界面
~~~
const v={
    html:`<div></div>`,
    render(){}
}
~~~
3. C-controller(控制器)负责其他
~~~
const c={
    init(){}
}
~~~
## 表驱动编程是做什么的
表驱动法，又称之为表驱动、表驱动方法。 “表”是几乎所有数据结构课本都要讨论的非常有用的数据结构。表驱动方法出于特定的目的来使用表，程序员们经常谈到“表驱动”方法，但是课本中却从未提到过什么是"表驱动"方法。表驱动方法是一种使你可以在表中查找信息，而不必用很多的逻辑语句（if或Case）来把它们找出来的方法。事实上，任何信息都可以通过表来挑选。在简单的情况下，逻辑语句往往更简单而且更直接。但随着逻辑链的复杂，表就变得越来越富有吸引力了。
~~~
const c={
    events: {
     'click #add1': 'add',
     'click #minus1': 'minus',
     'click #mul2': 'mul',
     'click #divide2': 'div'
 }, 
}
const autoBindEvent(){
    for(let key in c.events){
        const value=c.events[key]
        const spaceIndex=key.indexOf(' ')
        const part1=key.slice(0,spaceIndex)
        const part2=key.slice(spaceIndex+1)
        this.el.om(part1,part2,value)
    }
}
~~~
## 我是如何理解模块化的
模块化开发其实就是封装细节，提供使用接口，彼此之间互不影响，每个模块都是实现某一特定的功能，同时也需要避免全局变量的污染，最初通过函数实现模块，实际上是利用了函数的局部作用域来形成模块。