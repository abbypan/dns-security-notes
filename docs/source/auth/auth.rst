authoritative server
#########################

Authority DNS解析的性能更多是取决于NS记录的缓存时间，单独把A记录的TTL调低没太大影响

反向解析比正向解析多，比例约为3:2

lame server表示该dns不负责某个网域的解析，但是却将该网域的ns记录指向此dns

正常情况下，99%的dns查询走udp

global server load balancing (GSLB)-type DNS ：根据发起请求的用户所在地，返回不同的ip

tld
==========================================================

`OARC TLDmon Service <https://www.dns-oarc.net/oarc/services/tldmon>`_

`tldmon nagios <https://tldmon.dns-oarc.net/nagios/>`_

`tldmon history <https://tldmon.dns-oarc.net/history/>`_


sld
==========================================================

zone 授权
----------------------------------------------------

存在跨层授权。

例如递归已知 aaa.yyy.com / xxx.aaa.yyy.com 都不存在，无法推断 zzz.aaa.yyy.com 是否存在。

因为 zzz.aaa.yyy.com 理论上有可能在 yyy.com 上直接授权。

同理，XXX.abc.com (XXX为随机数)，即使已知 abc.com 不存在，也会到 com 查一遍。

nxdomain cut的问题。

权威NS更新
----------------------------------------------------

对域名testxxx.com做ns记录修改，本地ns服务器ns.new.net提供该域名解析

在域名注册商处修改ns成功：原来是 ns.old.net ，现在是ns.new.net

dig testxxx.com -t ns  本地查询返回ns.old.net

dig testxxx.com -t ns +trace 从根开始问到底，中间在com.处返回ns.new.net；继续问ns.new.net时，又返回ns.old.net

在com.和 ns.new.net返回两次testxxx.com的ns，分别是一新一旧两个记录

这是因为ns.new.net上配置了testxxx.com的ns记录是ns.old.net

在域名注册商处把ns记录换成ns.new.net，父域com.的ns知道有改动了，但是ns.new.net上的旧记录没有更新。


