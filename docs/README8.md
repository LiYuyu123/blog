# 《JS对象基本用法》
## 声明对象的两种语法
1. let obj={'name':'lizi','age':18}
2. let obj=new Object({'name':'lizi'})
### 细节
1. 键名是字符串，不是标识符，可以包含任意字符
2. 引号可以省略，省略之后只能写标识符
3. 就算引号省略了，键名还是字符串
#
## 如何删除对象的属性
### 写法
1. delete obj.xxx
2. delete obj['xxx']
### 细节
1. 请区分[属性值为undefined]和[不含属性名]
2. 用'xxx' in obj===false 可以知道对象里有没有xxx属性
3. 用'xxx' in obj&&obj.xxx===undefined 判断含属性名，但值为undefined
4. obj.xxx只能判断属性值，不能判断属性名
#
## 如何查看对象的属性
### 查看所有属性名
1. Object.key(obj)
### 查看所有属性值
1. Object.values(obj)
### 查看所有的属性值和属性名
1. Object.entries(obj)
### 查看自身属性和共有属性
1. console.dir(obj)
### 查看单个属性
1. obj['key']
2. obj.key
#
## 如何修改或增加对象的属性
有属性则改，没有属性则增
### 直接赋值
let obj={name:'lizi'}
1. obj.name='xxx'
2. obj['name']='xxx'
3. let key='name' obj[key]='xxx'
### 批量赋值
1. Object.assign(obj,{p1:1,p2:2})
#
## 'name' in obj和obj.hasOwnProperty('name') 的区别
1. 'name' in obj 是查看name有没有再obj中
2. obj.hasOwnProperty('name')是判断一个属性是不是自身的属性