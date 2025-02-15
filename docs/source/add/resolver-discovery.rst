Adaptive DNS Resolver Discovery
==========================================================

https://datatracker.ietf.org/doc/html/draft-pauly-add-resolver-discovery-01

Discovery:
- SVCB RR, DNSSEC
- provision domain (PvD) file from Designated DoH Resolver

Validation:
- a well-known HTTPS URI based on a zone apex
- TLS certificate to confirm of domain name ownership

avoid deploying a DoH server that is only designated by a small number of names.
