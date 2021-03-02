#### 介绍DOM事件级别
    ```html
    // DOM0
    element.onclick = function () {}
    ------------------------------------------
    // DOM2
    element.addEventListener('click', function () {
        //false冒泡阶段，true捕获阶段
    }, false); 
    ------------------------------------------
    // DOM3(增加了事件类型)
    element.addEventListener('keyup', function () {

    }, false);
    DOM1没注册跟事件相关的东西x
    ```
#### 请封装时间监听和解绑的兼容写法
    var myEventUtil = {
        addEvent : function (ele,event,func) {
            //用能力检测进行跨浏览器兼容处理
            if(ele.addEventListener) {
                //false表示冒泡事件模型
                ele.addEventListener(event,func,false);
            }else if(ele.attachEvent){
                ele.attachEvent('on'+event,func);
            }else{
                ele['on'+event]=func;
            }
        },
        delEvent : function (ele,event,func) {
            if(ele.removeEventListener){
                ele.removeEventListener(event,func,false);
            }else if(ele.detachEvent){
                ele.detachEvent('on'+event,func);//IE
            }else {
                ele['on'+event]=null;
            }
        }
    }
#### 介绍下事件模型？
    捕获，冒泡
#### 介绍下事件流
    1. 定义：用户与浏览器当前页面的交互过程
    2. 三个阶段：捕获阶段、目标阶段、冒泡阶段
#### DOM事件捕获的具体流程是怎样的
    window => document => html => body => ... => 目标元素
#### Event对象有哪些常用应用
    1. 阻止默认事件：event.preventDefault() || e.returnValue = false;
    2. 阻止冒泡：event.stopPropagation() || e.cancelBubble = true
    3. 阻止调用相同事件得到其他侦听器（事件响应优先级）：event。stoplmmediatePropagation（）
    4. 当前绑定时间元素：event.currentTarget
    5. 当前被点击的元素：event.target
#### 如何自定义事件
    var event = new Event('custome');
    dom.addEventListener('custome', funcion () {});
    dom.dispatchEvent(event);
    > Event 与CustomEvent唯一区别：CustomEvent除了可指定事件名，还可以根自定义参数，做指定参数
