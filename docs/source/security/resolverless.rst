resolverless 
================


如果doh只是把http当成dns的tunnel/proxy，并没有改变解析结构的本质。

反之，如果把doh推进到resolverless，主要有两种场景：

1. 网站返回dnssec记录，相当于隐形的resolver，client可以进行validation，但是基本只适合cdn集中控制子域名的业务。类似于srv rr on http。

#. client无条件信任server提供的一系列ip地址（因为实际上并没有多少子域名部署dnssec），这相当于在安全信任上主动开口，传递信任。由谁来监督server？此外，还有server给到client记录的ttl问题。类似于<img src="https://example.com/img/f.jpg" ip="192.0.2.1">。


好处
-----

1. server可以精准控制具体client的解析ip（cdn厂商喜欢这个），比ecs之类解决的更彻底。

#. 节省到递归的查询时延（其实时延上的好处有限）。

#. 可以少建一些公用递归被当作DDoS攻击的反射器。
