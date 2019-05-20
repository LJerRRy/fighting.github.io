---
layout: post
title: 如何配置Nginx使得http重定向到https
date: 2019-05-20 22:47:01
catalog:    true
author: "Jerry"
header-img: "img/post-bg-os-metro.jpg"
tags: 
    - Nginx
---

## 如何配置Nginx使得http重定向到https

这个其实是很简单的， 只需要配置如下代码

```
server {
    listen 80;
    server_name  yourserve_name;
    return 301 https://$server_name$request_uri; // 这行进行重定向
    # rewrite ^(.*)$  https://$host$1 permanent; // 或者rewrite也可以
}
```

但是我这样配置遇到<p style="color:red">网页生成了过多的重定向。清除此网站的Cookie</p>的问题，原来，我https中又配置了`proxy_pass http://yourserve_name;`导致这个错误，浪费我半小时找这个错误，/(ㄒoㄒ)/~~，不过下次应该就知道了


ps. Nginx有必要去学习学习



