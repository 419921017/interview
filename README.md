# 学习

## vue组件传值
    1. props 传值

    2. vuex 传值

## es6语法

    [es6新特性](http://www.cnblogs.com/raocheng/articles/6614133.html)

## 注册页面逻辑

    1. 默认状态、填写状态、反馈状态
    2. 整理信息、规划步骤，把需要用户录入的信息全部列举出来，然后设定到一个或多个步骤里，形成整个注册过程

## js中的继承

    1. js原型（prototype）实现继承
    
        ```
            function Person(name,age){  
                this.name=name;  
                this.age=age;  
            }  
            Person.prototype.sayHello=function(){  
                alert("使用原型得到Name："+this.name);  
            }  
            var per=new Person("马小倩",21);  
            per.sayHello(); //输出：使用原型得到Name:马小倩  

            
            function Student(){}  
            Student.prototype=new Person("洪如彤",21);  
            var stu=new Student();  
            Student.prototype.grade=5;  
            Student.prototype.intr=function(){  
                alert(this.grade);  
            }  
            stu.sayHello();//输出：使用原型得到Name:洪如彤  
            stu.intr();//输出：5  
        ```

    2. 构造函数实现继承

        ```
            function  Parent(name){  
                this.name=name;  
                this.sayParent=function(){  
                    alert("Parent:"+this.name);  
                }  
            }  

            function  Child(name,age){  
                this.tempMethod=Parent;  
                this.tempMethod(name);  
                this.age=age;  
                this.sayChild=function(){  
                    alert("Child:"+this.name+"age:"+this.age);  
                }  
            }  

            var parent=new Parent("江剑臣");  
            parent.sayParent(); //输出：“Parent:江剑臣”  
            var child=new Child("李鸣",24); //输出：“Child:李鸣 age:24”  
            child.sayChild();  
        ```

    3. call , apply实现继承

        ```
            function  Person(name,age,love){  
                this.name=name;  
                this.age=age;  
                this.love=love;  
                this.say=function say(){  
                    alert("姓名："+name);  
                }  
            }  

            //call方式  
            function student(name,age){  
                Person.call(this,name,age);  
            }  

            //apply方式  
            function teacher(name,love){  
                Person.apply(this,[name,love]);  
                //Person.apply(this,arguments); //跟上句一样的效果，arguments  
            }  

            //call与aplly的异同：  
            //1,第一个参数this都一样,指当前对象  
            //2,第二个参数不一样：call的是一个个的参数列表；apply的是一个数组（arguments也可以）  

            var per=new Person("武凤楼",25,"魏荧屏"); //输出：“武凤楼”  
            per.say();  
            var stu=new student("曹玉",18);//输出：“曹玉”  
            stu.say();  
            var tea=new teacher("秦杰",16);//输出：“秦杰”  
            tea.say();  

        ```


## js中写一个类

    [详解JS类概念的实现](https://segmentfault.com/a/1190000004700001)

## 命名空间

    [JavaScript 中的命名空间](http://chengkang.me/2016/06/21/Namespacing%20in%20JavaScript/)

## vue问题

## mix混入

## 布局问题

    - 盒子居中，flex，table-cell，absolute定位都设置为零，会撑满body嘛？

## compenets和extend组件继承


## 对vue的理解

## vue生命周期

    [VUE生命周期和钩子函数](https://segmentfault.com/a/1190000008010666)


## render函数

    [刺破 vue 的心脏之——详解 render function code](https://juejin.im/post/5928e9030ce4630057689e84)

## webgl

## webwork

    1. webwork,分别通过onmessage和postMessage来回传递数据，从而实现了多线程。(这个类似node下的get和post方法下的req和res,毕竟node和webwork都是异步通讯，原理也就类似)

## js性能

    [js 性能、单线程、setTimeout 性能优化的解决方法](https://github.com/woai30231/webDevDetails/tree/master/12)

## 前端性能优化(在操控门槛上依次递增，优化效果上越发没有不明显)

    1. 静态资源优化
        - 合并css、js文件，制作雪碧图：减少http的请求次数，节省网络请求时间
        - 静态资源cdn分发：客户端可以通过最佳的网络链路加载静态资源
        - js、css文件压缩，图片压缩，gzip压缩：减少请求返回的数据量
        - 静态资源缓存机制
        - 权衡dns的查找

    2. 接口访问优化
        - 静态资源加载完成了，页面依然还在转菊花，用户依然还在等待。现如今web应用已经走过完全由php和jsp等后端脚本语言渲染界面的时代，ajax异步加载数据的方式已经成为主流，各种前端的mvc框架层出不穷，先加载静态资源，在执行js中的ajax请求到后台请求数据，重新渲染界面已经是一种通行的方案，这样便出现了静态资源加载完成，页面可见，然而用户还需要等待请求数据的进度条的情况（特别是接口访问速度慢的时候）
        - 用户点击任意一个按钮，进度条加载了半天，也没有响应。很多复杂的功能需要并行或者串行的请求很多接口才能完成，前端的网络状况稍微差一点，给与用户的体验都极差。
        ### 首屏直出、同构
        - 首屏直出、同构对于上述的问题一，如果页面的初始化数据，在后端完成渲染，其它的用户交互使用ajax的方式完成，也就是传统意义上的首屏直出，就可以得到很好的解决这种介于完全后端渲染和完全ajax渲染的方式是一个不错的思路，但是在node出现之前，很多人宁愿容忍首屏加载的菊花，也不愿意使用，为什么？因为前端和后端要维护两套模板，令人抓狂node出来之后，前后端都都可以使用js语言，前后端同构（前端和后台公用模板代码）使得首屏直出重新拥有了生存的土壤，所以同构直出现在常常相提并论，形同一个成语(react在同构直出方面做得比较出众)

        ### 接口合并
        - 一个交互需要请求多个并行或串行接口实属正常，前端使用3g/4g等弱网络也着实是不可抗因素，所以最好的办法就是通过接口合并的方式来提高接口访问速度后台提供的接口有其既有粒度，强行合并不合时宜，提供一个新的合并的接口也缺乏机动性（前端发现一个新的合并需求，就要求后端提供一个接口，后端有开发工作量不说，还得没完没了的发版）如果把接口合并的主动权交给前端，那情况将会好很多，前端是最接近战火的地方，最知道应该如何组合接口。基于代理服务的接口合并方案应运而生（这是本人第一个值得骄傲的原创方案，这其中还包含了node实现，想想还有点小鸡动~）
        

    3. 页面渲染速度优化
        - css放在顶部：优先渲染
        - js放在底部：避免阻塞
        - 减少DOM元素数量：这个最能体现变成水平了
        - img标签要设置高宽：减少重绘重排
        - vue、react 等框架的虚拟dom渲染方案, 做到最小化操作真实dom
        - 使用一些页面性能分析工具给自己的页面跑分，可以帮助养成良好的编程习惯、提升编程素质，例如：WebPagetest、Yslow

## promise用法及原理

    [理解Promise简单实现的背后原理](http://bupt-hjm.github.io/2017/03/23/study-promise/)

## 动画性能

    [前端性能优化（CSS动画篇）](https://segmentfault.com/a/1190000000490328)

## jq和c3,哪个性能更好


## cookie,sessionstorage,localstorage区别

    [前端 JS，localStorage/sessionStorage、cookie 及 url 等实现前台数据共享、传输](https://github.com/woai30231/webDevDetails/tree/master/9)


## 很多ie兼容问题

    [再谈ie浏览器兼容问题](http://jartto.wang/2016/12/06/talk-about-ie-compatible-over-again/)

## jq原理

    [揭秘JQuery](https://github.com/shaodahong/dahong/issues/4)

## return出来的是什么

## webpack
    [webpack中文文档](http://www.css88.com/doc/webpack2/concepts/entry-points/)

## vue性能

    [vue 性能优化](https://github.com/Coffcer/Blog/issues/3)

## 途牛，es6箭头函数的区别，没有arguments

    [什么时候你不能使用箭头函数？](https://juejin.im/post/58fda157570c350058e6afb8)

## 异步嵌套有哪些方法，除了promise

    [JS中的异步操作](http://www.jianshu.com/p/6f91e7696b91)

## vue组件data返回的是一个function里面放的是对象，为什么？

    - 当一个组件被定义， data 必须声明为返回一个初始数据对象的函数，因为组件可能被用来创建多个实例。如果 data 仍然是一个纯粹的对象，则所有的实例将共享引用同一个数据对象！通过提供 data 函数，每次创建一个新实例后，我们能够调用 data 函数，从而返回初始数据的一个全新副本数据对象。

    - 如果需要，可以通过将 vm.$data 传入 JSON.parse(JSON.stringify(...)) 得到深拷贝的原始数据对象。


## 会话机制的原理

    [3种web会话管理的方式](http://www.cnblogs.com/lyzg/p/6067766.html)

## C3transition和animation的区别

## object和function区别！

    [一张图看懂 Function 和 Object 的关系及简述 instanceof 运算符](https://juejin.im/post/58358606570c35005e4142bd)


## es6类的概念

    [面向对象的 JavaScript – 深入了解 ES6 类](http://www.css88.com/archives/7383)

## 除了es6 其他实现类的方式（new,this）

## 三级联动，ie兼容，class

## axios

    [axios全攻略](https://ykloveyxk.github.io/2017/02/25/axios%E5%85%A8%E6%94%BB%E7%95%A5/#more)

CHENJUN930@pingan.com.cn