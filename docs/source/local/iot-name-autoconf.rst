DNS Name Autoconfiguration for Internet of Things Devices
==============================================================

`DNS Name Autoconfiguration for Internet of Things Devices <https://tools.ietf.org/html/draft-jeong-ipwave-iot-dns-autoconf-01>`_

https://datatracker.ietf.org/meeting/94/materials/slides-94-6man-1/

https://www.ietf.org/proceedings/91/slides/slides-91-dnssd-6.pdf

https://www.ietf.org/proceedings/91/slides/slides-91-homenet-4.pdf

想省掉物联网设备初始化DNS配置的过程，直接自动注册名称

.. raw::

    unique_id + vendor_device_model + device_category + domain_suffix (e.g., .home) 

在 Node Information Protocol 及 DNS Dynamic Update 的基础上实现

这个号称跟mdns场景不同，主要因为mdns是局域网场景，而dnsna可以支持公网IPv6地址

个人觉得不同点主要在于，mdns是在节点上同时实现了轻量级的server/client收发广播包，而dnsna是通过ipv6 zero-config先找到本地局域网DNS然后进行自动化注册登记

名称的自动生成方式其实也可以参考oid/ons/handle等协议

远程控制家庭物联网设备，必然通过网关。因此，局域网地址/ipv6公网地址在该场景下，区别不会非常大（同样都要开放监听端口接收命令）

