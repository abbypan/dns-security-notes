DNS安全笔记
===========

.. note::

   https://github.com/abbypan/dns-security-notes

目录
----

.. toctree::
   :maxdepth: 1
   :caption: 根

   root/index
   root/anycast
   root/root-ana

.. toctree::
   :maxdepth: 1
   :caption: 顶级域

   tld/tld



.. toctree::
   :maxdepth: 1
   :caption: 递归

   recur/index
   recur/public-recur
   recur/forwarding-recur
   recur/open-recur


.. toctree::
   :maxdepth: 1
   :caption: 权威

   auth/lame


.. toctree::
   :maxdepth: 1
   :caption: RR

   rr/chaos
   rr/ns
   rr/deleg
   rr/svcb
   rr/srv


.. toctree::
   :maxdepth: 1
   :caption: security

   security/dnssec
   security/nsec
   security/nsec3-iter
   security/nsec5
   security/nxdomain-nsec
   security/dnscurve
   security/resolverless
   security/hijack

.. toctree::
   :maxdepth: 1
   :caption: Extension

   ext/edns0
   ext/multiple-res


.. toctree::
   :maxdepth: 1
   :caption: DANE

   dane/tlsa
   dane/pmta-pay
   dane/ipseca


.. toctree::
   :maxdepth: 1
   :caption: privacy

   privacy/ecs
   privacy/eil
   privacy/namecoin
   privacy/dnssd-privacy
   privacy/confidential-dns
   privacy/start-tls
   privacy/knell-dns

.. toctree::
   :maxdepth: 1
   :caption: qos

   qos/resolve-performance
   qos/cache-dns

.. toctree::
   :maxdepth: 1
   :caption: Local

   local/split-ikev2
   local/iot-name-autoconf
   local/mdns


.. toctree::
   :maxdepth: 1
   :caption: DDoS

   ddos/dns-cookies
   ddos/long-ttl
   ddos/disposable-dom


.. toctree::
   :maxdepth: 1
   :caption: ADD

    add/add
    add/ddr
    add/dnr
    add/enterprise-net
    add/iot-byod
    add/resolver-discovery


.. toctree::
   :maxdepth: 1
   :caption: Service

   service/httpdns
   service/doh
   service/dnssd
   service/hybrid-dnssd

.. toctree::
   :maxdepth: 1
   :caption: software

   software/dns-software-finger
   software/bind
   software/pcap


.. toctree::
   :maxdepth: 1
   :caption: app

   app/diameter-s-naptr
   app/origin-http2


.. toctree::
   :maxdepth: 1
   :caption: Attack

   attack/packet-injection
   attack/dnssec-keytrap
   attack/nxnsattack
   attack/ddos
   attack/conf-err
   attack/hijack
   attack/manage


