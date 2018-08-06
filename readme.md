#关于Nodejs搭建项目学习整理

* 前端框架
  - vue-cli
  - vuex
  - webpack
  - elemnetUI
  - bootstrap
  - iView

* 后端框架
    - egg
    - express

## Vue脚手架搭建项目
    1. Vue init webpack project_name
    2. cd  project_name
      tree :
        ├─build           //构建项目目录
        ├─config          //构建配置目录
        ├─node_modules    //node工具包目录
        │  └─.staging
        │      └─selenium-server-1975358d
        │          └─lib
        │              └─runner
        ├─src             //源码目录
        │  ├─assets       //初始项目资源目录
        │  ├─components   //组件目录
        │  └─router
        │  │  └─index.js  //路由配置文件
        │  ├─App.vue      //页面级vue组件,App入口文件
        │  └─main.js      //页面入口js文件,主配置文件
        ├─static          //静态文件目录，资源放置目录
        └─test            //测试文件目录
        │    ├─e2e
        │    │  ├─custom-assertions
        │    │  └─specs
        │    └─unit
        │        └─specs
        ├─index.html      //项目入口文件
        ├─package.json
        ├─.eslintrc.js    //ES语法检查配置
        ├─README.md
        └─package-lock.json  //npm5新增文件，优化性能
    3. npm install & npm install modules

### 修改配置
    1. config构建目录
      * index.js        //配置主文件
      * dev.env.js      //开发配置文件
      * prod.env.js     //编译配置文件
      * test.env.js     //测试配置文件

    2. src源码目录配置
      tree:
        ├── App.vue                         // APP入口文件
        ├── api                             // 接口调用工具文件夹
        │   └── index.js                    // 接口调用工具
        ├── components                      // 组件文件夹，目前为空
        ├── store                           // 组件文件夹，目前为空
        ├── config                          // 项目配置文件夹
        │   └── index.js                    // 项目配置文件
        ├── frame                           // 子路由文件夹
        │   └── frame.vue                   // 默认子路由文件
        ├── main.js                         // 项目配置文件
        ├── page                            // 我们的页面组件文件夹
        │   ├── content.vue                 // 准备些 cnodejs 的内容页面
        │   └── index.vue                   // 准备些 cnodejs 的列表页面
        ├── router                          // 路由配置文件夹
        │   └── index.js                    // 路由配置文件
        ├── style                           // scss 样式存放目录
        │   ├── base                        // 基础样式存放目录
        │   │   ├── _base.scss          // 基础样式文件
        │   │   ├── _color.scss         // 项目颜色配置变量文件
        │   │   ├── _mixin.scss         // scss 混入文件
        │   │   └── _reset.scss         // 浏览器初始化文件
        │   ├── scss                    // 页面样式文件夹
        │   │   ├── _content.scss       // 内容页面样式文件
        │   │   └── _index.scss         // 列表样式文件
        │   └── style.scss              // 主样式文件
        └── utils                       // 常用工具文件夹
          └── index.js                  // 常用工具文件

    3. static静态文件目录
      tree:
        ├── css             // 放一些第三方的样式文件
        ├── font            // 放字体图标文件
        ├── lib             // 也可以是一些第三方的脚本文件
        ├── image           // 放图片文件，如果是复杂项目，可以在这里面再分门别类
        └── js              // 放一些第三方的JS文件，如 jquery

    4. test测试文件目录
      略。

### 新建页面与路由
    1. 组件的定义、注册和调用
      * 组件定义在 src/components目录，可以单独为某一个组件新建一个文件夹，包含index.js和index.vue文件，此时components目录下的组件都是子组件，需要在父组件App.vue中进行注册调用
      * 比如说在src/components/目录下有个Child.vue文件进行声明子组件:
        <template>
          <div>...</div>
        </template>
      * 然后可以在父组件App.vue中直接注册调用:
        <template>
          <div>
            <Child>....</Child>
          </div>
        </template>

    2. 创建路由的起点
      * src/router/index.js   单系统应用，可以默认使用一个路由文件
      * src/router/*.js       多系统应用，设置多个路由文件给不同系统使用
      * 嵌套路由 routers中可以添加children的嵌套二级路由,在配置path的时候，以"/"开头的嵌套路径会被当做根路径，所以子路由的path不需要添加"/"
      * 正如第一点的组件定义、注册和调用，我们需要在路由中导入该组件，并在routes对象中配置路由的路径path以及相映射的组件component:
        import Child form '@/components/Child'
        export default new Router({
          routes: [
            {
              path: '/',
              name: 'Child',
              component: Child
            }
          ]
        })
      * 注意点： export default Router 必须写在文件底部，而且后面还需要接一空行，否则无法通过 ESlint 语法验证

    3. 主页面界面编辑
      * 针对在components文件夹下定义好的组件文件，需要在父组件中进行注册，那么可以在page目录下为不同的主页面创建不同的页面模板，然后在里面注册和调用组件模板

    4. 关于vue-router和router-view
      * 我们经常可以看到App.vue中有一个<router-view>组件，那么这个组件是如何进行渲染的呢？
        <router-view>是用来渲染通过路由映射过来的组件，当路径更改时，<router-view>中的内容也会相应更改，比如我们打开http://localhost:8080/home的时候，<router-view>中就会渲染home.vue组件
      * home.vue中也同样可以在<template/>中添加<router-view>组件，这样也会在home.vue的<routerr-view>中渲染相应的子组件

### 父子组件数据传递
    1. props和$emit方式
      * 子组件通过this.$emit()派发事件，父组件利用v-on对事件进行监听，实现参数的传递
        父组件：<v-cartcontrol :food="food" v-on:changeCart="changeCart"></v-cartcontrol>
        子组件：this.$emit('changeCart',event.target)/*向父组件派发事件，同时传递参数event.target,后面的参数的个数不限*/

    2. vuex this.$store
