Hijack 
##########################################################

没有DNSSEC, DNSCrypt, DNSCurve，又或Registrar失守，递归被骗，如何处治？

the logic of hijack location

resolution path : user PC -> ISP recursive / Public recursive -> authoritative ( root, TLD, SLD )

client : PC host file

recursive : the geolocation distribution of influnence clients

recursive : the type distribution of influnence recursive servers, public/isp/company

SLD : the influnence domain type distribution

TLD : the truncate difference of TLD, com/net/cn/...

important business domain authoritative server : same NS, different domain's resolution

recursive log of important business domain : in NS TTL expiration, same hot business domain resolution

root
----------

2014.01 根域劫持事件
==========================================================

劫持定位逻辑题

解析路径：用户PC ->  ISP递归 / 公共递归 -> 各级权威（根 、TLD、二级权威）

终端：终端侧监测host表异常？

递归：影响覆盖递归地理分布？

递归：影响覆盖递归类型（公共、运营商、公司自建）？

二级权威：影响覆盖互联网业务域名分布？

TLD：不同TLD查询截断表现？

重点业务域名权威：同NS下，不同业务域名的解析表现？

递归侧重点业务域名记录：NS的TTL时序内，同一热点业务域名的解析表现？

sld
-----------

2010.01 百度NS事件
==========================================================

主动监测，Glue变更锁定，设法延长未过期NS的递归针对热点域名的有效时长

recursive
---------------

递归侧xxx域名A记录劫持
==========================================================

本地Forwarding Resolver劫持,替换钓鱼IP

本地网关设备劫持,替换热点域名IP,挣钱

运营商侧异常外部劫持,恶意识别

运营商侧广告劫持,省钱

运营商侧缓存劫持,挣钱

运营商篡改正常IP响应/轮换策略,进水

运营商侧本地IP劫持,更加进水

递归侧xxx域名MX记录劫持
==========================================================

邮箱安全

仅次于手机验证码安全

Stub
---------

2018 Mami篡改macOS的stub DNS及本地根证书 
====================================================

`New MaMi Malware targets macOS systems and changes DNS settings <https://securityaffairs.co/wordpress/67709/malware/mami-malware-dns-changer.html>`_
