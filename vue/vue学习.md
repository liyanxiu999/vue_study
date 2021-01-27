### object.defineProperty
  Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
  vue原理即通过object.defineProperty来实现set和get的拦截
  set：设置vue中某个值的修改。。。
  get：类似于访问某个值，但未 修改
  Vue.set(vm.classobj,"d",true)新开一条通道，插入想输入得值 
  Vue.set(vm.styleobj,"fontSize",'40px')新开一条通道，插入想输入得值 
  `html
  <div id="box">
    <div :class="classobj">动态切换class-对象写法</div>
    <!-- Vue.set(vm.classobj,"d",true)新开一条通道，插入想输入得值 -->
    <div :class="classarr">动态切换class-数组写法</div>
    <!-- vm.classarr.push("d"),新开一条通道，插入想输入得值 -->
    <div :style="styleobj">动态切换style-对象写法</div>
    <div :style="stylearr">动态切换style-数组写法</div>
  </div>

  <script>
    var vm = new Vue ({
      el:"#box",
      data:{
        classobj:{
          a:true,
          b:true,
          c:true
        },
        classarr:['a','b','c'],
        styleobj:{
          backgroundColor:"red"
        },
        stylearr:[{
          backgroundColor:"red"
        }]
      }
    })
    //  Vue.set(vm.classobj,"d",true)新开一条通道，插入想输入得值 
    //  Vue.set(vm.styleobj,"fontSize",'40px')新开一条通道，插入想输入得值 
  </script>
  ### .ignore文件配置方法
    1.配置语法：
　　  以斜杠“/”开头表示目录；
　　  以星号“*”通配多个字符；
　　  以问号“?”通配单个字符
      以方括号“[]”包含单个字符的匹配列表；
　　  以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；
　　  此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；
    2、示例：
    （1）规则：fd1/*
　　　　  说明：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/ 目录，还是某个子目录 /child/fd1/ 目录，都会被忽略；
    （2）规则：/fd1/*
　　　　  说明：忽略根目录下的 /fd1/ 目录的全部内容；

  ### template
    template就是一个包装元素，不会真正的创建在页面上
  ### 条件渲染
    * key值：
      跟踪每个节点的身份，从而重用和重新排序现有的元素
      理想的key值是没想都有的且卫衣的id。data.id
    * 数组更新检测
      a.vue将被侦听的数组的变更方法进行了包裹，所以他们也将会触发视图更新。这些包裹方法包括：
      push(),pop(),shift(),unshift(),splice(),sort(),reverse()
      b.filter(),concat()和slice(),新数组替换旧数组
      c.不能检测一下变动的数组
        vm.item[indexOf(item)] = newValue
        解决方法：
          1.Vue.set(example.items,indexOf(item),newValue)
          2.splice
  ### 修饰符
    a. .stop修饰符：阻止冒泡行为 
    b. .prevent修饰符：阻止默认行为
    c. 表单修饰符
        .lazy: 失去焦点同步一次
        .number:格式化数字
        .trim：去除首尾空格
  ### 选项/数据
    1. data:状态
    2. computed:注重结果
        a. 逻辑计算，防止模板过重，有缓存
        b. 监听：依赖修改，get方法必须return
    3. methods
       a. 点击事件处理函数，return不是必须的
       b. 函数表达式的逻辑处理，没有缓存
    4. watch

