# Node.js 文件模块和单元测试
## 做一个基于文件的todo工具
### 功能：
1. 可以列出所有todo
2. 可以新增，编辑，删除，标记
### 命令：
1. t
2. t add 任务名
3. t clear
### 用到的库
1. commander(创建命令的库)
2. inquirer(写出列表的一个库)
### 知识点
#### Node.js 获取用户home目录和home变量
~~~
const homedir=require('os').homedir()
const home=process.env.HOME || homedir
~~~
#### Node.js提供了path来拼路径
~~~
const p=require('path')
const dbPath=p.join(home,'.todo')
~~~
#### 读fs.readFile(path,options,callback)
#### 写fs.writeFile(path,data,options,callback)
####
~~~
if(process.argv.length===2){
    //说明用户直接运行node cli
    api.showAll()
}
~~~
## 单元测试
### 步骤
1. 选择测试工具：jest
2. 设计测试用例
3. 写测试，运行测试，改代码
~~~
const db=require('../db.js')
const fs=require('fs')
jest.mock('fs')
describe('db',()=>{
    afterEach(()=>{
        //每次it之后调用
        fs.clearMocks()
    })
    it('can read',async ()=>{
        const data=[
            {title:'',done:true}
        ]
    fs.setMock('/xxx',null,JSON.stringify(data))
      const list =await db.read('/xxx')
        expect(list).toStrictEqual(data)
    })
    it('can write',async ()=>{
        const list=[{title:'你好',done:true}]
        let fakeFile
        fs.writeMock('/yyy',(path,data,callback)=>{
            fakeFile=data
            callback(null)
        })
       await db.write(list,'/yyy')
        expect(fakeFile).toBe(JSON.stringify(list)+'\n')
    })
})
~~~
~~~
const fs = jest.createMockFromModule('fs');
const _fs=jest.requireActual('fs') //真的fs
Object.assign(fs,_fs)


let readMocks={}
fs.setMock=(path,error,data)=>{
    readMocks[path]=[error,data]
}

fs.readFile=(path,options,callback)=>{
    if(callback===undefined){
    //fs.readFile('xxx',fn)
        callback=options
    }
    if(path in readMocks){
      callback(...readMocks[path])
    }else {
        _fs.readFile(path,options,callback)
    }
}
let writeMocks={}
fs.writeMock=(path,fn)=>{
    writeMocks[path]=fn
}
fs.writeFile=(path,data,options,callback)=>{
    if(path in writeMocks){
        writeMocks[path](path,data,options,callback)
    }else {
        _fs.writeFile(path,data,options,callback)
    }
}
fs.clearMocks=()=>{
    readMocks={}
    writeMocks={}
}
module.exports = fs;
~~~