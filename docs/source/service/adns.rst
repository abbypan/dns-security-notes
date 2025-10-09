Attested DNS 
=================

Transparent Attested DNS for Confidential Computing Services

https://arxiv.org/pdf/2503.14611

新增 dns server 关联的 account 密钥对，dns server 侧基于TEE（例如SGX）向ACME Server发请求，校验后签发/管理证书。

dns server 基于TEE向 dns client 提供 attestation（基于DANE关联），使得dns client确信其身份可靠。
