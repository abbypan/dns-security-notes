Discovery of Network-designated Resolvers (DNR) 
==========================================================

`RFC9463 DHCP and Router Advertisement Options for the Discovery of Network-designated Resolvers (DNR) <https://datatracker.ietf.org/doc/rfc9463/>`_

内容比较简单，就是DHCP/RA把ADN(Authenticated Domain Name)、或者IP Address + Port 同步一下。

信任锚点的问题仍然存在。区分managed CPE & unmanaged CPE。

DHCP/RA的合法性：
- DHCPv6-Shield : RFC7610，CPE扔掉local endpoint的DHCP Response message
- RA-Guard: RFC7113, CPE扔掉local endpoint的RA message
- Source Address Validation Improvement (SAVI) for DHCP: RFC7513, CPE过滤fourged source IP addresses packets
