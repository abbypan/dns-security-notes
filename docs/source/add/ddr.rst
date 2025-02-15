Discovery of Designated Resolvers (DDR)
==========================================================

`RFC9462  Discovery of Designated Resolvers <https://datatracker.ietf.org/doc/rfc9462/>`_ 

涉及两种Resolver: 提供SVCB信息的原Resolver、SVCB指定的Designated Resolver

已知原Resolver的Address，Discovery: dns://resolver.arpa，查询_dns.resolver.arpa的SVCB
- Authenticated Discovery: Encrypted DNS部署的certificate必须包含双方的IP/Domain 
- Opportunistic Discovery: 如果双方的IP地址相同，且为Private IP，则opportunistically跳过certificate检查

已知原Resolver的Domain Name，Discovery:  查询_dns.example.net的SVCB

resolver.arpa 为 special use domain name (SUDN)，不应cache

Discovery过程缺乏认证，可能MITM。
