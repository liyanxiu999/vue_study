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
  

