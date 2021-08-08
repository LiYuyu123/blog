
# 《CSS 知识总结》
#  css的基本慨念
## 文档流（文档中元素流动的方向）
### 流动方向
1. inline元素是从左到右到达最右边才会换行
2. block元素是从上到下，每一个都是另起一行的
3. inline-block 也是从左到右
### 宽度
4. inline的宽度为内部inline元素的和，而且不能用width指定
5. block默认自动计算宽度，可用width指定（永远不要写width：100%）
6. inline-block 结合两者的特点，可用width设置
### 高度 
1. inline高度是由line-height间接确定的，跟height无关
2. block高度是有内部文档流元素决定的，可以设置height
3. inline-block更block类似，可以设置height
## overflow （溢出）
1. 等内容高度或高度大于容器是，会溢出
2. 可用overflow来设置是否显示滚动条
3. auto 可以设置灵活的滚动条
4. scroll 设置滚动条但会永远显示
5. hidden 是设置直接隐藏溢出的部分
6. visble 是直接显示溢出的部分
## 脱离文档流
### 哪些元素是脱离文档流的   
1. float
2. poistion：absolute
## 盒模型
### 两种和模型
1. content-box 内容盒-内容就是盒子的边界
2. border-box 边框盒-边框就是盒子的边界
### 说明
1.css模型分两种一种是content-box和border-box区别是content-box的跨度只包含content border-box的宽度包含border+padding+content
## margin 合并
### 哪些情况会合并
1. 父子margin 合并
2. 兄弟 margin 合并
###如何阻止合并
1. 加一个 display：inline-block
### 说明
margin的左右是不会重叠的 ，上下会合并。父子级的元素第一级和最后一级的margin会合并，如果父级margin小于子级margin也会重合，但是子级margin会盖住父级的
# css布局
## 布局是什么
把页面分一块一块，按左中右 上中下等排列
## 布局分类
1. 固定宽度布局，一般宽度为960/100/1024px
2. 不固定宽度布局。主要靠文档流的原理来布局
3. 响应式布局是一种混合布局 意思就是pc上固定宽度手机上不固定
# float布局
## 步骤
1. 在子元素上加上float：left和width
2. 在父元素上加clearfix  .clearfix::after{content:'';diaplay:block;clear:both;}
## 做布局时
1. 做导航栏时发现logo图片多出来，就在img里加上vertical-align：top（maiddle）
2. 有时候border会干扰你的宽度那就把border改成outline
3. 要让内容居中加margin-left：auto和margin-right：auto
4. 在做平均布局的时候要布局中间加上一个x的图层，x图层的左边距时负的，用margin-right：-12px
# flex布局
## flex container有哪些样式
### 让一个元素变成flex容器 
1. display：flex和inline-flex
### 改变items流动方向
1. 改变流动方向（竖着）flex-direction：column
2. 改变流动方向（竖着 从下往上排）flex-direction：column-reverse
3. 改变流动方向（横着 默认的）flex-direction：row
4. 改变流动方向（横着 从右往左排）flex-direction：row-reverse
### 改变折行
1. 默认的是不折行flex-wrap：nowrap
2. 折行flex-wrap：wrap
### 主轴对齐方式
1. 默认主轴是横轴 除非你改变了flex-direction方向
2.  justify-content：flex-start
3.  justify-content：flex-end
4.  justify-content：space-between
5.  justify-content：space-around
6.  justify-content：space-evenly
##  次轴对齐
1. 默认次轴是纵轴
2. align-items：flex-start（往上顶）
3. align-items：flex-end（都在下面）
4. align-items：center（居中）
5. align-items：stretch（默认）
6. align-items：baseline
### flex item 有哪些属性
1. item上面加order
2. item：first-child（做为第一个儿子的item）
3. item：nth-child
4. item：last-child（最后一个儿子）
5. item上面加flex-grow控制如何变胖
6. flex-shrink控制如何变瘦
7. flex-basis控制基准宽度
8. 想使一个item可以独立 向下 align-self:flex-end
### 说明
1. 做导航栏时可以直接用margin-left：auto来直接把你需要的向右移
2. 永远不要把width和height写死，用min-width，max-width，min-height，max-height
# grid布局
### 二维布局用grid
1. 出发条件在父元素上加display：grid
### 设行和列
1. grid-template-columns：第一列 第二列 第三列
2. gird-template-row： 第一行 第二行 第三行
### item可以设置范围
1. grid-column-start
2. grid-column-end
3. grid-row-start
4. grid-row-end
### fr——free space(份)
1. grid-template-columns：1fr 1fr 1fr
2. gird-template-row：1fr 1fr
3. 如果想要平均布局就告诉空多少像素grid-gap：xx px
4. min-height：100vn （整个页面高度）
### grid-template-areas（分区）
1. gird-template-areas：“header header header”“aside aside aside”“ footer footer footer”
2. 在想要分区的标签里加入grid-area：header/......
# css定位
### 布局是屏幕平面上的
### 定位是垂直于屏幕的
## 从左边看一个div的结构
 ![div](1.png)
1. 浮动元素里的文字是在文字内容的下面
2. 浮动元素是脱离文档流的
## position属性
1. position：static（默认值，待在文档流里）
2. position：relative(相对定位，升起来，但不脱离文档流)
3. position：absolute(绝对位置，定位基准是祖先里的非static元素就是在用的时候在父级加个position：relative ，会脱离文档流)
4. position：fiexd(固定位置 定位基准是viewpart ，会脱离文档流)
5. position：sticky(粘滞定位)
## 层叠上下文
![图片](2.png)
### 层叠上下文也叫做堆叠上下文
1. 每个层叠上下文就是一个新的小世界（作用域）
2. 这个小世界里的z-index跟外界无关
3. 处在同一个小世界的z-index才能比较
4. z-index再小也不能小出大也不能大出html的世界
5. 负z-index是逃不出小世界的
### 有哪些css属性可以创建层叠上下文(需要记得)
1. z-index
2. display：flex
3. opactiy
4. transform
# css动画
## 动画的原理
### 动画定义
1. 由许多静止的画面(帧)
2. 以一定的速度连续播放
3. 肉眼因视觉残像产生错觉
4. 而误以为是活动的画面
### 动画的概念
1. 帧：每个静止的画面都叫做帧
2. 播放速度：每秒24帧（视频）或每秒30帧以上（游戏）
## 浏览器渲染的原理
### 渲染的步骤
1. 根据html构建html树（DOW）
2. 根据css构建css树（CSSOM）
3. 将两根树合并在一棵渲染树（render tree）
4. layout布局（文档流，盒模型，计算大小和位置）
5. paint绘制（把边框颜色，文字颜色，阴影画出来）
6. composete合成（根据层叠关系展示画面）
### 三种更新方式
1. js/css >样式 > 布局 >绘制 >合成
2. js/css >样式 >绘制 >合成
3. js/css >样式 >合成
### css动画优化
#### js优化
1. 使用requestAnimationFrame代替setTimeout或setInterval
#### css优化
1. 使用will-change或translate
## transform
### 四种常用工能
1. transform：translate（位移）
2. transform：scale（缩放）
3. transform：rotate（旋转）
4. transform：skew（倾斜）
### transform：translate
1. translateX (以x轴来位移)
2. translateY (以y轴来位移)
3. translateZ (以z这个视点来位移)
### transform：scale
1. scaleX(变胖)
2. scaleY(变高)
3. scale(变大成原来的几倍)
### transform：rotate
1. rotateX(以x轴来旋转)
2. rotateY(以y轴来旋转)
3. rotateZ
### transform：skew
1. skewX(以x轴来倾斜)
2. skewY(以y轴来倾斜)
### 说明
1. 都可以组合起来使用 用空格隔开
2. 取消所有transform：none
## transition（过渡）
### 作用是补充中间帧
### 语法
1. transition：属性名 时长 过渡方式 延迟
2. 属性名transition:left 200s ,可以用逗号分隔两个属性，可以用all代表所有属性
3. 过渡方式有：liner，ease，ease-in，ease-out，ease-in-out，cubic-bezier，step-start，step-end，steps
### 注意
#### 不是所有属性都能过渡
1. display=>block是没法过渡的，一般换成visibility：hidden=>visible
2. background可以过渡
## 如果有两次变化，有两种办法
### 使用两次transform
1. .a===transform===>.b
2. .b===transform===>.c
### 使用animation
## animation
### 缩写语法
#### animation：时长|过渡方式|延迟|次数|方向|填充模式|是否暂停|动画名
1. 时长：1s或者1000ms
2. 过渡方式：跟transition取值一样
3. 次数：3或者4或者infinite（一直变）
4. 方向：reverse（换个方向）|alternate(先去在回来)|alternate-reverse（先去在回来，在换个方向再来一遍）
5. 填充模式：none|forwards(意思是到最后就不要在回来)|backwards|both
6. 是否暂停：paused（使画面暂停）|running（是画面恢复动起来）
~~~~
#demo.start{
    animation:xxx 1s;
}
@keyframes xxx {
    0%{
        transform:none
    }
    66.66%{
        transform:translateX(200px);
    }
    100%{
         transform:translateX(200px);
         transform:translateY(200px);
    }
}
   
   