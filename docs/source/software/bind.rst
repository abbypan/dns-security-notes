bind
#########

资料
==========================================================

- dns server 软件对比：http://en.wikipedia.org/wiki/Comparison_of_DNS_server_software
- bind 的源码、手册等：ftp://ftp.isc.org/isc/
- bind 一些安全配置项：http://www.aitechsolutions.net/dnsservertips.html
- power dns 手册：http://doc.powerdns.com/html/index.html
- BIND 9 DNS Security：http://www.nsa.gov/ia/_files/vtechrep/I733-004R-2010.pdf

版本信息
==========================================================

http://www.isc.org/software/bind/versions

Response Rate Limiting (RRL)
==========================================================

- https://www.isc.org/blogs/isc-adds-ddos-defense-module-to-bind-software/
- https://kb.isc.org/article/AA-01000

BIND 添加了 ddos 防护模块：

主要是Response Rate Limiting (RRL)，每秒种响应同一个源IP的相同查询的最大次数

Debian : 安装bind9，配置允许本地递归查询
==========================================================

apt-get install bind9 dnsutils

编辑/etc/bind/named.conf.options，在

    options{
        ....
    };

内添加

    allow-recursion {
        127.0.0.1;
    }; 

如果提示 rndc: connect failed: 127.0.0.1#953: connection refused  

rndc-confgen > /etc/bind/rndc.conf

测试bind

named -g

重启bind

/etc/init.d/bind9 restart
