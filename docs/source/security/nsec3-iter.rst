NSEC3PARAM iteration count
#############################



背景
==========================================================

NSEC3PARAM 的hash迭代次数问题

Iterations标记计算hash时的迭代次数，取值为0其实是用1次salt，逗比……

.. raw::

      IH(salt, x, 0) = H(x || salt), and
      IH(salt, x, k) = H(IH(salt, x, k-1) || salt), if k > 0

这就有了：迭代次数的开销问题。

迭代次数太多的cpu cost以及攻击风险。

迭代次数不够导致的insecure denial of existence问题（概率低）。


问题
==========================================================

有多少域名部署了NSEC3？

有多少域名正确配置了NSEC3算法适合的Iterations？

有多少域名启用了合适的salt？

有多少域名真正需要NSEC3？


解决？
==========================================================

限制Iterations<150 ？

推荐Iterations最好为 0 / 1 ？

精明的verisign取Iterations=0，置salt为空，无比和谐，效果已经尽可能接近NSEC了：

.. raw::

    $ dig +dnssec avwwwvadkllksjfwalskjfv.com

    ; <<>> DiG 9.11.2 <<>> +dnssec avwwwvadkllksjfwalskjfv.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 26495
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 8, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;avwwwvadkllksjfwalskjfv.com.	IN	A

    ;; AUTHORITY SECTION:
    com.			899	IN	SOA	a.gtld-servers.net. nstld.verisign-grs.com. 1515390115 1800 900 604800 86400
    com.			899	IN	RRSIG	SOA 8 1 900 20180115054155 20180108043155 11324 com. NPYJ+jXqNUokYhx+JQes65fxwX81lCHcWoZCP3LRm2cCt4eEzPqi6AhA tG0WxQMM+iA6ZoTnRHY9o9QiANEmZKPKqqnyiICYM21OJZUgr7eRuJ/l gGvF+04pRztbYmnMk2rM5hJ7AbYWcDWh1mm0586Ghuyc6EEzNRepqxmU GOg=
    CK0POJMG874LJREF7EFN8430QVIT8BSM.com. 86399 IN NSEC3 1 1 0 - CK0Q1GIN43N1ARRC9OSM6QPQR81H5M9A  NS SOA RRSIG DNSKEY NSEC3PARAM
    CK0POJMG874LJREF7EFN8430QVIT8BSM.com. 86399 IN RRSIG NSEC3 8 2 86400 20180112055033 20180105044033 11324 com. cMyjjxb3+ZyjbPKje2t8/kaIFpxDBOV35kILoxO1QX95qBvoiBXAzJdd WNqKwcIPUuy+k3KlguxJIWCNqs6ujyT7qqXnthDqjt3uvyGIgzdLkeXt fN4NkcsQ5dDsfLFpRreEiPe9G0g4UROSJBYJW3qzGPe2mvpleF4Gk9a/ 3r8=
    VCH6DHAVTOGEHJQOTJN3P41D3TQU8P8F.com. 86399 IN NSEC3 1 1 0 - VCH8QMTP2B5UKJEMQQUS1METJ0QVONCA  NS DS RRSIG
    VCH6DHAVTOGEHJQOTJN3P41D3TQU8P8F.com. 86399 IN RRSIG NSEC3 8 2 86400 20180112053458 20180105042458 11324 com. IEypMBmuiuEgJ81Dsyjk00Joge49+ofC8pUVVmDmq4SEZk5AZRGIkhC6 B1/mtu28HlYvzs5y7O6Eao28ZWs77CDyK92W6mbORwpIXOlPtNBXxBXV sQFkRKTE1iAP0LUfyNT0+V49eUpYKKgKMiPmdC2buEU5zClXqBirykVV uoM=
    3RL20VCNK6KV8OT9TDIJPI0JU1SS6ONS.com. 86399 IN NSEC3 1 1 0 - 3RL3ODP8D910939I655B97GAQU6VE1Q7  NS DS RRSIG
    3RL20VCNK6KV8OT9TDIJPI0JU1SS6ONS.com. 86399 IN RRSIG NSEC3 8 2 86400 20180113052606 20180106041606 11324 com. QrK+/VpRwCufqQFbjVajvy6xFmauXjEeVQj1aSqL+5FNtv8QxeJVI7bj 18c2GZ00ZD+Tizmm+GtATpV/CC6v3nQkU6cCbRW4i6xeqtPtE/U1qdAv 70TXDu+pAZax1DmwK4CUIuYjkk6rTfJxsquqcFYOoY8xdEmzr9LQbeDH KNE=


讨论
==========================================================

针对verisign这种使用场景，那么NSEC3的意义是？NSEC的薄马甲？

NSEC5不是折腾的答案。

然而我们并不知道有多少域真正需要隐藏子域。


NSEC3 + OptOut
==========================================================

OptOut的场景是，TLD有海量子域名，但并不想全部部署NSEC3，运算量大。

于是只在签名的子域名集合里做NSEC3运算，标记为OptOut。

这个除了接口兼容性之外，显然接近于白算了，因为其他未签名的域名可能事实存在。

因此，NSEC3 Aggressive 没法在 OptOut 置位的场景下生效。反过来说，在OptOut置位的场景下，NSEC3记录并不能提供qname以外的其他 ENT ( Empty Non-Terminal ) 子域名存在与否的辅助信息。

理想安全场景：NSEC3 + not OptOut, 定期更新 Iterations + salt

相对安全场景：NSEC3 + not OptOut，Iterations + salt 随 ZSK/KSK 一起更新

部分安全场景：NSEC3 + OptOut，Iterations + salt 随 ZSK/KSK 一起更新 

省钱场景：NSEC3 + OptOut，Iterations = 0, empty salt (verisign的选择)

2B场景：NSEC3 + OptOut, Iterations + salt 错误配置消耗大量cpu资源


资料
==========================================================

- `NSEC3PARAM iteration count update <https://www.ietf.org/mail-archive/web/dnsop/current/msg21656.html>`_
- `NSEC3 Iterations <https://tools.ietf.org/html/draft-york-dnsop-deploying-dnssec-crypto-algs-05#section-2.3.1>`_
- `NSEC3 interations max <https://github.com/miekg/dns/issues/611>`_
- `The NSEC3 Resource Record <https://tools.ietf.org/html/rfc5155#page-7>`_
- `The NSEC3PARAM Resource Record <https://tools.ietf.org/html/rfc5155#page-12>`_
- `RFC7129: Authenticated Denial of Existence in the DNS <https://tools.ietf.org/html/rfc7129>`_
- `RFC7129: Authenticated Denial of Existence in the DNS <https://tools.ietf.org/html/rfc7129>`_
- `RFC5155: DNS Security (DNSSEC) Hashed Authenticated Denial of Existence <https://tools.ietf.org/html/rfc5155>`_
- `RFC8198: Aggressive Use of DNSSEC-Validated Cache <https://tools.ietf.org/html/rfc8198>`_
- `DNSSEC: TLD NSEC3 + OptOut <http://www.communitydns.eu/DNSSEC.pdf>`_

