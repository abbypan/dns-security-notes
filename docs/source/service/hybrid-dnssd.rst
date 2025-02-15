hybrid dnssd
==========================================================

`Hybrid Unicast/Multicast DNS-Based Service Discovery <https://tools.ietf.org/html/draft-cheshire-dnssd-hybrid>`_

dns-sd同时支持组播与单播。 例如apple用dns-sd组播查询，与mdns结合，可以自动获取本地服务实例的端口及IP地址信息。

但是由于mdns只支持本地组播，无法处理多局域网的本地服务发现。

hybrid方案是用Multicast Discovery Proxy，在各本地链路仍是mdns，但是不同链路有不同的Unicast DNS namespace。

这个Multicast Discovery Proxy可以用VLAN trunk port模式出现在各局域网链路。。。

client同时发组播跟单播查Domain Enumeration的PTR记录：

1. 如果应答里给了Unicast DNS name: example.com，那么client就单播再查example.com下面的PTR

    .. raw::

        b._dns-sd._udp.example.com.    PTR   Building 1.example.com.
                                              PTR   Building 2.example.com.
                                              PTR   Building 3.example.com.
                                              PTR   Building 4.example.com.

    再用该PTR记录查SRV

    My Printer._ipp._tcp.Building 1.example.com.
                                  SRV 0 0 631 prnt.bldg1.example.com.
    prnt.bldg1.example.com.       A   203.0.113.2


#. client 同时发 .local 域下的组播查询

    .. raw::

    My Printer._ipp._tcp.local. SRV 0 0 631 prnt.local.
    prnt.local.                 A   203.0.113.2

最终可兼用两者返回结果。
