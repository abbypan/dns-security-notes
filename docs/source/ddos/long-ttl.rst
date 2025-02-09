long ttl
#############

https://www.ietf.org/proceedings/66/slides/dnsop-3.pdf

Improving DNS Service Availability by Using Long TTL Values, V. Pappas, B. Zhang, E. Osterweil, D. Massey, L. Zhang, Internet Draft, draft-pappas-dnsop-long-ttl-03, Oct. 2006

NS经常设置为12小时，或更短一点

在DNS迭代时用到的NS可以设长一点，到达权威的NS可以设短一点

可以让本地NS与A/AAAA的TTL保持一致

也可以在修改之前，先把旧的TTL搞短，新记录迅速扩散之后，再把TTL调长
