# computed和watch的例子
## computed用户展示
~~~
new Vue({
  data: {
    user: {
      email: "2248868140@qq.com",
      nickname: "李子杰",
      phone: "13812312312"
    }
  },
  computed: {
    displayName: {
      get() {
        const user = this.user;
        return user.nickname || user.email || user.phone;
      },
      set(value) {
        console.log(value);
        this.user.nickname = value;
      }
    }
  },
  // 不如用 computed 来计算 displayName
  template: `
    <div>
      {{displayName}}
      <div>
      {{displayName}}
      <button @click="add">set</button>
      </div>
    </div>
  `,
  methods: {
    add() {
      console.log("add");
      this.displayName = "圆圆";
    }
  }
}).$mount("#app");
~~~
## computed列表展示
~~~
let id = 0;
const createUser = (name, gender) => {
  id += 1;
  return { id: id, name: name, gender: gender };
};
new Vue({
  data() {
    return {
      users: [
        createUser("小明", "男"),
        createUser("小红", "女"),
        createUser("小新", "男"),
        createUser("小葵", "女")
      ],
      gender: ""
    };
  },
  computed: {
    displayUsers() {
      const hash = {
        male: "男",
        female: "女"
      };
      const { users, gender } = this;
      if (gender === "") {
        return users;
      } else if (typeof gender === "string") {
        return users.filter(u => u.gender === hash[gender]);
      } else {
        throw new Error("gender 的值是意外的值");
      }
    }
  },
  methods: {
    setGender(string) {
      this.gender = string;
    }
  },

  template: `
    <div>
      <div>
      <button @click="setGender('') ">全部</button>
      <button @click="setGender('male')">男</button>
      <button @click="setGender('female')">女</button></div>
      <ul>
        <li v-for="(u,index) in displayUsers" :key="index">{{u.name}} - {{u.gender}}</li>
      </ul>
      
    </div>
  `
}).$mount("#app");
~~~
## watch撤销
~~~
new Vue({
  data: {
    n: 0,
    history: [],
    inUndoMode: false //不在撤销模式
  },
  watch: {
    n: function(newValue, oldValue) {
      console.log(this.inUndoMode);
      if (!this.inUndoMode) {
        this.history.push({ from: oldValue, to: newValue });
      }
    }
  },
  template: `
    <div>
      {{n}}
      <hr />
      <button @click="add1">+1</button>
      <button @click="add2">+2</button>
      <button @click="minus1">-1</button>
      <button @click="minus2">-2</button>
      <hr/>
      <button @click="undo">撤销</button>
      <hr/>

      {{history}}
    </div>
  `,
  methods: {
    add1() {
      this.n += 1;
    },
    add2() {
      this.n += 2;
    },
    minus1() {
      this.n -= 1;
    },
    minus2() {
      this.n -= 2;
    },
    undo() {
      const last = this.history.pop();
      this.inUndoMode = true;
      console.log("ha" + this.inUndoMode);
      const old = last.from;
      this.n = old; // watch n 的函数会异步调用
      this.$nextTick(() => {
        this.inUndoMode = false;
      });
    }
  }
}).$mount("#app");
~~~
## 用watch模拟computed的用户展示
~~~
new Vue({
  data: {
    user: {
      email: "22454540140@qq.com",
      nickname: "杰杰",
      phone: "1375455561"
    },
    displayName: ""
  },
  watch: {
    "user.email": {
      handler: "changed",
      immediate: true // 第一次渲染是也触发 watch
    },
    "user.nickname": {
      handler: "changed",
      immediate: true // 第一次渲染是也触发 watch
    },
    "user.phone": {
      handler: "changed",
      immediate: true // 第一次渲染是也触发 watch
    }
  },
  // 不如用 computed 来计算 displayName
  template: `
    <div>
       {{displayName}}
       <button @click="user.nickname=undefined">remove nickname</button>
    </div>
  `,
  methods: {
    changed() {
      console.log(arguments);
      const user = this.user;
      this.displayName = user.nickname || user.email || user.phone;
    }
  }
}).$mount("#app");

~~~