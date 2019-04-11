## 1. 什么是跨域
**跨域**： 浏览器不能执行其他网站的脚本, 由浏览器的同源策略导致
**同源策略** ： 域名、协议、端口均相同

**同源限制了以下**： 
  - Cookie、LocalStorage、IndexedDB 等存储性质内容
  - DOM节点
  - Ajax 请求
  
**三个标签允许跨资源**
- `<img src="xxx">`
- `<link href="xxx">`
- `<script src="xxx">`


## 实现跨域
- [1. 什么是跨域](#1-%E4%BB%80%E4%B9%88%E6%98%AF%E8%B7%A8%E5%9F%9F)
- [实现跨域](#%E5%AE%9E%E7%8E%B0%E8%B7%A8%E5%9F%9F)
- [1.jsonp](#1jsonp)
- [2.cors](#2cors)
- [3.document.domain](#3documentdomain)
- [4.postMessage](#4postmessage)
- [5.windowName](#5windowname)

## 1.jsonp
Jsonp (json with padding) 
动态创建script标签
script 标签没有同源策略限制, 可以跨域, 兼容性好

**缺点** 
1. 只能get请求
2. xss 攻击 跨站脚本攻击(Cross Site Scripting)

## 2.cors
CORS: "跨域资源共享"（Cross-origin resource sharing）

  1. Access-Control-Allow-Origin
    设置那个源可以访问, `*` 表示任意域名
  2. Access-Control-Allow-Credentials
    布尔值, 表示是否允许接收Cookie
  3. Access-Control-Expose-Headers
    允许返回的头
    CORS XMLHttpRequest 的对象 getResponseHeader() 仅能接受：
    cache-Control、ContentLanguage、Content-Type、Expires、Last-Modified、Pragma
  4. Access-Control-Allow-Headers
    允许携带的头
  5. Access-Control-Allow-Methods
    允许那些方法
  6. Access-Control-Max-Age
    预检测 存活时间毫秒

**兼容性**
需要浏览器和服务器同时支持, 目前所有的浏览器都支持, IE10及以上


## 3.document.domain
适用主域相同, 不同子域之间的跨域
设置相同的主域, 使同源检测通过
```
// a.abin.com
// b.abin.com
document.domain = 'abin.com';
```

## 4.postMessage
完全不同域的跨域
html5引入的API, 用于多窗口间的跨页面通信

```
  otherWindow.postMessage(message, targetOrigin, [transfer])
```
 - message: 传输数据
 - targetOrigin: 返回的窗口对象
 - transfer: 对象所有权传递给消息接受方

接受数据: 监听页面`message`事件的发生

**兼容性**
需要IE11及以上

**安全性**
采用双向安全机制, 通过`event.origin` 来判断是否来自正确可靠的发送方

## 5.windowName
