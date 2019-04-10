## 1. 什么是跨域
**跨域**： 浏览器不能执行其他网站的脚本, 由浏览器的同源策略导致
**同源策略** ： 域名、协议、端口均相同

**同源限制了以下**： 
  - Cookie、LocalStorage、IndexedDB 等存储性质内容
  - DOM节点
  - Ajax 请求
  
**三个标签允许跨资源**
- <img src="xxx">
- <link href="xxx">
- <script src="xxx">


## 实现跨域
1. [jsonp](#jsonp)
2. [cors](#cors)
3. [postMessage](#postMessage)
4. document.domain
5. window.name
6. locations.hash
7. http-proxy
8. nginx
9. websocket

## jsonp
Jsonp (json with padding) 
script 标签没有同源策略限制, 可以跨域, 兼容性好

**缺点** 
1. 只能get请求
2. xss 攻击 跨站脚本攻击(Cross Site Scripting)

## cors

## postMessage
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