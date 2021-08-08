# 《jQuery的功能》
## jQuery 如何获取元素
使用jQuery的第一步，往往就是将一个选择表达式，放进构造函数jQuery()（简写为$），然后得到被选中的元素。
选择表达式可以是CSS选择器：
~~~
$(document) //选择整个文档对象
$('#div1') //选择ID为div1的网页元素
$('.red') // 选择class为red的元素
~~~
## jQuery的链式操作是怎样的
选中网页元素以后，可以对它进行一系列操作，并且所有操作可以连接在一起，以链条的形式写出来
~~~
　$('div').find('h3').eq(2).addClass('Hello')
~~~
它的原理在于每一步的jQuery操作，返回的都是一个为api的一个jQuery的对象
## jQuery如何创建元素
创建新元素的方法非常简单，只要把新元素直接传入jQuery的构造函数就行了
~~~
　$('<p>Hello</p>')

　　$('<li class="new">new list item</li>')

　　$('ul').appendTo('<li>list item</li>')
~~~
## jQuery如何移动元素
第一种方法是使用.insertAfter()，把div元素移动p元素后面：
~~~
　$('div').insertAfter($('p'))
~~~
第二种方法是使用.after()，把p元素加到div元素前面：
~~~
　　$('p').after($('div'))
~~~
## jQuery如何修改元素的属性
~~~
　　.html() 取出或设置html内容

　　.text() 取出或设置text内容

　　.attr() 取出或设置某个属性的值

　　.width() 取出或设置某个元素的宽度

　　.height() 取出或设置某个元素的高度

　　.val() 取出某个表单元素的值
~~~