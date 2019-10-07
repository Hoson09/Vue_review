# vue_review

## Project setup
```
yarn install 打开文件，根据package.json文件下载项目所需要的插件和依赖
```

### Compiles and hot-reloads for development
```
yarn run serve 在dev阶段，运行项目，其中自动为我们在本地生成一个url路径地址
```

### Compiles and minifies for production
```
yarn run build 在prod阶段，把项目打包到dist目录下。
```

### Run your tests
```
yarn run test 测试代码
```

### Lints and fixes files
```
yarn run lint 对项目的js代码进行eslint校验
```

### Run your unit tests
```
yarn run test:unit 测试代码
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# 1.Vue_生命周期

### (1).Vue_单个实例的生命周期
> 1. 创建Vue实例,然后开始解析构造的参数
> 2.  data等一系列参数还没有初始化完成之前，先执行beforeCreate()钩子
> 3. data参数初始化完成,开始监控data参数中数据的变化
> 4. 事件初始化完成，可以进行this调用
> 5. 然后调用created()钩子，在调用created()的时候，vue实例的中的data和methods方法都已经初始化完毕，可以进行this调用了,在整个页面形成过程中,created()钩子只会执行一次,正是因为这个特性，所以我们一般在created()方法中进行ajax请求一些数据和调用一些事件和方法，给data参数的数据赋值
> 6. 然后查找vue实例是否存在el参数对应的Dom对象，如果没有就查找vue实例方法vm.$mount()上是否有Dom对象
> 7. 找到挂载在vue实例上的el参数或者vm.$mount()方法对应的那个Dom对象后，查找在这个Dom对象中是否有Template模板，如果有Template模板，则把编译模板,即把data里面的参数和Template模板相结合
> 8. 如果没有Template模板,则把el参数对应的那个Dom对象编译成模板
> 9. 开始执行beforeMount()钩子，注意:此时编译好的模板还没有挂载替换到vue实例的el参数对应的html中的Dom元素上去,也就是说Dom对象还没有准备好，在这个钩子是无法进行访问和调整Dom对象的
> 10. 把上面编译好的模板去替换渲染el参数指向的Dom对象
> 11. 开始执行mounted()钩子，此时模板已经渲染到html页面中了,可以做任何关于这个html页面中Dom对象的调用和调整了，比如$refs的使用，此时也可以做一些ajax请求，注意:mounted()钩子只会执行一次
> 12. 模板挂载到html之后,开始实时监控数据的变化，随时更新Dom元素 
> 13. 当data数据发生改变,Dom元素更新之前，调用beforeUpdate()钩子方法
> 14. Dom元素更新之后，调用updated()钩子方法
> 15. 在Vue实例销毁前执行,beforeDestroy()钩子方法
> 16. Vue实例销毁了，然后执行destroyed()钩子方法

当在created()钩子有需求要操作Dom节点的时候但是此时Dom节点还没有挂载好,那么可以在created()钩子中执行调用this.$nextTick()方法,这个方法虽然在created()钩子中调用，但是这个方法实际中会在mounted()钩子执行之后才会被调用，也就是当页面上的Dom已经被模板渲染之后才会被真正触发调用这个方法,且this.$nextTick()只执行一次。

代码见 /Vue_html/Vue_lifeCircle.html;

### (2).Vue_components_lifeCircle
> 1. 根组件的beforeCreate()钩子调用
> 2. 根组件的created()钩子调用
> 3. 根组件的beforeMount()钩子调用
> 4. 子组件的beforeCreate()钩子调用
> 5. 子组件的created()钩子调用
> 6. 子组件的beforeMount()钩子调用
> 7. 子组件的mounted()钩子调用
> 8. 根组件的mounted()钩子调用
> 9. 根组件的nextTick()方法调用执行
> 10. 子组件的nextTick()方法调用执行

代码见 /Vue_html/Vue_components_lifeCircle.html

### Vue的细碎知识点：
1. 依赖：es6 webpack git 
2. vue: vue-loader vue,vuex,vue-router,vue-cli 
   #### (1)Vue Loader 是一个 webpack 的 loader，它允许你以一种名为单文件组件 (SFCs)的格式撰写 Vue 组件。
  例子如下：
   ```html
    <template>
      <div class="example">{{ msg }}</div>
    </template>

    <script>
    export default {
      data () {
        return {
          msg: 'Hello world!'
      }
    }
   }
   </script>

   <style>
    .example {
      color: red;
    }
    </style>
    ```
    Vue Loader 还提供了很多酷炫的特性：
     * 允许为 Vue 组件的每个部分使用其它的 webpack loader，例如在 <style> 的部分使用 Sass 
     * 允许在一个 .vue 文件中使用自定义块，并对其运用自定义的 loader 链；
     * 使用 webpack loader 将 <style> 和 <template> 中引用的资源当作模块依赖来处理；
     * 为每个组件模拟出 scoped CSS；
     * 在开发过程中使用热重载来保持状态。
   #### (2)Vue 是一套用于构建用户界面的渐进式框架,被设计为可以自底向上逐层应用
   #### (3)Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 应用的核心就是 store 在整个项目中是单一数据源即单一的全局的变量,其中主要分为state(数据),getters(state派生出来的计算属性，可以对state进行预处理),Mutation(突变,可以通过突变给state进行赋值),Action(与Mutation相似，不过Action 提交的是 mutation，而不是直接变更状态，包含任意异步操作。),Module(模块化,在每个组件或者Vue页面中对Vuex进行模块化处理)。
   #### (4)vue-router：Vue.js 官方的路由管理器,用 Vue.js + Vue Router 创建单页应用,只需要将组件 (components) 映射到路由 (routes)，然后告诉 Vue Router 在哪里渲染。
   #### (5)CLI：是全局安装的一个npm包,里面包括Vue的命令行。可以是用vue ui可视化安装一个vue项目，也可以使用vue create在终端创建一个vue项目。

3. vue: 自定义指令。。。要会简单使用自定义指令。Vue.directive('sss',{});
4. v-if 和 v-show的区别:是否生成到dom树。 应用场景:1.权限上应用v-if 2.无关紧要的使用v-show，可以提升性能。
5. 回答问题的方式，1.分析需求。2.回答问题。3.回答应用场景。
6. v-html是啥？？ 字符实体？？ &copy;就是一种字符实体。 enocde
v-html:是标签的一个vue指令，可以更新Dom元素中的 innerHTML，内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译，与jQuery中的$('#id').html()方法类似。在网站上动态渲染任意 HTML 是非常危险的，因为容易导致攻击。因此只在可信内容上使用 v-html，永不用在用户提交的内容上。示例：<div v-html="html"></div>
7. v-for key值必须独一无二的存在。与v-if连用的时候，v-if的优先级弱于v-for。可以遍历数组，对象，也可以遍历一个数字，v-for="item in 10" 。
8. vue实例中的data中数组的响应式双向绑定的方法 支持数组整体赋值。
9. 过滤器，可以写一些全局过滤器，全局都可以进行使用。 如果有些方法你看不懂，要先考虑是否是自定义的全局方法。
10. 虚拟的diff方法,操作一次，执行所有。数据更新完成后才会执行$nextTick()。虚拟dom的优化。***$nextTick()在promise().then()的最后执行。
11. props 如果传递一个props未声明的属性，这个属性会落到组件的根元素上去。
12. 事件的修饰符 stop prevent self  v-modal的修饰符 number  trim 
13. 模块实例的管理？？导入的模块实例都是单例的！！！！在一个js脚本中生成一个的模块实例，然后在项目中所有的地方import导入的实例都是同一个实例。
14. this七种指向 1.借用调用 2.call apply 3.函数调用 4.方法调用 5.构造函数调用 6.（bind(this指向第一个参数) 返回一个新函数。与call,apply区别是bind不会执行函数，但是会返回一个新函数，但是会把this指向给bind的第一个参数。let k = x.bind(第一个参数);k();而call和apply只会返回最后的结果。） 7.箭头函数.
15. 双向绑定的原理 v-modal  
  (1)核心原理是发布订阅模式，实质就是改写Object.defineProperty()方法。
  (2)在vue中的具体实现是,Vue官网的响应式原理,。
  (3)data对象中新声明的属性值是不受监听的，如果使用Vue.set(obj,'k',val)方法才可以接受Vue监听。
16. v-modal & 组件 ：实现①value属性和②@input事件。
17. vue-router: 嵌套路由定义children和使用route-view标签。<router-link></router-link>==<a></a>。路由守卫：beforeEach()钩子方法。获取路由数据 meta,params,query 与this.$router结合使用。动态添加路由。跳转 this.$router.go()/push();<router-link to=''></router-link>。
18. compute 计算属性也是双向绑定的。watch 是单方面监听不严格算双向绑定
19. mutation 同步 action 异步。
20. Vuex的模块化处理; 监听Vuex所有的变化 使用subscribe方法;Vuex的持久化处理插件 ;
21. Vue-CLI vue create '项目名' 可以创建一个项目 这个命令和 vue ui 效果一样。只是vue ui是形成可视化界面，而vue create是在终端进行相关配置形成相关的项目工程文件。
22. VUE_APP_ENV 环境变量的配置？
 在根目录中的.env文件中进行声明VUE_APP_ENV变量既可以配置vue项目的环境变量。
23. vue引入公共样式的方法？
 在vue.config.js文件中可以设置sass，然后引入公共样式
24. 构建单文件中，省略文件名的方法 在webpack中进行配置。
25. vue-Loader 单文件组件规范。 
26. 父组件影响子组件的方式：在css文件中，使用 父组件的类选择器 >>> 子组件的类选择器; 在scss文件中使用 父组件 /deep/ 子组件
27. 虚拟dom批量处理？？
28. v-modal组件话处理
29. nextTick()??