improvements to dns resolver 
#################################

`Improvements to DNS Resolvers for Resiliency, Robustness, and Responsiveness <http://tools.ietf.org/html/draft-vixie-dnsext-resimprove-00>`_

主要集中于递归对NS记录的处理，很多细节值得再读，类似于最佳实践总结

1. 父域NS的TTL到期时，重新对其授权进行验证

#. 碰到NXDOMAIN，不再往下查，原有的cache也清掉

#. 授权时获得的NS记录信任度增强

NS
===

1. 由于父域NS的TTL与子域NS的TTL不同步，且子域NS是权威记录，授权生效之后父域NS的TTL基本无意义了（其实就是授权的太彻底）

#.  父域NS的TTL过期后，触发子域NS重新验证；返回cache记录时，要确保该cache来源的NS还没过期（其实就是A与NS也要挂钩）

#.  某个域的重新验证，可能触发其他域也开始重新验证（相同父域上有授权NS更新），离根越近的越先试起

#.  重新验证完成后，还是迅速启动子域提供的NS，而非父域的glue

#.  如果NS有变化，从旧NS覆盖的cache都清掉

#.  重新验证的TTL略小于NS记录的TTL，主要是给验证腾出时间

NXDOMAIN
==========

1. 注意，empty nonterminal domain names 和 nonexistent names 是有区别的，不过现实的NXDOMAIN默认该对象无子域

#. 碰到一个cached NXDOMAIN，停止查询

#. 碰到NXDOMAIN，原来往下的cache都删掉，也都返回NXDOMAIN

#.  查FOO.TLD、BAR.FOO.TLD，如果FOO.TLD不存在，会到TLD查两次；不过下回碰到 xxx.FOO.TLD就直接NXDOMAIN不再查

NS授权的信任
===============

1. child的NS如果覆盖parent的NS，可能导致cache只记得child的结果。如果parent NS挂掉child的NS又太短，悲剧不可避免的发生。

#. 如果触发重新验证，原始的trigger query等到validation query搞完才返回。（RFC不说人话就是这种，举个例不行嘛）

#. 授权NS更新，则一二三四重走一遍

#. 如果父域的NS与子域的NS不同，以子域为准（承认村骗乡，乡骗县的节奏）

安全
=====

1. NXDOMAIN cache poison的受害范围增大

#. 下层域被NS cache poison长TTL影响缓解，因为上层glue有重新验证的时间（如果是在TLD注册的那些域，估计还是够呛）

