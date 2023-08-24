title: Vue+apollo-vue实现 loading效果
tags:
  - VUE
author: Mia Liu
categories:
  - 前端
photos:
  - /upload/computer.jpg
date: 2018-08-06 15:34:00
---
需求描述：
子路由数据渲染完成以前实现loading组件的效果。<br/>

```javascript
文档写的
<div v-if="$apollo.queries.ping.loading">Loading...</div>
或者
<div v-if="$apollo.loading">Loading...</div>
不起作用，控制台也不报错，所以还是采用简单原始的方法，子组件向父组件传值
```
```javascript
//父组件
<div class="sec-con clearfix">
        <loading id="loading"
        v-if="isload == true"
          class='center'
          :loadingWord="loadingWord"
       ></loading>
<div id="content">
    <router-view @getstatus="getstatus"></router-view>
</div>


...
methods: {
    getstatus (isLoading) {
      this.isload = isLoading
    }
  }
```

    <pre>
    //子组件
    apollo: {
    ...,
    watchLoading (isLoading) {
        this.$emit('getstatus', isLoading)
      }
    }
    </pre>


    经测试，功能正常实现。