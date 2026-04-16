DNS （Domain Name System 的缩写）的作用非常简单，就是根据域名查出IP地址。

有了IP也就有了主机网络地址，互联网通信协议中，就可以通过ip定位到具体的公网主机，有了ip才可以建立tcp连接，才会有数据的发送和接收过程，当然这个过程之中还涉及路由、网关、MAC地址、端口、ARP等等，这里就不多说了，可网上查阅资料。

例如，抓包，看到数据如下

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2019/png/13020/1552036389615-16104ff6-7c24-40ba-b3ed-215797bfcd74.png?x-oss-process=image%2Fresize%2Cw_2285%2Climit_0" width="2285" title="" crop="0,0,1,1" id="Ag58E" class="ne-image">

（展开后）

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2019/png/13020/1552036464628-50566382-ba02-4755-8acd-8c23685b2991.png?x-oss-process=image%2Fresize%2Cw_961%2Climit_0" width="961" title="" crop="0,0,1,1" id="BiYfA" class="ne-image">





游戏请求自己后端的服务一般都是使用域名，所以必定要经过dns解析得到ip地址，就像我们的biubiu客户端中，也使用biubiu001.com的域名请求一样，好处之一是只要域名不变，域名后面的机器增加或删除，对前端的调用者而言，可以忽略。



DNS一般使用UDP

https://www.51cto.com/article/658944.html
