## 1. 什么是跨域
**跨域**： 浏览器不能执行其他网站的脚本, 由浏览器的同源策略导致
**同源策略** ： 域名、协议、端口均相同

**同源限制了以下**： 
  





协议 域名 端口 同域


## 实现跨域
1. [jsonp](#jsonp)
2. cors
3. postMessage
4. document.domain
5. window.name
6. locations.hash
7. http-proxy
8. nginx
9. websocket

## jsonp
script 标签没有同源策略限制, 可以跨域
**缺点** 只能get请求