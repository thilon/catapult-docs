### 密码学(Cryptography)

NEM使用基于**椭圆曲线加密算法**。底层曲线的选择对于保证安全性和速度非常重要

私匙和公匙
===

私匙(private key)是一个256位随机整数。公匙(public key)是由私匙加密的方式生成。NEM是用`Ed25519 elliptic curve`和`SHA3`Hash算法

