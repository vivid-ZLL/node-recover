#关于Nodejs搭建项目学习整理

* 前端框架
  - vue-cli
  - vuex
  - webpack
  - elemnetUI
  - bootstrap

* 后端框架
    - egg
    - express

## Vue脚手架搭建项目
    1. Vue init webpack project_name
    2. cd  project_name
      tree :
        ├─build   //构建项目目录
        ├─config  //构建配置目录
        ├─node_modules  //node工具包目录
        │  └─.staging
        │      └─selenium-server-1975358d
        │          └─lib
        │              └─runner
        ├─src     //源码目录
        │  ├─assets
        │  ├─components
        │  └─router
        │  ├─App.vue    //页面级vue组件
        │  └─main.js    //页面入口js文件
        ├─static  //静态文件目录
        └─test    //测试文件目录
        │    ├─e2e
        │    │  ├─custom-assertions
        │    │  └─specs
        │    └─unit
        │        └─specs
        ├─index.html
        ├─package.json
        ├─README.md
    3. npm install & npm install modules
      安装成功之后还会有一些

### 修改配置及新建页面
    1. config构建目录
      * index.js
      * dev.env.js
      * prod.env.js
      * test.env.js

    2. src源码目录
    3. static静态文件目录
    4. test测试文件目录
    5. index.html入口页面
    6. package.json 项目描述文件(所需模块版本、脚本执行命令等)
    7. .eslintrc.js ES语法检查配置
