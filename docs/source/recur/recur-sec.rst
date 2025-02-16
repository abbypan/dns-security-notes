recursive security
#########################

域名在递归侧异常事件分析
==========================================================

域名在递归侧的安全事件影响程度的关键性指标：递归的重要性（递归服务的用户数），解析IP的风险性(是否高风险），事件持续时间，受影响业务的重要性

解析IP的风险性：
- 正确IP, ok
- 旧版的正确IP，是否ttl过期仍存在，持续未刷新
- 跨网解析IP，例如电信递归获得联通ip
- 故障IP，例如127.0.0.1/0.0.0.0等非公网IP
- 劫持IP
    * 无法成功访问的公网IP
    * squid等缓存服务IP
    * 运营商插入的广告劫持IP
    * 本地路由器插入的广告劫持IP
    * 恶意劫持IP，如包含钓鱼表单、中奖假消息等内容的网页

对于单个公司的业务，终端侧可以采用专用tunnel/overlay的形式进行闪避

然则，对于无dnssec环境下的公网解析，尤其是公共wifi场景，情况往往并不乐观

权威异常时递归的处理
==========================================================

权威ns异常时，递归是否有足够的智能加以判断？

baidu ns篡改事件如何应急?

递归->权威ns出现servfail时是否复用旧ip ?

递归->tld出现fail时，是否利用域名的旧ns ? 

诸如此类，递归运维的选择，直接影响问题域名的事件影响

且往往与ns ttl交织影响

域名已经删除了但仍可以在递归持续解析
==========================================================

http://netsec.ccert.edu.cn/duanhx/archives/1656?lang=zh-hans

清华的paper

假设域名为 somedomain.com

关键点在于，递归从com获取 somedomain.com 的 ns1.somedomain.com之后，相信ns1.somedomain.com发过来的所有消息，包括ns记录！

当com已经删除了somedomain.com时，ns1.somedomain.com已经先跟递归说了还有个ns2.somedomain.com。

ns1.somedomain.com可以定期发包强调当前权威可用，同时update用ttl。保证让递归一直相信下去，不去com问问。。。

解决的时候，一个注意NS要从上级问，还有得按层次检查域名。

权威错误数据传到递归后，递归如何清除缓存
==========================================================

`hijacking-dns-error-ddos-what-happened-and-what-you-can-do <https://www.isc.org/blogs/hijacking-dns-error-ddos-what-happened-and-what-you-can-do/>`_

`How do I flush or delete incorrect records from my recursive server cache <https://kb.isc.org/article/AA-01002>`_

与缓存中毒不同，LinkedIn的问题出在注册商，所以从TLD权威开始就错了。

需要递归主动刷新CACHE，用rndc flush之类的命令


intranet recursive dns
==========================================================

问题根源在于recursive内外混用

线上server使用intranet recur，存在通过该server访问intranet的可能（如网页快照）

切换网络环境时，从intranet recur自动切换成internet recur，访问intranet内容时
- 内部newg dom请求可能泄漏到root上
- 内部传统dom请求如果与外部dom collision，可能泄漏到外部server上

`2013 dotless <http://www.potaroo.net/ispcol/2013-10/dotless.html>`_
讨论了 dotless 在 newg 下，name collision 是否真的会很严重。作者观点：1）更可能出现在上网环境变更，自动切换dns，使得内部查询请求泄漏到root；2）关键在于统一操作系统、浏览器对于dotless的处理。（说实话这问题就是以前乱用留下的债，我也觉得挺无聊）

