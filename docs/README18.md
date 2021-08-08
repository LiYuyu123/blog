# .sync修饰符的有什么用
## 举个列子
~~~
  <div class="app">
     我现在有 {{total}}
    <hr>
    <Child :money="total" v-on:update:money="total=$event"/>
  </div>
<script>
   Vue.component('Child',{
         props: ["money"]
         template:`  
         <div class="child">
             {{money}}
             <button @click="$emit('update:money', money-100)">
             <span>花钱</span>
             </button>
        </div>`
};
   })
   new Vue({
       data(){
           return {
               total: 10000
           }
       }
   })
<script/>
~~~
点击花钱时data就会改变减去100。
1. vue的规则:组件不能修改props外部的数据。
2. vue的规则:$emit可以触发事件,并传参。
3. vue的规则:$event可以获取$emit的参数。
### 这样会很麻烦,每次都要写这么长的代码，所有就用到了.sync修饰符
~~~
<Child :money="total" v-on:update:money="total=$event"/>就等价于<Child :money.sync="total" />
~~~
.sync修饰符其实是一个语法糖,它会被扩展为一个自动更新父组件属性的 v-on 监听器。
  