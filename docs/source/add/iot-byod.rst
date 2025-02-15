DoT & DoH for IoT & BYOD 
==========================================================

`A Bootstrapping Procedure to Discover and Authenticate DNS-over-TLS and DNS-over-HTTPS Servers for IoT and BYOD Devices <https://datatracker.ietf.org/doc/draft-reddy-add-iot-byod-bootstrap/>`_

先连接到指定网络，例如VPN，或者local network

dnssd 或者 mdns 获取EST Server地址: _est._tcp.example.com / _est._tcp.local

rfc7030: Enrollment over Secure Transport (EST)，PAKE协议认证EST server后，下载并信任DNS Service EE Certificate
