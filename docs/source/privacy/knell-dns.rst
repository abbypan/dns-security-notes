Knell for DNS
####################

`DNS Privacy : NSA’s MORECOWBELL - Knell for DNS <https://gnunet.org/sites/default/files/mcb-en.pdf)>`_

法国人写的，吐槽在nsa监听下的技术应对，综述吧

监测dns query-> 探测解析 -> 收集http信息 -> 监测变化，服务、地理

QUANTUMDNS : 或攻击，或劫持，或故障之

根区文件由IANA维护，由ICANN运维处理。之前ICANN与NTIA有联系，或者说NTIA对ICANN有影响力。NTIA是美国政府背景。2015.12.30日，NTIA-IANA管理权移交。

DNSSEC主要解决劫持问题。NSEC则是否定缓存减轻负载的问题，NSEC3是防快速遍历的问题（要我说，NSEC5是有点走火入魔的问题）。

query minimization，对运维本身是好事，对想知道下面更多东西的上级权威而言就未必了。（递归的重要性进一步扩大。且涉及到中间多层无效解析的问题，有ddos连锁反应）

T-DNS，dns over tls，链路上看不到我查了毛线（除非两端spy，或中间人攻击）

DNS Curve，算是被DNSSEC pk掉的方案之一。权威支持的话，递归以及用户终端都可以应用。需要server/client侧的private/public key对，因此server本身的public key部署又是个事，当然，还是比dnssec少多啦！

DNSCrypt，主要基于dns curve，终端stub找cache recur查的时候，可以用，例如opendns就支持。

Confidential DNS，用ENCRYPT字段发布domain的public key，查NS的时候一起应答。两种模式，authenticated 需要父域支持仍是链式信任； opportunistic 就只是自己发了个key。（个人觉得这个太折腾了，还是over tls更简单点）

namecoin，核心是把信息分散化到blockchain网络上，注册并发布一个名字有一些cost，主打防篡改。

GNU Name System，跟Name coin差不多，弄个DHT查key-value，还是有层次授权信息绑定，到终点提供服务。加密查询应答，加入网络的节点也要帮忙解析。（感觉这个rr频繁修改有可能出毛病，效果未知）
