catalog zone
==========================================================

draft-muks-dnsop-dns-catalog-zones

catalog zone，用于记录与一个域自身配置相关的信息，思路类似于配置通过DNS记录自举

不过把ACL策略放这里让人看总觉得有点那啥……

allow-query.catalog1.example.org. 3600 IN APL (1:192.0.2.0/24 2:2001:db8::/32)

