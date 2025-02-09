根镜像(Anycast)
===============

`全球根镜像 <http://www.root-servers.org/>`_

根镜像部署涉及地理区域、运营商选择策略，保证覆盖全球重点地区。

根镜像的评估指标
----------------

RTT时延，跨境访问，跨网访问，本地vs异地


F根
---

看当前访问的F根的镜像

    dig hostname.bind @f.root-servers.net chaos txt
    traceroute @f.root-servers.net

K根
----

看当前访问的K根的镜像

    dig id.server @k.root-servers.net chaos txt
    traceroute @k.root-servers.net

L根
----

参考draft-jabley-dnsop-anycast-mapping-04

看L根的镜像列表

    dig NODES.L.ROOT-SERVERS.ORG TXT +short +tcp

看当前访问的L根的镜像

    dig -4 @L.ROOT-SERVERS.NET ID.SERVER CH TXT +short
    dig -6 @L.ROOT-SERVERS.NET ID.SERVER CH TXT +short
    dig IDENTITY.L.ROOT-SERVERS.ORG TXT +short 
    dig IDENTITY.L.ROOT-SERVERS.ORG A +short


参考资料
--------------

- `anycast介绍 <http://www.net.cmu.edu/pres/anycast/>`_
- `dns anycast实作 <http://netlinxinc.com/netlinx-blog/45-dns.html?layout=default>`_
- `anycast 对比 unicast 的好处 <http://communitydns.eu/Anycast.pdf>`_
- `cisco Challenges to DNS Scaling <http://www.cisco.com/web/about/ac123/ac147/archived_issues/ipj_14-4/144_dns.html>`_
- `icann 2009.08.Scaling the Root Report on the Impact on the DNS Root System of Increasing the Size and Volatility of the Root Zone <https://www.icann.org/en/system/files/files/root-scaling-study-report-31aug09-en.pdf>`_
- `icann 2009.09.Root Scaling Study Description of the DNS Root Scaling Model <https://www.icann.org/en/system/files/files/root-scaling-model-description-29sep09-en.pdf>`_
- `icann 2010.10 Summary of the Impact of Root Zone Scaling <https://www.icann.org/en/topics/new-gtlds/summary-of-impact-root-zone-scaling-06oct10-en.pdf>`_

