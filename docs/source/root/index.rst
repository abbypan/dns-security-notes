说明
=======

`根区文件 <https://www.internic.net/domain/root.zone>`_ 由IANA维护，其中登记了所有顶级域的NS记录。

掌握了根区文件的管理权，相当于掌握了互联网服务解析的入口。

`全球根服务器 <http://www.iana.org/domains/root/servers>`_

IANA -> RIPE/APNIC/ARIN

root server由ICANN管理

时延(RTT)
---------

由于DNS的分层解析架构，根(Root)区访问的时延的短时抖动一般不会对用户终端体验产生明显的影响，而递归(Recursive Resolver)上热点域名的时延的短时抖动可能迅速影响用户终端访问体验。


BGP安全
-------

- 根镜像的BGP路由劫持，可能导致某些区域的域名解析大面积异常。
- 根镜像的BGP路由泄漏，尤其是大型ISP的路由泄漏，可能导致某些区域的根流量被重定向到非最优的路径。

稳定性
------

- 根服务器IP的切换，需要递归侧更新hint文件，应急缓存优化等等
- RFC8806 Running a Root Server Local to a Resolver: 递归侧主动获取根区文件，而非基于hint查询。
- 部署geo及isp选择策略的问题，保证重点地区的镜像覆盖


DNSSEC
-------

根NS的DNSSEC校验链太长的问题，.net下来回切换

13个NS RRSIG太长，未来是否统一成单个root label也ICANN RSSAC组讨论选项中


根服务安全
-----------

本地是否有可信的根镜像服务

根服务器自身的安全性

以DNSSEC为基础，多区域共治，本地anycast优化，递归hint file/root zonefile load定期更新等等

根区密钥轮转，根镜像载入zonefile前后时延

极端场景下，保持与世界互联互通的问题


TLD安全
--------

顶级域在根区生存权管理的问题，谁负责更新根区文件的问题，ICANN移交管理权

极端场景下，保持与世界互联互通的问题


