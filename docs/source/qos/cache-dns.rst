cache dns/forwarding resolver 评测指标
###########################################

缓存递归DNS服务器评测点

吞吐量
==========================================================

每秒支持多少次查询

测吞吐量可以用resperf

- 一次查询所需的CPU time，网卡吞吐量，带宽，缓存命中时能支持的最大查询次数p，缓存未命中时能支持的最大查询次数q；

- 实际的吞吐量介于p与q之间，靠近p还是靠近q与实际查询命中率相关；

- q还与递归查询的深度有关

时延
==========================================================

平均每次查询返回时长

相关参数：重复查询量，网络质量，失败查询率，客户端查询失败后的重试次数，客户端超时重试时长

客户端超时重试时长与bind8及其之前的查询算法有关：
- bind发现找不到name server的ip，会马上跑去查；
- 但是查完之后，不会再去查客户端之前发起的query，而会等客户端超时重试再去查；
- 此时总时延就与客户端超时重试时长有关

测时延可以用dnsperf

解析查询包
==========================================================

解析查询流量的pcap包可以用queryparse
