# 简述DOM事件模型或DOM事件机制
## 事件的捕获与冒泡
1. 从外向内找监听函数的，叫事件捕获
2. 从内向外找监听函数的，叫事件冒泡
## 事件绑定API(addEventListener)
1. IE:baba.attachEvent('onclick',fn)//冒泡
2. 网景:baba.addEventListener('click',fn)//事件捕获
3. W3C:baba.addEventListener('click',fn,bool)
   ~~~
   如果bool不传或为falsy，就让fn走冒泡，即当浏览器在冒泡阶段发现baba有fn监听函数，就会调用fn，并提供事件信息。
   如果bool为true，就让fn捕获，即当浏览器在捕获阶段发现baba有fn监听函数，就会调用fn，并提供事件信息。
   ~~~
## 顺序
特例：绑定在被点击元素的事件是按照代码的顺序发生的。
其他的都是先捕获在冒泡的。
