The ORIGIN HTTP/2 Frame
==========================================================

`RFC8336 The ORIGIN HTTP/2 Frame <https://datatracker.ietf.org/doc/html/rfc8336>`_

一个新头部origin，用于server主动提示client某些域名可以复用当前http2连接（不用发起多个连接）

这个主要帮CDN厂商省钱

http流量重组变得更麻烦了，那啥监控分析的成本也会提高

Secondary Certificate Authentication in HTTP/2
==========================================================

https://tools.ietf.org/html/draft-ietf-httpbis-http2-secondary-certs-06

这个感觉是为了配合上面的ORIGIN省钱搞出来的配套……

提供在HTTP层获取CA的机制，注意这跟之前的TLS握手不在一个层了。死道友不死贫道，跟你死我也一起死的区别。

.. raw::

    Rather than needing to subvert DNS or IP routing in order to use a compromised certificate, a malicious server now only needs a client to connect to _some_ HTTPS site under its control in order to present the compromised certificate.
