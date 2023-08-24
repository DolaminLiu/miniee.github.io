{}
date: 2018-08-06 11:53:01
---
VUE+Apollo实现页面loading效果

<pre>{
    path: '/',
    component: Home,
    name: 'home',
    children: [{
      path: '/robot',
      component: Robot,
      iconCls: 'jqlb-wt',
      name: '机器列表'
    }, {
      path: '/status',
      component: Status,
      iconCls: 'yxzt-wt',
      name: '运行状态',
      children: [{
        path: '',
        redirect: 'current'
      },
      {
        path: 'current',
        component: Current,
        name: '当前报警'
      }, {
        path: 'history',
        component: Historyinfo,
        name: '历史报警'
      }, {
        path: 'basic',
        component: Basicinfo,
        name: '基本信息'
      }, {
        path: 'hardware',
        component: Hardware,
        name: '硬件配置'
      }, {
        path: 'firmware',
        component: Firmware,
        name: '固件版本'
      }, {
        path: 'application',
        component: Application,
        name: '应用软件'
      }]
      .....
    }
    </pre>
