TLSA
#######

RFC6698: TLSA

`DANE und DNSSEC <https://www.fehcom.de/pub/DANE.pdf>`_

`The DNS-Based Authentication of Named Entities (DANE) Transport Layer Security (TLS) Protocol: TLSA <https://tools.ietf.org/html/rfc6698>`_

复用dnssec基础设施，发布 tls 的ca，而非通过传统的 ca chain

client 查 www.example.com 的时候可以顺便返回tlsa记录

.. raw::

     _443._tcp.www.example.com. IN TLSA (
          0 0 1 xxxxxxxxxxxxxxx )

相当于信任锚点的转移，域名可以自行签发ca证书，重要的事情说三遍。。。

ssl proxy 型的中间人攻击没法用了，主要是在底层协议ca检查过不了。

