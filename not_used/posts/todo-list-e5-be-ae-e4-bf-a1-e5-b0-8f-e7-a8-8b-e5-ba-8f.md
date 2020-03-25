---
title: Todo-list 微信小程序
url: 14685.html
id: 14685
categories:
  - Computer
date: 2018-06-07 08:53:07
tags:
---

![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot-29.png) ![](http://blog.echo.cool/wp-content/uploads/2018/06/微信图片_20180607084711.png) 做这个小程序，本来是想自己拿python写后端，但后来发现，用LearnCloud明显更方便。 再加上其高效的API，小程序很快就完成了。 ![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot-34.png) 这里再放几段用到的代码： 微信小程序复制操作：

<text class="tblin\_items\_txt" selectable="true">{ {detail.taokouling||''}}</text> <!-- 复制的对象-->  
<view class="tblin\_items\_btn" bindtap="copyTBL">一键复制安卓App下载地址</view><!-- 复制操作 -->

  copyTBL2: function (e) {
    var self = this;
    wx.setClipboardData({
      data: "http://todo.echo.cool/",
      success: function (res) {
        // self.setData({copyTip:true}),  
        wx.showModal({
          title: '提示',
          content: '复制成功',
          success: function (res) {
            if (res.confirm) {
              console.log('确定')
            } else if (res.cancel) {
              console.log('取消')
            }
          }
        })
      }
    });
  },

定义Done：

const AV = require('../utils/av-live-query-weapp-min');
class Done extends AV.Object {
  get done() {
    return this.get('done');
  }
  set done(value) {
    this.set('done', value);
  }

  get content() {
    return this.get('content');
  }
  set content(value) {
    this.set('content', value);
  }
}

AV.Object.register(Done, 'Done');
module.exports = Done;

安卓APP：

App({
    options: {
        debug: false
    },
    /\*\*
     \* 当wap2app初始化完成时，会触发 onLaunch
     */
    onLaunch: function() {
        console.log('launch');
    },
    /\*\*
     \* 当wap2app启动，或从后台进入前台显示，会触发 onShow
     */
    onShow: function() {
        console.log('show');
    },
    /\*\*
     \* 当wap2app从前台进入后台，会触发 onHide
     */
    onHide: function() {
        console.log('hide');
    }
});
Page('\_\_W2A\_\_todo.echo.cool', { //首页扩展配置
    onShow: function() {

    },
    onClose: function() {

    }
});

6.7修改 小幅度更改布局，增加分享功能 ![](http://blog.echo.cool/wp-content/uploads/2018/06/Capture-383x600.jpg)