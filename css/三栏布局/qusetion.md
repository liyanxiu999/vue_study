

#### 三栏布局，高度已知，左右两栏固定，中间自适应的三栏布局有几种实现方式，各自的优缺点是什么
        1. float实现
            优点：兼容性好
            缺点：脱离文本流，DOM节点顺序错误
            注意：中间栏写在左右两栏后
                <div class="left">1</div>
                <div class="right">3</div>
                <div class="center">2</div>
        2. absolute实现
            优点：快捷
            缺点：脱离文本流
        3. margin 负值实现
            优点：兼容性好
            缺点：节点顺序错误，需要在外层多添加一层div。出问题难以排查
        4. flex实现
            优点：新布局方式，解决以上两种布局方式的缺陷
            缺点：兼容性较差
        5. table实现
            优点：兼容性好、快捷
            缺点：单元格限制，当某个但愿个高度调整时，其他单元格也会被调整
            原理：利用父元素display:table;子元素：display:table-cell
        6. grid实现
            优点：将网格布局标准化，将复杂问题简单化
            缺点：兼容性差
#### 三栏布局，高度未知，以上布局哪些人可用，哪些不能用
    1. float：不可用
    2. absolute：不可用
    3. flex：可用
    4. table: 可用
    5. grid：不可用
#### 三栏布局，高度已知，左中固定，右自适应
    与左固定，中自适应的三栏布局相似
#### 三栏布局，上下固定，中自适应

#### css居中布局有哪些，适用于哪些场景，举例说明
    一、 CSS居中：margin设为auto
        1. 做法：把要居中的元素margin-left和margin-right都设为auto
        2. 场景：只能进行水平的居中，且对浮动元素或绝对定位元素无效
    二、 CSS居中：使用text-align:center
        1. 场景：只能对图片，按钮，文字等行内元素（display为inline或inline-block等）进行水平居中
            > 注意：在IE6、7中，他能对任何元素进行水平居中
    三、 CSS居中：使用line-height让单行的文字垂直居中
        1. 做法：把文字的line-height设为文字父容器的高度
        2. 场景：适用于只有一行文字的情况
    四、 CSS居中：使用表格
        1. 做法：td/th元素设置align="center"、valign="middle"即可处理单元格里面内容的水平和垂直居中问题
        2. 场景：必须是table
    五、 CSS居中：使用display：table-cell来居中
        1. 做法：利用父元素display:table;子元素：display:table-cell
        2. 场景：IE6/7无效
    六、 CSS居中：使用绝对定位，margin负值进行居中
        1. 场景：只适用于元素宽度或高度已知的元素
        2. 原理： 通过这个通过把这个绝对元素的left或top的属性设为50%，这个时候元素并不是居中的，而是比居中的位置向左或是向右偏了这个元素宽度或高度的一般的距离，所以需要使用一个负的margin-left或margin-top的值来把他拉回到居中的位置上，这个负的margin值取为这个元素的宽或者高一般距离
    七、 CSS居中：使用绝对定位进行居中
        1. 场景：只适用于宽度或高度已知的元素。且只支持IE9+，谷歌、火狐等符合w3c标准的现代浏览器
        2. 方法: left,right,top,bottom设为0
    八、 CSS居中：使用浮动配合相对定位来进行水平居中
        1. 场景： 无需知道要居中元素的宽度，缺点是需要一个多余的元素来包裹要居中的元素
        2. 原理：把浮动元素相对定位到父元素宽度50%的地方，但这时元素还不是居中的，而是比居中的位置多出自身宽度的一半，这是需要他里面的子元素再用一个相对定位，把多出自身一般的宽度拉回来，而相对定位正式向对自身来进行定位的，所以自身壁板的宽度只需要把left或者right设为50%就可以了，因而不用知道自身的实际宽度是多少。
        ```html
            <div class="box">
                <style>
                    body {
                        margin: 0;
                        padding: 0;
                    }
                    .box {
                        width: 300px;
                        height: 300px;
                        border: 1px solid red;
                        margin: auto;
                    }
                    .parent {
                        float: left;
                        position: relative;
                        left: 50%;
                        clear: both;
                    }
                    .child {
                        border: 1px solid cyan;
                        position: relative;
                        left: -50%;
                    }
                </style>
                <div class="parent">
                    <div class="child">
                        我水平居中啦
                    </div>
                </div>
            </div>
        ```