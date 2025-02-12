## IP

互联网协定(internet Protocol)，简称：IP，现实中寄快递送外卖需要知道位置，在互联网的世界里IP就相当于现实里的地址

浏览网站等于是你的电脑向另一部电脑获取信息，你的电脑向另一台电脑的IP地址发送信息，同时也附带着自己的IP地址



## DNS

域名解析系统(DNS)，可以让域名与对应的IP地址关联在一起，比如当你访问www.baidu.com，你的电脑会使用DNS查询解析域名，来获取对应的IP地址









##当我从浏览器输入一个url后到页面渲染出来之间发生了什么

当你从浏览器输入一个 URL 并按下回车键后，到页面最终渲染出来之间，发生了许多复杂的步骤。这个过程可以大致分为以下几个阶段：

---

### 1. **URL 解析**
   - 浏览器解析你输入的 URL，确定协议（如 `http` 或 `https`）、域名、端口号（默认是 80 或 443）、路径和查询参数。
   - 如果 URL 不完整（例如只输入了域名），浏览器会尝试补全（如自动添加 `http://` 或 `https://`）。

---

### 2. **DNS 查询**
   - 浏览器需要将域名（如 `www.example.com`）转换为服务器的 IP 地址。
   - 浏览器首先检查本地缓存（如浏览器缓存、操作系统缓存）中是否有该域名的 IP 地址。
   - 如果缓存中没有，浏览器会向配置的 DNS 服务器发送请求，递归查询域名对应的 IP 地址。
   - DNS 查询过程：
     1. 查询本地 DNS 缓存。
     2. 向根域名服务器查询。
     3. 向顶级域名服务器（如 `.com`）查询。
     4. 向权威域名服务器查询，最终获取 IP 地址。

---

### 3. **建立 TCP 连接**
   - 浏览器通过 IP 地址和端口号与服务器建立 TCP 连接。
   - 如果是 HTTPS 协议，还会进行 TLS/SSL 握手，建立加密通道。
   - **三次握手**：
     1. 客户端发送 SYN 包到服务器。
     2. 服务器回复 SYN-ACK 包。
     3. 客户端发送 ACK 包，连接建立。

---

### 4. **发送 HTTP 请求**
   - 浏览器向服务器发送 HTTP 请求，请求中包含请求方法（如 `GET` 或 `POST`）、路径、请求头（如 `User-Agent`、`Accept` 等）和可能的请求体（如 POST 请求的数据）。
   - 示例：
     ```
     GET /index.html HTTP/1.1
     Host: www.example.com
     User-Agent: Mozilla/5.0
     Accept: text/html
     ```

---

### 5. **服务器处理请求**
   - 服务器接收到请求后，根据路径和参数处理请求。
   - 服务器可能会执行后端逻辑（如查询数据库、调用 API 等），然后生成响应。
   - 响应通常包括状态码（如 `200 OK`）、响应头（如 `Content-Type`）和响应体（如 HTML 文件）。

---

### 6. **接收 HTTP 响应**
   - 浏览器接收到服务器的响应。
   - 如果状态码是 `200 OK`，浏览器开始解析响应体（通常是 HTML 文件）。
   - 如果状态码是 `301` 或 `302`，浏览器会重定向到新的 URL。

---

### 7. **解析 HTML 并构建 DOM 树**
   - 浏览器解析 HTML 文件，将其转换为 **DOM（文档对象模型）树**。
   - 解析过程中，如果遇到 `<script>`、`<link>` 或 `<img>` 等标签，浏览器会发起额外的请求来加载这些资源。
   - **DOM 树** 是浏览器对 HTML 的结构化表示，用于后续的渲染。

---

### 8. **加载外部资源**
   - 浏览器根据 HTML 中的标签（如 `<script>`、`<link>`、`<img>`）加载外部资源（如 JavaScript、CSS、图片等）。
   - 加载过程是并行的，但某些资源（如 JavaScript）可能会阻塞 DOM 树的构建和渲染。

---

### 9. **解析 CSS 并构建 CSSOM 树**
   - 浏览器解析 CSS 文件，将其转换为 **CSSOM（CSS 对象模型）树**。
   - CSSOM 树与 DOM 树结合，形成 **渲染树（Render Tree）**。

---

### 10. **执行 JavaScript**
   - 浏览器解析并执行 JavaScript 代码。
   - JavaScript 可能会修改 DOM 或 CSSOM，导致浏览器重新构建渲染树。

---

### 11. **布局（Layout）**
   - 浏览器根据渲染树计算每个元素在页面中的位置和大小（即布局或回流）。
   - 布局是一个递归过程，从根元素开始，逐级计算子元素的位置。

---

### 12. **绘制（Paint）**
   - 浏览器将渲染树中的每个元素绘制到屏幕上。
   - 绘制过程包括将元素的颜色、边框、背景等绘制到页面上。

---

### 13. **合成（Compositing）**
   - 如果页面有复杂的图层（如动画、3D 变换等），浏览器会将不同的图层合成到一起，最终显示在屏幕上。

---

### 14. **页面渲染完成**
   - 页面完全渲染出来，用户可以与之交互。
   - 如果页面中有异步加载的资源（如懒加载图片），浏览器会在资源加载完成后更新页面。

---

### 总结
从输入 URL 到页面渲染完成的过程可以简化为以下步骤：
1. URL 解析 → 2. DNS 查询 → 3. TCP 连接 → 4. HTTP 请求 → 5. 服务器处理 → 6. HTTP 响应 → 7. 解析 HTML → 8. 加载资源 → 9. 解析 CSS → 10. 执行 JavaScript → 11. 布局 → 12. 绘制 → 13. 合成 → 14. 页面渲染完成。

这个过程涉及浏览器、网络、服务器和后端逻辑的协同工作，每一步都可能影响页面的加载速度和用户体验。