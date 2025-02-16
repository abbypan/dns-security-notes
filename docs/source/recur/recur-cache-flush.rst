recursive cache flush 
#########################

`A Mechanism for Remote-Triggered DNS Cache Flushes (DNS FLUSH) <http://tools.ietf.org/html/draft-jabley-dnsop-dns-flush-00>`_

让权威主动通知某些递归，有某个域数据变了，不要等ttl过期，赶快flush

用于：

1. DNSSEC域签名认证失败的快速恢复

#. 注册局/注册商服务异常的快速恢复，场景有点类似baidu的ns被改案例

刷新的通信复用DNS NOTIFY的设计，通信认证复用TSIG

这个用于应急不错，好处明显

不过cache估计得限制能给它notify的域，不然搞一堆免费域发notify也容易被调戏 
