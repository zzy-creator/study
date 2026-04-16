### <font style="color:rgba(25, 26, 31, 0.9);">API</font>
<font style="color:rgba(25, 26, 31, 0.9);">API 是计算机程序用来向操作系统、软件库或计算机上运行的任何其他服务提供者，请求服务的一组函数、过程、方法或类。</font>

<font style="color:rgba(25, 26, 31, 0.9);">按照 API 调用时物理链路，可以将 API 分为本地 API 和 远程 AP</font>

+ <font style="color:rgba(25, 26, 31, 0.9);">前者在单个操作系统内部闭环完成</font>
+ <font style="color:rgba(25, 26, 31, 0.9);">后者需要走网络调用</font>

<font style="color:rgba(25, 26, 31, 0.9);">网关服务于远程 API </font>

<font style="color:rgba(25, 26, 31, 0.9);"></font>

### <font style="color:rgba(25, 26, 31, 0.9);">API 网关</font>
**<font style="color:rgba(25, 26, 31, 0.9);">API 网关是客户端和服务端的中间层。它充当反向代理，将请求从客户端路由到服务。它还可以执行各种横切任务，例如身份验证、SSL 终止和速率限制。</font>**

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1744956452576-10e94c4e-9caa-46ba-89ec-950ea688bca8.png" width="1230.4" title="" crop="0,0,1,1" id="u36eafd38" class="ne-image">

**<font style="color:rgba(25, 26, 31, 0.9);">API网关是一种通过单一入口点集中处理所有客户端请求的架构模式</font>**<font style="color:rgba(25, 26, 31, 0.9);">。它解决了微服务架构中客户端如何高效访问不同服务的问题，尤其是在面对细粒度API、不同客户端数据需求、不同网络性能要求以及后端服务动态变化的情况下。</font>

<font style="color:rgba(25, 26, 31, 0.9);"></font>

<font style="color:rgba(25, 26, 31, 0.9);">API 网关作为额外增加的一个中间层，可以带来如下一些好处：</font>

+ **<font style="color:rgba(25, 26, 31, 0.9);">统一接入点</font>**
    - <font style="color:rgba(25, 26, 31, 0.9);">安全性提升：无需暴露内部所有服务；门禁，入口处统一做安全加固、流量控制、访问控制</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">易于观测：流量汇聚点；可注入全链路 traceID；提高 API 调用的可见性</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">简化服务端配置：在网关处统一配置安全策略、部署防火墙等，维护成本更低</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">简化前端接入：只需与单个网关打交道（不用连接多个域名、处理不同的 CORS 和认证方式）；后端服务对前端隐藏，可以轻易变更位置，前端不感知（Location-transparency）</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">集中 API 管理</font>**
    - <font style="color:rgba(25, 26, 31, 0.9);">API 全生命周期管理：设计 -> 开发 -> 测试 -> 发布 -> 管理 -> 下线</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">安全合规策略、数据分析、运营</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">通用能力复用</font>**
    - <font style="color:rgba(25, 26, 31, 0.9);">横向切面职责：协议转换、认证、安全、日志、统计、容错、服务发现等</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">统一下沉到网关，减少建设维护成本，提高业务响应速度</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">前后端解耦</font>**
    - <font style="color:rgba(25, 26, 31, 0.9);">作为「Adapter」：独立变化、兼容旧接口、易于替换、互操作性</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">作为「Facade」：聚合/编排 API 请求、协议转换，简化前端工作</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">可支持 Mock / Stub 能力：方便 API 测试</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">形成API生态</font>**
    - <font style="color:rgba(25, 26, 31, 0.9);">API 服务目录：可发现、可消费、可复用；接入支持（文档 / portal）</font>
    - <font style="color:rgba(25, 26, 31, 0.9);">API 商业变现：账号管理、计量计费、支付管理</font>

<font style="color:rgba(25, 26, 31, 0.9);"></font>

<font style="color:rgba(25, 26, 31, 0.9);">所有中大型公司都会有自己的api网关服务（因为后端都是需要分散成多个服务来处理不同领域的业务逻辑，故需要一个统一的接入层来对前端做接口暴露），所以我们node发送给服的请求其实是先发给了ping-gateway这个网关层，再由网关自己来转发到对应业务服</font>

<font style="color:rgba(25, 26, 31, 0.9);"></font>

### <font style="color:rgba(25, 26, 31, 0.9);">正向代理 反向代理</font>
<font style="color:rgba(25, 26, 31, 0.9);">正向代理：</font>**<font style="color:rgb(51, 51, 51);">"代理服务器"代理了"客户端"，去和"目标服务器"进行交互</font>**

+ **<font style="color:rgb(51, 51, 51);">突破访问限制：</font>**<font style="color:rgb(51, 51, 51);">通过代理服务器，可以突破自身IP访问限制，访问国外网站，教育网等。</font>
+ **<font style="color:rgb(51, 51, 51);">提高访问速度：</font>**<font style="color:rgb(51, 51, 51);">通常代理服务器都设置一个较大的硬盘缓冲区，会将部分请求的响应保存到缓冲区中，当其他用户再访问相同的信息时， 则直接由缓冲区中取出信息，传给用户，以提高访问速度。</font>
+ **<font style="color:rgb(51, 51, 51);">隐藏客户端真实IP：</font>**<font style="color:rgb(51, 51, 51);">上网者也可以通过这种方法隐藏自己的IP，免受攻击。</font>

<font style="color:rgba(25, 26, 31, 0.9);">反向代理：</font>**<font style="color:rgb(51, 51, 51);">"代理服务器"代理了"目标服务器"，去和"客户端"进行交互</font>**

+ **<font style="color:rgb(51, 51, 51);">隐藏服务器真实IP：</font>**<font style="color:rgb(51, 51, 51);">使用反向代理，可以对客户端隐藏服务器的IP地址。</font>
+ **<font style="color:rgb(51, 51, 51);">负载均衡：</font>**<font style="color:rgb(51, 51, 51);">反向代理服务器可以做负载均衡，根据所有真实服务器的负载情况，将客户端请求分发到不同的真实服务器上。</font>
+ **<font style="color:rgb(51, 51, 51);">提高访问速度：</font>**<font style="color:rgb(51, 51, 51);">反向代理服务器可以对于静态内容及短时间内有大量访问请求的动态内容提供缓存服务，提高访问速度。</font>
+ **<font style="color:rgb(51, 51, 51);">提供安全保障：</font>**<font style="color:rgb(51, 51, 51);">反向代理服务器可以作为应用层</font><font style="color:rgb(0, 82, 217);">防火墙</font><font style="color:rgb(51, 51, 51);">，为网站提供对基于Web的攻击行为（例如DoS/DDoS）的防护，更容易排查恶意软件等。还可以为后端服务器统一提供加密和SSL加速（如SSL终端代理），提供HTTP访问认证等。</font>

<font style="color:rgb(51, 51, 51);"></font>

**<font style="color:rgb(0, 0, 0);">正向代理和反向代理的区别</font>**

<font style="color:rgb(51, 51, 51);">虽然正向代理服务器和反向代理服务器所处的位置都是客户端和真实服务器之间，所做的事情也都是把客户端的请求转发给服务器，再把服务器的响应转发给客户端，但是二者之间还是有一定的差异的。</font>

<font style="color:rgb(51, 51, 51);">1、</font>**<font style="color:rgb(51, 51, 51);">正向代理其实是客户端的代理</font>**<font style="color:rgb(51, 51, 51);">，帮助客户端访问其无法访问的服务器资源。</font>**<font style="color:rgb(51, 51, 51);">反向代理则是服务器的代理</font>**<font style="color:rgb(51, 51, 51);">，帮助服务器做负载均衡，安全防护等。</font>

<font style="color:rgb(51, 51, 51);">2、</font>**<font style="color:rgb(51, 51, 51);">正向代理一般是客户端架设的</font>**<font style="color:rgb(51, 51, 51);">，比如在自己的机器上安装一个代理软件。而</font>**<font style="color:rgb(51, 51, 51);">反向代理一般是服务器架设的</font>**<font style="color:rgb(51, 51, 51);">，比如在自己的机器集群中部署一个反向代理服务器。</font>

<font style="color:rgb(51, 51, 51);">3、</font>**<font style="color:rgb(51, 51, 51);">正向代理中，服务器不知道真正的客户端到底是谁</font>**<font style="color:rgb(51, 51, 51);">，以为访问自己的就是真实的客户端。而在</font>**<font style="color:rgb(51, 51, 51);">反向代理中，客户端不知道真正的服务器是谁</font>**<font style="color:rgb(51, 51, 51);">，以为自己访问的就是真实的服务器。</font>

<font style="color:rgb(51, 51, 51);">4、正向代理和反向代理的作用和目的不同。</font>**<font style="color:rgb(51, 51, 51);">正向代理主要是用来解决访问限制问题。而反向代理则是提供负载均衡、安全防护等作用。二者均能提高访问速度。</font>**
