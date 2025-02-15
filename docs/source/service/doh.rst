DOH
==========================================================

`DNS Queries over HTTPS <https://datatracker.ietf.org/doc/html/rfc8484>`_

端到端安全。防DNS阻断、污染。

新增 application/dns-udpwireformat，POST请求的body提交的是原始查询包；GET请求提交的是base64url(RFC4648)

这个比较适合android之类客户端到递归的场景。

押1个桔子，针对递归服务器的IP blocking要上升。


