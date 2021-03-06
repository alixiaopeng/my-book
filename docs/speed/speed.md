
前端的性能优化，可以从下面这几个方向出发：

1. 加载篇
2. 执行篇
3. 用户体验

## 加载
#### 请求服务器资源
- **减少DNS查找**：浏览器在DNS域名解析之前不会下载任何东西，减少域名主机的数量可以减少查询的次数，但可能造成并行下载数的减少，折中方案是内容分布到2-4个不同主机上。
- **重用TCP连接**：尽可能地使用持久连接，以消除TCP握手的延迟。
- **减少重定向**：最简单的比如有时候的跳转页面，直接a标签就行了，不必交给服务器触发重定向
- **使用CDN**：内容分发网络，减少请求延迟
- **删除没必要的资源**：多余资源直接删除
- **客户端缓存资源**：重复数据不必再通过服务器，直接从缓存中读取
- **数据压缩**：开启gzip等等压缩资源
- **减少不必要的请求开销**：如HTTP首部的cookie数据
- **升级HTTP/2.0**：多路复用合并TCP请求、头部压缩、二进制分帧、服务器推送
- **开启负载均衡**：增加并发和吞吐量
#### 页面加载
- **延迟加载组件**：折叠的图片、拖拽相关的库都可以延迟加载
- **预加载组件**：预先加载用户可能用到的资源
- **懒加载**：延迟并非第一视觉展现的组件
- **异步加载js**：异步加载不需要等待的JavaScript文件
- **按需加载CSS**：通过link的media属性按需加载css
- **按需加载组件**：比如使用antd库的时候，使用按需
#### 资源优化
- **图片优化**：响应式图片、压缩图片质量、使用占空间不大的图片格式、尽可能移除颜色为黑白色、循环的HTML5视频代替GIF、css精灵
- **字体优化**：字蛛通过分析本地 CSS 与 HTML 文件获取 WebFont 中没有使用的字符，并将这些字符数据从字体中删除以实现压缩，同时生成跨浏览器使用的格式。
- **音视频优化**：压缩音视频体积
## 执行
- **Web Worker**创建多线程环境，将高延迟任务交给worker负担
- **动画优化**：高性能消耗的动画，可以使用分层canvas缓存
- **避免回流和重绘**：尽量避免浏览器重绘和回流，盒子模型、定位属性、文字相关属性、颜色相关都有机会出发回流和重绘制
- **开启GPU加速**：设置opacity、transform会获得GPU加速
## 用户体验
- **渐进增强**：先设计和构建核心体验，然后为高级浏览器增强体验
- **白屏loading**：从解析url到第一个元素可见中间是白屏阶段
- **骨架屏**：例如"知乎"等网站在加载阶段就展示的是骨架屏，可以在ant design里实现
