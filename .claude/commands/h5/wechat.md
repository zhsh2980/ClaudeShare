---
description: 开发微信生态H5应用
argument-hint: [应用名称]
allowed-tools: Write(*), Edit(*), Bash(*)
---

# 💬 微信小程序H5

构建 $ARGUMENTS 微信H5应用：

## 1. 微信JS-SDK集成
```javascript
// 微信配置
import wx from 'weixin-js-sdk';

class WeixinHelper {
  constructor() {
    this.config = {
      debug: false,
      appId: process.env.WECHAT_APP_ID,
      timestamp: '',
      nonceStr: '',
      signature: '',
      jsApiList: [
        'chooseImage',
        'uploadImage',
        'getLocation',
        'onMenuShareTimeline',
        'onMenuShareAppMessage'
      ]
    };
  }

  async init() {
    // 获取签名
    const signature = await this.getSignature();
    this.config.timestamp = signature.timestamp;
    this.config.nonceStr = signature.nonceStr;
    this.config.signature = signature.signature;

    wx.config(this.config);

    return new Promise((resolve, reject) => {
      wx.ready(() => resolve(wx));
      wx.error((err) => reject(err));
    });
  }

  shareToTimeline(title, link, imgUrl) {
    wx.onMenuShareTimeline({
      title: title,
      link: link,
      imgUrl: imgUrl
    });
  }
}
```

## 2. 微信支付集成
```javascript
class WeixinPay {
  async pay(orderInfo) {
    const payData = await this.getPayParams(orderInfo);

    return new Promise((resolve, reject) => {
      wx.chooseWXPay({
        timestamp: payData.timestamp,
        nonceStr: payData.nonceStr,
        package: payData.package,
        signType: payData.signType,
        paySign: payData.paySign,
        success: (res) => resolve(res),
        fail: (err) => reject(err)
      });
    });
  }
}
```

## 3. 授权登录
```javascript
class WeixinAuth {
  getAuthUrl() {
    const params = new URLSearchParams({
      appid: process.env.WECHAT_APP_ID,
      redirect_uri: encodeURIComponent(window.location.href),
      response_type: 'code',
      scope: 'snsapi_userinfo',
      state: 'STATE'
    });

    return `https://open.weixin.qq.com/connect/oauth2/authorize?${params}#wechat_redirect`;
  }

  async getUserInfo(code) {
    const response = await fetch('/api/wechat/userinfo', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ code })
    });

    return response.json();
  }
}
```

## 4. 小程序跳转
```javascript
// 跳转到小程序
wx.miniProgram.navigateTo({
  url: '/pages/index?param=value'
});

// 返回小程序
wx.miniProgram.navigateBack();
```

应用名称：$ARGUMENTS