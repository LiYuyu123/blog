# 《HTML常用标签》g
## a标签的用法
### a标签的属性
1. href（起引用的效果）
2. target（指定那个窗口打开）
3. download（下载网页)
4. rel=noopener (可以解决安全问题)
### a的href的取值
1. 网址：可以用https：//www.google.com和http：//www.google.com还可以用//google.com
2. 路径/a/b/c 和a/b/c
3. 伪协议：javascript：;````<a href="javascirpt:;">````；可以当空链接来使用 mailto：邮箱 ````<a href="mailto:2248868140@qq.com">````点击可以打邮箱 tel：手机号 ````<a href="tel:17365454">````点击可以打电话
### a的target的取值
1. _blank( 可以使点击在另一个页面打开) ````<a href="" target="_blank">````
2. _top( 可以是点击在最顶层页面打开)````<a href="" target="_top">````
3. _parent(可以是点击在父级打开) ````<a href="" target="_parent">````
4. _self(是一个默认值 可以使页面在原来的页面打开)````<a href="" target="_self">````


## img标签的用法
### 作用
1. 发出get请求，展示一张图片
### 属性
1. alt(表示加载失败代替的文字)````<img src="" alt="文字">````
2. height(表示高)````<img src="" height=200px>````
3. width(表示宽)````<img src="" width=200px>````
4. src(表示图片的地址)
### 事件
1.onload和onerror是用来监听图片有没有加载成功
### 响应式
1.max-width：100%（可以用来设置手机上加载的图片）

## table标签的用法
## 语法
~~~~
<table>
      <thead>
            <tr>
                <th></th>
                <td></td>
            </tr>
      </thead>
      <tbody>
            <tr>
                <td></td>
                <td></td>
            </tr>
      </tbody>
      <tfoot
            <tr>
                <td></td>
                <td></td>
            </tr>
      </tfoot>
</table>
~~~~
### 相关的样式
1. table-cayout
2. border-collapse(可以是每格合并)
3. border-spacing（可以调整每格之间的距离）
## 我的感想
* 今天学到了很多知识 非常开心




