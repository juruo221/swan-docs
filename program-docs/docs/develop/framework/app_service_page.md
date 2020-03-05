---
title: 参数说明
header: develop
nav: framework
sidebar: app_service_page
---

 
 

**解释**：Page 函数用来注册一个页面。接受一个 object 参数，其指定页面的初始数据、生命周期函数、页面事件处理函数、组件事件处理函数等。

**Web 态说明：**

由于 Web 态框架暂不支持当前是否进入前、后台的状态检测，因此在下列场景中，Page.onShow、Page.onHide 生命周期无法触发
- 当 Web 态小程序从后台切换至前台时，如从任务管理器进入、或关闭显示在上层的语音助手等，Page.onShow 生命周期无法触发
- 当 Web 态小程序从前台切换至后台时，如按下 Home 键，Page.onHide 生命周期无法触发
- 当从 Web 态小程序跳转至其它第三方网页或应用时，如从 Web 态小程序打开拨号界面，Page.onHide 生命周期无法触发
- 关闭 Web 态小程序，Page.onHide 生命周期无法触发

**Object参数说明**：

|属性  |类型  |描述  |
|---- | ---- | ---- |
|data | Object | 页面的初始数据 |
|onLoad | Function | 页面的生命周期函数 -- 监听页面加载 |
|onShow | Function | 页面的生命周期函数 -- 监听页面显示 |
|onReady | Function | 页面的生命周期函数 -- 监听页面初次渲染完成 |
|onHide | Function | 页面的生命周期函数 -- 监听页面隐藏 |
|onUnload | Function | 页面的生命周期函数 -- 监听页面卸载 |
|onForceReLaunch|Function|页面的生命周期函数 -- 监听页面重启，单击右上角菜单栏的重启按钮时触发|
|onPullDownRefresh | Function | 页面的事件处理函数 -- 监听用户下拉动作 |
|onReachBottom | Function | 页面的事件处理函数 -- 上拉触底事件的处理函数 |
|onShareAppMessage | Function | 页面的事件处理函数 -- 用户点击右上角转发 |
|onPageScroll | Function | 页面的事件处理函数 -- 页面滚动触发事件的处理函数 |
|onTabItemTap | Function | 页面的事件处理函数 -- 当前是 tab 页时，点击 tab 时触发 |
| onURLQueryChange | Function | 页面的事件处理函数 -- 监听页面 URL query 改变 |
|其他 | Any | 开发者可以添加任意的函数或数据到 object 参数中 |

**名词解释:**

菜单栏: 页面右上角获取菜单按钮（右上角胶囊按钮）中三个点的图标，点击会弹出菜单面板(包含: 分享、评价、重启小程序等功能)。

**代码示例**

```js
// page.js
Page({
    data: {
        text: 'init data'
    },
    onLoad(options) {
        // do something when page load
    },
    onReady() {
        // do something when page ready
    },
    onShow() {
        // do something when page show
    },
    onHide() {
        // do something when page hide
    },
    onUnload() {
        // do something when page unload
    },
    onForceReLaunch() {
        // do something when page force reLaunch
    },
    onPullDownRefresh() {
        // do something when pull down
    },
    onReachBottom() {
        // do something when page reach bottom
    },
    onShareAppMessage() {
        // return custom share data
    },
    onPageScroll() {
        // do something when page scroll
    },
    onTabItemTap(item) {
        console.log(item.index);
        console.log(item.pagePath);
        console.log(item.text);
    },
    onURLQueryChange({newURLQuery, oldURLQuery}) {
        // do something when url query change
    },
    customData: {}
});
```
- 在页面中使用 behaviors

页面可以引用 behaviors 。 behaviors 可以用来让多个页面有相同的数据字段和方法。

**代码示例**

```js

// my-behavior.js
module.exports = Behavior({
  data: {
    sharedText: 'data shared between pages.'
  },
  methods: {
    sharedMethod: function() {
      this.data.sharedText === 'data shared between pages.'
    }
  }
})

```

```js

// page-a.js
var myBehavior = require('./my-behavior.js')
Page({
  behaviors: [myBehavior],
  onLoad: function() {
    this.data.sharedText === 'data shared between pages.'
  }
})

```






