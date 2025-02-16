nxdomain black lies
==========================================================

draft-valsorda-dnsop-black-lies	  

对于不存在域名，不是返回NXDOMAIN, 而是返回 NODATA，这样只要给一个NSEC+RRSIG，没有传统的NSEC(3)的zone-walking威胁。
