NSEC5
#######

`NSEC5: Provably Preventing DNSSEC Zone Enumeration <http://www.cs.bu.edu/~goldbe/papers/nsec5.html>`_

NSEC x1<x<x2 

NSEC3 把x换成h(x) 

NSEC5 把h(x)再换成h2(RSA-1(h1(x)))

粽子又包了一层，而且夹了一层RSA验证。

所以为了防zone遍历，你知道人家有多努力嘛。

此外，递归又更好打了。
