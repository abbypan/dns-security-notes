DNSCURVE
##########

概要
=====

`DNSCurve: Usable security for DNS <http://www.dnscurve.org/index.html>`_

`Shaping DNS Security with Curves <http://curvedns.on2it.net/get/shaping_dns_security_with_curves.pdf>`_

`CurveDNS <http://curvedns.on2it.net/>`_

注意，DNSCURVE提供点到点的安全，而非端到端；也就是说，能保证采用DNSCURVE通信的相邻两节点DNS查询/应答通信数据的加密、认证。

针对“NS”的公钥认证，维护成本较低；一个NS可以有多个公私钥对

挑战码+DH交换协商对称密钥，支持加密通信

客户端时间不准对解析结果无影响，抗重放攻击

不会降低外部探知整个域配置的难度

没有引入新RR，域名配置文件略微增大，主要是NS记录比以前长，可以继续用UDP

耗CPU的攻击威胁增大，每个包都要涉及加解密计算，否定缓存应答不需要特殊处理

放大攻击的风险较小

draft
==========================================================

https://tools.ietf.org/html/draft-dempsky-dnscurve-01

`Cryptography in NaCl <http://cr.yp.to/highspeed/naclcrypto-20090310.pdf>`_

加密算法
----------------------------------------------------

.. note::

    c = aes(aes_key, src_data)
    h = sha256(c)
    s = rsa_client_private_sign(h)
    key_s = rsa_server_public_encrypt(aes_key, h, s)
    main_data = concat(key_s, c)

两种通信方案
----------------------------------------------------

Streamlined Format ：解包，cryptbox 直接是原始DNS查询、应答包

TXT Format：解压TXT，把内容提取出来，跟header组装成DNS查询、应答包

过程
----------------------------------------------------

client : client public key, client_nonce, cryptbox query

server : 用 server private key 解密，用 client public key 验证

server ：搞一个 server_nonce，附在 client_nonce 之后，在应答包里用server private加密传回去

client ：解包，验nonce，验DATA


讨论
------

改动量比较大，保密性太好了，又比较耗资源，以致于没法让大家往下用。。。


