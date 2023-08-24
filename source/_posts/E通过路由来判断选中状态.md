title: VUE通过路由来判断选中状态
tags:
  - VUE
author: Mia Liu
categories:
  - 前端
date: 2018-04-26 17:42:00
photos: 
- /upload/router.jpg
---
路由配置

![路由.png](https://upload-images.jianshu.io/upload_images/4620451-875a1f46bb2f0616.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

/main是一个非登录的首页，主要功能就是有四个菜单选项，点击进入相应的子页面

![main页面.png](https://upload-images.jianshu.io/upload_images/4620451-a564816e793d32dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这些子页面都有共同的头部和侧边栏，所以归类到/home这个路由下，main.js需要配置一下项目一打开进入的是/main页面

![home.jpg](https://upload-images.jianshu.io/upload_images/4620451-24624f94a258af92.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
router.beforeEach((to, from, next) => {
  if (to.path === '/') {
    next({ path: '/main' })
  } else {
    next()
  }
})
```
/home侧栏的写法
```javascript
// 左边导航菜单
  <div class="side-bar">
    <div class="side-list">
        <div :default-active="$route.router" class="menu-demo" router>
          <div v-for="item in $router.options.routes[2].children" class="nav-list"
          :key="item.id"
          :class="$route.path.indexOf(item.path) >= 0 ?'is-active':''"
          @click="$router.push(item.path)">
            <div :index="item.path" class="rt-link">
              <i :class="item.iconCls"></i>
              <h4> {{ item.name }}</h4>
            </div>
          </div>
        </div>
    </div>
  </div>
```