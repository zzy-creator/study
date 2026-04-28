快速入门：[https://juejin.cn/post/7097139417151701006](https://juejin.cn/post/7097139417151701006)  
计算属性 vs 方法：[https://cn.vuejs.org/guide/essentials/computed](https://cn.vuejs.org/guide/essentials/computed)

+ 计算属性会缓存，方法不会缓存
+ 计算属性只在响应式数据更新时才会重新计算，方法每次都会执行

vuex：状态管理[https://juejin.cn/post/6928468842377117709#heading-14](https://juejin.cn/post/6928468842377117709#heading-14)

### Vue SSR服务端渲染
renderer渲染器：将组件、模板或数据转换为最终呈现在屏幕上的 HTML、CSS 或其他视觉元素（此过程称为渲染）

ssr服务端渲染的过程：

+ 客户端请求url时，由服务端构建完整html并返回
+ 此时得到的页面是静态的，数据是不具有响应式的，且dom上没有事件挂载
+ 接着客户端在得到完整的html后加载并执行js，进行再次渲染得到具有交互性的界面



node项目的h5页面用的都是ssr的渲染方式

+ node项目是nodejs环境，服务端环境（所以是部署到线上服务器里）。Vue Server Renderer 将 Vue 组件在服务器端渲染成 HTML 静态页面，返回给electron那边的渲染进程（浏览器环境，客户端环境）
+ 在Entry的实现里面判断了当前的环境是客户端还是服务端，会进行不同的init（客户端里会把vue组件挂载上去）



详细了解：

[https://www.whyyy.net/blog/fe-nuxt/#before](https://www.whyyy.net/blog/fe-nuxt/#before) 各个渲染模式的概念、流程

[https://juejin.cn/post/7021521450611769380#heading-0](https://juejin.cn/post/7021521450611769380#heading-0) 简单入门、简单的代码示例

[https://v2.ssr.vuejs.org/zh/](https://v2.ssr.vuejs.org/zh/) 全面的指南


