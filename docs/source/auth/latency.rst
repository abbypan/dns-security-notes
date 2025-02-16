latency
##########################################################


权威dns时延分析
==========================================================

`Measuring Query Latency of Top Level DNS Servers <http://netsec.ccert.edu.cn/duanhx/files/2013/02/latency.pdf>`_

多个分布式探测点，探测权威ns时延

1. 每个节点每n分钟发1个udp包，每个包等5s , 简单 , 受网络丢包影响

#. 每个节点每n分钟同时发s个udp包，每个包等5s , 简单 , 权威ns较多时，发包也多。每个节点每n分钟同时发s个udp包，每个包等5s。支持量化评估权威时延。

#. 每个节点先发1个udp包，超过t秒无返回，再发第2个包，最多重试x次 , 避免偶然丢包的影响 , 某些情况下权威ns查询时延/失败波动被主动忽略。一般用于时延报警策略误报优化，不用于基础数据探测。当等待时延t设置小于某些真实时延时，最终得出的时延与实际情况有偏差，且未知增减：
    - <=t秒：无影响
    - 重试x次，写入x*t + succ_rtt：影响可能偏大
    - 重试x次，写入succ_rtt：影响偏小
    - 重试x次，均未在t秒内返回，返回失败：影响偏大

NXDOMAIN-QUERY
==========================================================

    client到根的rtt：client 向递归 dns_r 查不存在的tld域名查询，那么递归dns_r就会去根root查。 

    client到递归的rtt：理论上可以发非递归的查询请求（不过实际上经常没用），或者查一个已缓存的域名。

    最终得到 递归dns_r到根root 的时延：T(dns_r , root) = T(c, root) - T(c,r)


这个方法只能得到递归dns_r到指定域（例如root）下的整体时延。

但不清楚是到这个域下的哪个具体ns server的时延，因为递归dns_r对同一个域下的多个ns的选择算法可能不同。

文章中用这个方法测了root，.com / .net / .org 等流行tld。


KING root
==========================================================

用king法测量递归到13个根的时延，测的是到13个根anycast ip的rtt

注意，这边的误差在于，这些ip做了全球anycast，递归的真实rtt可能不是去到king法选的路径上

用king法测量给出了F、L根的unicast ip的RTT，并与上面anycast ip的rtt做对比，可衡量unicast镜像的作用啥的

此外还用fpdns探测了一下bind版本 

king end host
----------------------------------------------------

`King: Estimating Latency between Arbitrary Internet End Hosts <http://homes.cs.washington.edu/~gribble/papers/king.pdf>`_

利用dns测两个ip之间的RTT
- ip_a 本地网段有个递归 dns_r
- ip_b 本地网段有个域 somedomain.com 的权威 dns_a
- 认为RTT(ip_a, ip_b)可以约等于RTT(dns_r, dns_a)


RTT(dns_r, dns_a) 可以用以下方法计算：
- 从节点c 向 dns_r 请求 somedomain.com 下的一个不存在的域名，RTT(dns_a, c)
- 从节点c 向 dns_r 发ping包，或查询一个dns cache记录，RTT(dns_r, c)
- RTT(dns_r, dns_a) = RTT(dns_a, c) - RTT(dns_r, c)

这边要考虑 somedomain.com 有多个权威dns_a的情况。

要先确定当前dns_r会去查的是哪个dns_a。

假设dns_r查到somedomain.com的ns
- ns1.somedomain.com
- ns2.somedomain.com

并且 ns1.somedomain.com 对应的dns_a是
- xxx.xxx.xxx.xxx
- yyy.yyy.yyy.yyy

根据dns_r的配置不同选择看法，可能选择查询的dns_a不同 
