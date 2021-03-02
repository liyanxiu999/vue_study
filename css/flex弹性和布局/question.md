### flex 弹性和布局

#### CSS3弹性盒布局理解
    web应用有不同尺寸和分辨率，这是需要响应式界面设计来满足复杂的布局需求，Flex弹性盒模型的优势在于开发人员只是声明布局应该具有的行为，而不需要给出具体的实现方式，浏览器负责完成实际布局

    当布局涉及到_不定宽度，分布对齐_的场景时，就要优先考虑__弹性盒布局__
#### 容器属性
    主轴的方向：
        flex-direction：row | row-reverse | column | column-reverse
        row(默认值) ：主轴为水平方向，起点在左端
        row-reverse： 主轴为水平方向，起点在右端
        column： 主轴为垂直方向，起点在上方
        column-reverse： 主轴为垂直方向，起点在下方
#### 换行属性
    flex-wrap: nowrap | wrap | wrap-reverse
    nowrap(默认)：不换行
    wrap：换行，第一行在上方
    wrap-reverse:换行，第一行在下方
#### 简写：方向 + 换行
    flex-flow: <flex-direction> || <flex-wrap>;
#### 主轴对齐方式
    justify-content：flex-start | flex-end | center | space-between | space-around
    flex-start（默认）：左对齐
    flex-end：右对齐
    center: 居中
    space-between：两端对齐，项目之间的间隔相等
    space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框之间的间隔大一倍
#### 交叉轴对齐方式
    align-content：flex-start | flex-end | center | space-between | space-around | stretch
    flex-start：与交叉轴起点对齐
    flex-end：与交叉轴终点对齐
    center: 与交叉轴中点对齐
    space-between：与交叉轴两端对齐，轴线之间的间隔平均分布
    space-around：每根轴线两侧的间隔相等。所以，轴线之间的间隔比轴线与边框之间的间隔大一倍
    stretch（默认）：轴线占满整个交叉轴
#### 项目属性
    1. 排列顺序，数值越小，排列越靠前，默认为0
        order：<integer>
    2. 项目的放大比例，默认为0，即如果存在剩余空间，也不放大
       flex-grow: <number>; /* default 0 */
    3. 项目的缩小比例，默认为1，即如果空间不足，该项目将缩小    
        flex-shrink: <number>; /* default 1 */
    4. 项目占据的空间，默认为auto，及项目本身的大小
        flex-basis: <length> | auto; /* default auto */
    5. 简写：flex-grow，flex-shrink和flex-basis
        flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    6. 独立的对齐方式
        align-self: auto | flex-start | flex-end | center | baseline | stretch;
#### 关于项目属性flex的理解
            简写方式                完整形式
             默认值               flex : 0 1 auto
            flex : 1              flex : 1 1 0%; 
            flex: auto            flex : 1 1 auto;
            flex : none           flex: 0 0 auto;
            flex : 0%             flex : 1 1 0%;
            flex : 2 3            flex : 2 3 0%;
            flex : 2 3px          flex : 2 1 3px;
        > 注意：重点理解flex：1和flex：auto的区别，本质上是flex-basis的理解
        > flexbox在分配剩余空间时，需要计算剩余空间大小，这依赖于flex-basis
        > flex:1时flex-basis是0%，也就是元素就算设置了width也不会起作用，基准宽度为0，元素最终宽度是分配了生育宽度后得到的尺寸
        > flex:auto时，flex-basis是auto，基准宽度为元素设置的width，最终宽度等于基准宽度+剩余宽度分配后的宽度















             