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

.. toctree::
   :maxdepth: 1
   :caption: 顶级域

   tld/tld



.. toctree::
   :maxdepth: 1
   :caption: 递归

   recur/index
   recur/open_recur
   recur/forwarding_recur


.. toctree::
   :maxdepth: 1
   :caption: 权威

   auth/lame


.. toctree::
   :maxdepth: 1
   :caption: 资源记录

   rr/chaos
   rr/ns
   rr/deleg


.. toctree::
   :maxdepth: 1
   :caption: security

   security/dnssec
   security/nsec
   security/nsec5
   security/dnscurve
   security/resolverless
   security/hijack

.. toctree::
   :maxdepth: 1
   :caption: Extension

   ext/edns0


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
   privacy/dnssd
   privacy/confidential-dns
   privacy/start-tls

.. toctree::
   :maxdepth: 1
   :caption: qos

   qos/resolve-performance

.. toctree::
   :maxdepth: 1
   :caption: Local

   local/split-ikev2


.. toctree::
   :maxdepth: 1
   :caption: DDoS

   ddos/dns-cookies
   ddos/long-ttl


.. toctree::
   :maxdepth: 1
   :caption: Service

   service/httpdns

.. toctree::
   :maxdepth: 1
   :caption: software

   software/dns-software-finger
   software/bind


.. toctree::
   :maxdepth: 1
   :caption: Attack

   attack/packet-injection
   attack/dnssec-keytrap
   attack/ns-misconf
   attack/nxnsattack
