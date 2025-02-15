DNS-SD ( DNS-Based Service Discovery )
==========================================================

RFC6763
----------------------------------------------------

参考： `DNS Service Discovery (DNS-SD) <http://www.dns-sd.org/>`_

如果1楼的人查询 _ipp._tcp.example.com. 的SRV记录，随机选了一个7楼的打印机，显然是不合适的

因此，接着SRV记录的思路，加入服务实例的标识

先查询 _ipp._tcp.example.com. 的PTR记录，得到一堆服务实例域名的SRV信息

.. raw::

    Service Instance Name = <Instance> . <Service> . <Domain>

然后再选取其中1个实例域名，查询其TXT记录（此时还能支持一些key-value属性对）


dnssd privacy and security 
----------------------------------------------------------

RFC8882:  DNS-Based Service Discovery (DNS-SD) Privacy and Security Requirements

dnssd over mdns 不可避免的会泄漏某些信息。

核心是：是否泄漏identity信息、与business/social关联的信息(linkable identifiers)，client interest 等等

authenticity, integrity, freshness, confidentiality

dicitionary attack, ddos, sender impersonation, sender deniability

快稳省

信息锚点：pki, tofu, pake

