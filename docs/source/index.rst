DNS安全笔记
===========

.. note::

   https://github.com/abbypan/dns-security-notes

目录
----

.. toctree::
   :maxdepth: 1
   :caption: 根

   root/root
   root/root-anycast
   root/root-ana

.. toctree::
   :maxdepth: 1
   :caption: 顶级域

   tld/tld



.. toctree::
   :maxdepth: 1
   :caption: 递归

   recur/recur
   recur/public-recur
   recur/forwarding-recur
   recur/open-recur
   recur/recur-opt
   recur/recur-sec
   recur/recur-cache-flush
   recur/recur-improv



.. toctree::
   :maxdepth: 1
   :caption: 权威

   auth/lame
   auth/auth
   auth/glue-req
   auth/latency
   auth/delegation-req
   auth/ns-revalidation


.. toctree::
   :maxdepth: 1
   :caption: RR

   rr/chaos
   rr/ns
   rr/deleg
   rr/svcb
   rr/srv
   rr/apl
   rr/dnssec-rr


.. toctree::
   :maxdepth: 1
   :caption: security

   security/tsig
   security/dnssec
   security/nsec
   security/nsec3-iter
   security/nsec-wildcard
   security/nsec5
   security/nxdomain-nsec
   security/nsec-nxdomain-black-lies
   security/dnscurve
   security/resolverless
   security/hijack

.. toctree::
   :maxdepth: 1
   :caption: Extension

   ext/edns0
   ext/multiple-res
   ext/no-response
   ext/catalog-zone
   ext/attrleaf
   ext/dns-errors


.. toctree::
   :maxdepth: 1
   :caption: DANE

   dane/tlsa
   dane/pmta-pay
   dane/ipseca


.. toctree::
   :maxdepth: 1
   :caption: privacy

   privacy/privacy
   privacy/privacy-ana
   privacy/ecs
   privacy/eil
   privacy/namecoin
   privacy/dnssd-privacy
   privacy/confidential-dns
   privacy/start-tls
   privacy/knell-dns
   privacy/ip-anon

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
   ddos/rrl


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
   app/iot-dns-autoconf


.. toctree::
   :maxdepth: 1
   :caption: Attack

   attack/packet-injection
   attack/dnssec-keytrap
   attack/ns-attack
   attack/ddos
   attack/conf-err
   attack/hijack
   attack/manage


.. toctree::
   :maxdepth: 1
   :caption: STD

   std/deployment
