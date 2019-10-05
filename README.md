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

代码见 /Vue_html/Vue_lifeCircle.html;