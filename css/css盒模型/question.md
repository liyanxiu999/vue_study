#### CSS盒模型是什么
    盒子模型包括：content、padding、margin、border
#### 标准模型和IE模型的区别
    * 标准模型的宽高为content的宽高
    * IE魔性的宽高包括border
#### CSS如何设置这两种模型
    * 标准模式：box-sizing：content-box
    * IE模式： box-sizing:border-box
#### JS如何设置/获取和模型对应的宽高
    dom.style.width/height:内联样式宽高
    dom.currentStyle.width/height:渲染后的最终宽高（IE）
    window.getComputedStyle(dom).width/height:DOM标准，不支持IE
    dom.getBoundingClientRect().width/height:计算元素的绝对位置（视窗左顶点为起点，含left/right/height/top）
#### BFC是什么，讲一下原理
    块级格式化上下文
#### BFC布局规则
    1. 内部的box会在垂直的方向，一块一块的放
    2. box的垂直方向的距离由margin决定。属于同一个BFC的两个相邻的margin会发生重叠
    3. BFC的区域不会与float box重叠
    4. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然
    5. 计算BFC的高度，浮动元素也参与计算
#### 哪些元素会生成BFC
    1. float不为none
    2. position不为static/relative
    3. display的值为inline-block、table-cell、table-caption
        > caption属性返回了表格的caption元素，caption元素定义了表格的标题
    4. overflow的值不为visible
    5. 根元素
#### BFC的场景应用
    1. 自适应两栏布局
    ```html
        <style>
            .boc {
                width: 300px;
                position: relative;
            }
            .aside {
                width: 100px;
                height: 150px;
                float: left;
                background-color: #bfa;
            }
            .main {
                height: 200px;
                background-color: red;
                overflow: hidden;/*根据BFC布局规则第三条，BFC区域不会与float box重叠*/
            }
        </style>
        <div class="boc">
            <div class="aside"></div>
            <div class="main"></div>
        </div>
    ```
    2. 清除内部浮动
    ```html
        <style>
            .box {
                border: 2px solid red;
                width: 300px;
                /* 根据BFC布局规则第五条，计算BFC高度浮动元素也包含在内 */
                overflow: hidden;/*所以为达到清除浮动，可触发box BFC,在box计算高度时，浮动元素也包含在内*/
            }
            .child {
                border: 2px solid #fcc;
                width: 100px;
                height: 100px;
                float: left;
            }
        </style>
        <div class="box">
            <div class="child"></div>
            <div class="child"></div>
        </div>
    ```
    3. 防止垂直margin重叠
    ```html
        <style>
            p {
                color: #f55;
                background-color: #fcc;
                width: 200px;
                line-height: 100px;
                text-align: center;
                margin: 50px;
                /* 根据BFC布局规则第一条：box垂直方向的距离由margin决定，属于同一个BFC的两个相邻box的margin会发生重叠 */
                /* 解决方法：只需要在生成一个BFC，使两个BFC互不干扰 */
            }
            .wrap {
                overflow: hidden;
            }
        </style>
        <p>hahahha</p>
        <div class="wrap">
            <p>hehehhe</p>
        </div>
    ```