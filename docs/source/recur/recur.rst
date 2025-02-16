Recursive Resolver 
################################


递归(recursive resolver)负责从查询方(client)接收域名记录查询请求，向权威服务器(authoritative server)查询域名记录，最终返回给查询方。

- 按转发查询分类: forwarder resolver, forwarding resolver。

- 按服务提供方分类: ISP resolver, public resolver, open resolver。


user -> local forwarding resolver -> recursive resolver -> authoritative server

递归服务器的安全性、稳定性，直接影响了用户获取域名ip的安全性、稳定性

一个域名在全球服务效果，与该域名在全球重点递归上的应答ip是否正确（非劫持ip）、快速（用户访问该ip的时延短，没有电信用户到联通ip的跨网访问)、稳定(递归能正常访问域名权威，及时获得应答ip)紧密相关

重点递归对域名glue ns及权威ns的ttl处理，直接决定了域名安全事件的风险时间窗

在递归上的优化，往往非常有利于直接提升用户的隐私、安全
- 例如dnssec对dns hijack的防御效果，在权威已部署dnssec的条件下，关键点在于全球重点递归的dnssec验证支持
- 例如root on loopback，对于根服务异常的一个防护措施，可以让递归直接运行根区文件
- 例如qname minimisation，为了减小业务域名泄漏到根、顶级域，可以让递归修正向各级权威查询的域名层次
- 例如ecs，为了保证使用公共递归dns的用户体验，递归向权威发送查询时带上用户的subnet信息，以便权威进行智能解析

然而由于开放递归是全球分布的基础设施，也是dns ddos放大攻击的关键节点。dnssec rr的长度，又加剧了攻击放大比

isp ldns
==========================================================

运营商一般是有少量（比如3～4个）只接收解析请求的前端LDNS、由前端LDNS向后端一堆（比如20多个）负责进行解析的LDNS转发解析请求，后端LDNS再返回该域名NS服务器解析结果给前端LDNS，前端LDNS再返回给用户。

因此，靠近用户的运营商前端LDNS可能远小于靠近域名NS服务器的运营商后端LDNS。

LDNS收到域名解析的一些IP（比如10个）后，在缓存失效前，不会再向域名服务器发请求。如果后端LDNS返回不对IP做轮询处理，而总是以固定的顺序返回，则可能导致该地区用户在每个缓存期总是访问该域名下的某个特定的IP，负载失衡。

因此，单独通过域名解析的IP轮询做负载均衡还不够，还应该在接收服务请求时也做一些负载分担。 

recursive select ns
==========================================================

递归server迭代查询时，收到多个权威ns时的选择算法

见：
- http://www.nanog.org/meetings/nanog54/presentations/Tuesday/TrackYu.pdf
- http://irl.cs.ucla.edu/data/files/papers/res_ns_selection.pdf

这个比较了bind / powerdns / unbound / dnscache / windowsdns，比较全了

要点：
- 往RTT最短的ns查，速度较快
- 但同时要考虑负载均衡的问题，不能老往一个ns上压

问题：
- 短RTT的怎么个优先法
- 长RTT的又怎么办
- 多长时间能发现一个ns的RTT从长变短（也就是服务性能变好了，大家可以用了）


RTT初始化：
- 先测一下初始RTT（全查）
- 或者给所有ns赋一个初始低RTT

选择NS：
- 选RTT最低的
- 或者RTT低于某个阈值的NS里随机选一个

平滑RTT，即计算SRTT：
- 乘一个平滑参数，该参数与上一次RTT值相关
- 更新此次查询的RTT
作用：让长RTT的ns也有机会被选中；发现RTT从长变短的NS

没返回的ns怎么办：
- 定时查
- 直接当成长RTT处理（得等好久才能再一次被选中） 

windows stub query recursive
==========================================================

Windows : DNS 客户端 查询递归的 处理步骤

`DNS server selection by Brent Hu <http://social.technet.microsoft.com/Forums/en-US/winserverNIS/thread/963abb4f-c050-4725-9a92-2be59be3d1d9>`_

`DNS Processes and Interactions <http://technet.microsoft.com/en-us/library/cc772774%28WS.10%29.aspx#w2k3tr_dns_how_gaxc>`_

dns client service：
-  先从 优先级最高的适配器 读取配置的首个dns，发查询，等1秒
-  1秒内没收到应答，读取所有适配器配置的首个dns，发查询，等2秒
-  2秒内没收到应答，读取所有适配器配置的所有dns，发查询，等2秒
-  2秒内没收到应答，读取所有适配器配置的所有dns，发查询，等4秒
-  4秒内没收到应答，读取所有适配器配置的所有dns，发查询，等8秒
-  8秒内没收到应答，就返回time out
-  中间如果有收到应答，就将应答结果写入缓存，停止查询

并且，如果某个适配器上配置的所有dns都没有返回过dns应答包，那么在下一个30秒内，dns client service再收到任何发往这个适配器的、这些dns的查询包，都不去查，而是直接返回time out




