# 简述事件委托
## 事件的原理
1. 基于Js冒泡原理，把本来加在子元素身上的事件，加在了其父级身上。通过event对象里记录的“事件源”，查找发生事件的真正子元素
## 优点
1. 可以监听动态元素
2. 省监听数(内存)
## 事例
你要给100个按钮添加点击事件咋办?
监听100个按钮的祖先等冒泡阶段的时候判读target是不是这个按钮的其中一个
~~~
div1.addEventListener('click',(e)=>{
    const t=e.target
    if(t.tagName.toLowerCase()==='button'){
        console.log('button被点击了')
    }
})
~~~
## 封装事件委托
~~~
实现on('click','#div1',button,()=>{
    console.log('被点击了')
})
function on(eventType,element,selector,fn){
    if(!(element instanceof Element)){
        element=document.querySelector(element)
    }
    element.addEventListener('eventType',(e)=>{
        const el=e.target
        while(!el.matches(selector)){
            if(element===el){
                el=null
                break
            }
            el=el.parentNode
        }
        el&&fn.call(el,e,el)
    })
    return element
}
~~~