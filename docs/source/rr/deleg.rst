deleg
=========


`DNS and the proposed DELEG record <https://blog.apnic.net/2024/02/08/dns-and-the-proposed-deleg-record/>`_

deleg起作用的前提是配合dnssec使用，否则与无dnssec下的ns glue效果差别不大。

而如果有full resolution path形态的dnssec validation，deleg效用主要在合并查询。

resolver层面的性价比不高。
