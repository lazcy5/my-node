##### github访问很慢的问题

通过域名github.com查询到它的实际IP，本地host绑定一下



mac版

cd /etc

sudo vim hosts

```css
#解决git clone 速度慢的问题
192.30.253.112 github.com
151.101.185.194 github.global.ssl.fastly.net
```

