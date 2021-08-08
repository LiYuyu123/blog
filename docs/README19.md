# 路由
## 默认路由
~~~
 number = number || 1;
~~~
## 404路由
~~~
<div id="div404" style="display: none;">你要找的内容被狗吃了</div>
 if (!div) {
    div = document.querySelector("#div404");
  }
  div.style.display = "block";
  container.innerHTML = "";
  container.appendChild(div);
}
~~~
## hash模式
任何情况下都可以用做前端路由。
缺点就是SEO不友好，浏览器是不会把#后面的内容发个服务器。
谷歌有一个hash的SEO
~~~
const app = document.querySelector("#app");
const div1 = document.createElement("div");
div1.innerHTML = "1";
const div2 = document.createElement("div");
div2.innerHTML = "2";
const div3 = document.createElement("div");
div3.innerHTML = "3";
const div4 = document.createElement("div");
div4.innerHTML = "4";
const routeTable = {
  "1": div1,
  "2": div2,
  "3": div3,
  "4": div4
};

function route(container) {
  let number = window.location.hash.substr(1);

  number = number || 1;

  // 获取界面
  let div = routeTable[number.toString()];
  if (!div) {
    div = document.querySelector("#div404");
  }
  div.style.display = "block";

  // 展示界面
  container.innerHTML = "";
  container.appendChild(div);
}

route(app);

window.addEventListener("hashchange", () => {
  console.log("hash 变了");
  route(app);
});

~~~
## history模式
~~~
const app = document.querySelector("#app");
const div1 = document.createElement("div");
div1.innerHTML = "1";
const div2 = document.createElement("div");
div2.innerHTML = "2";
const div3 = document.createElement("div");
div3.innerHTML = "3";
const div4 = document.createElement("div");
div4.innerHTML = "4";
const routeTable = {
  "/1": div1,
  "/2": div2,
  "/3": div3,
  "/4": div4
};

function route(container) {
  let number = window.location.pathname;
  console.log("number: " + number);

  if (number === "/") {
    number = "/1";
  }

  // 获取界面
  let div = routeTable[number.toString()];
  if (!div) {
    div = document.querySelector("#div404");
  }
  div.style.display = "block";

  // 展示界面
  container.innerHTML = "";
  container.appendChild(div);
}

const allA = document.querySelectorAll("a.link");

for (let a of allA) {
  a.addEventListener("click", e => {
    e.preventDefault();
    const href = a.getAttribute("href");
    window.history.pushState(null, `page ${href}`, href);
    // 通知
    onStateChange(href);
  });
}

route(app);

function onStateChange() {
  console.log("state 变了");
  route(app);
}
~~~
## memory模式
适合非浏览器。
缺点没有url，如果你想把你的网址分享给你的朋友，你的朋友只会看到页面的初始状态。 
~~~
const app = document.querySelector("#app");
const div1 = document.createElement("div");
div1.innerHTML = "1";
const div2 = document.createElement("div");
div2.innerHTML = "2";
const div3 = document.createElement("div");
div3.innerHTML = "3";
const div4 = document.createElement("div");
div4.innerHTML = "4";
const routeTable = {
  "/1": div1,
  "/2": div2,
  "/3": div3,
  "/4": div4
};

function route(container) {
  let number = window.localStorage.getItem("xxx");

  if (!number) {
    number = "/1";
  }

  // 获取界面
  let div = routeTable[number.toString()];
  if (!div) {
    div = document.querySelector("#div404");
  }
  div.style.display = "block";

  // 展示界面
  container.innerHTML = "";
  container.appendChild(div);
}

const allA = document.querySelectorAll("a.link");

for (let a of allA) {
  a.addEventListener("click", e => {
    e.preventDefault();
    const href = a.getAttribute("href");
    window.localStorage.setItem("xxx", href);
    // 通知
    onStateChange(href);
  });
}

route(app);

function onStateChange() {
  console.log("state 变了");
  route(app);
}
~~~
