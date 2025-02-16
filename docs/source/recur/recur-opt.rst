recursive option test
==========================================================

测试edns & 后端resolver ip
----------------------------------------------------

    dig o-o.myaddr.l.google.com -t txt +short
    
    dig -t a whoami.v4.powerdns.org
    dig -t txt whoami.v4.powerdns.org
    dig -t txt whoami-ecs.v4.powerdns.org

    dig -t aaaa whoami.v6.powerdns.org
    dig -t txt whoami.v6.powerdns.org
    dig -t txt whoami-ecs.v6.powerdns.org

测试端口随机性 port randomness test
----------------------------------------------------

见：https://www.dns-oarc.net/oarc/services/porttest

把porttest.dns-oarc.net查询CNAME到z.y.x.w.v.u.t.s.r.q.p.o.n.m.l.k.j.i.h.g.f.e.d.c.b.a.pt.dns-oarc.net，计算这随后26个查询包源端口的标准差 

测试递归是否支持DNSSEC查询
----------------------------------------------------

    dig com. SOA +dnssec @8.8.8.8


测试递归DNS是否支持EDNS0
----------------------------------------------------

    dig com. ns +bufsize=4096 @61.139.2.69


测试递归可支持的RESPONSE长度
----------------------------------------------------

`OARC s DNS Reply Size Test Server <https://www.dns-oarc.net/oarc/services/replysizetest>`_

用户 <-> 递归（前端cache，后端forwarder）<-> 权威

oarc这个服务只能测单个链路(递归<->oarc权威)的edns支持情况，是否支持edns0的结论一般跟实际情况差别不会太大，测出的支持edns0最大长度则可能与实际不太一致（因为不同链路实际情况不同）。

当然是否支持edns0的结论也可能出错，当 用户<->某个递归 edns0正常，但是该递归<->oarc权威 edns0失败，就会出现不一致的探测结果。

分析
==========================================================

如果递归不支持EDNS，则无法接收超过512字节的数据

如果递归所在的防火墙过滤IP碎片或过滤>512字节的DNS应答包，则大块的RESPONSE数据可能会被丢掉

BIND 9.5.0 之后，递归查询如果time out，会把edns的buffer长度设回512

测试：``dig +short rs.dns-oarc.net txt @8.8.8.8``

跟递归说支持1024的buffer：``dig +bufsize=1024 rs.dns-oarc.net txt @8.8.8.8``

 注意这里1024只是dig查询时跟递归8.8.8.8说的，8.8.8.8查询的时候再转，跟 8.8.8.8 <-> dns-oarc权威实际支持的长度无关

 Nominum CNS只在收到truncated应答时才会发起带EDNS的查询，因此，针对Nominum CNS型的递归xxx.xxx.xxx.xxx，应答时TC置位迫使其用EDNS查：

``dig tcf.rs.dns-oarc.net txt @xxx.xxx.xxx.xxx``
 
检测原理
==========================================================

一次查询多次CNAME检测

每次查询，server通过填充authority/additional域数据，得到多个不同长度的应答包（CNAME域名里带了这个长度信息），按从大到小的次序发出。

假设每次收到的应答包长度都是可接受的最长的，几次CNAME折半后就能逼近最终长度

最终返回TXT记录，包含了上述测试的长度，以及是否支持EDNS的判断

注意
==========================================================

这个只能测 递归<->oarc权威之间的链路，没法测 用户<->递归 之间的链路

对于forwarder的情况，用一些不常见的RR填充数据包可能会更好一点
