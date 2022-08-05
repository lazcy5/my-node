```javascript
import Config from "../config/config";

/**
 * 请求接口数据
 * url
 * data 参数  object
 * type 请求类型  大写
 */
export default class Fetch {
  static request(url, data, type, resetHeader) {
    return new Promise((resolve, reject) => {
      try {
        // 获取登录用户信息
        const loginUserInfo = wx.getStorageSync("user") || "";
        const sessionId = loginUserInfo.sessionId || "";
        let header = resetHeader || {
          "content-type": type === 'POST' ? "application/json; charset=utf-8" : "application/x-www-form-urlencoded",
          platform: "5",
        };
        let reqUrl = url + '?source=WEIXIN&appSid=' + sessionId;
        // 分页POST请求是拼接一下分页参数到请求路径上
        if(type === 'POST') {
          reqUrl = data?.pageNo ? reqUrl + '&pageNo=' + data.pageNo : reqUrl;
          reqUrl = data?.pageSize ? reqUrl + '&pageSize=' + data.pageSize : reqUrl;
        }
        wx.request({
          url: Config.baseUrl + reqUrl,
          data: {
            ...data
          },
          method: type || "GET",
          header: header,
          success: res => {
            if (res.data.status === "C0000") {
              resolve(res.data);
            } else if (res.data.status === "E0009" || res.data.status === "E0004") {
              // 登录失效  sessionId 30天失效后
              wx.removeStorageSync("user");
              wx.removeStorageSync("userinfo");
              wx.showToast({
                title: '未登录，请登录后再查看',
                icon: 'none'
              })
              setTimeout(() => {
                wx.reLaunch({
                  url: "/pages/auth-login/index"
                });
              }, 2000)
              console.log(`终止接口${url}的请求：${res.data.message}`);
            } else {
              console.log(`接口${url}返回的错误信息：${res.data.message}`);
              resolve(res.data);
            }
          },
          fail: err => {
            console.log(err);
            wx.showToast({
              title: err.message || '服务器异常',
              icon: 'none'
            })
            reject(new Error("服务器异常"));
          }
        });
      } catch (error) {
        console.log(error);
        wx.showToast({
          title: error.message || '服务器异常',
          icon: 'none'
        })
        reject(new Error("服务器异常"));
      }
    });
  }
}

```

