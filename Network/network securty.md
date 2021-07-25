

# lesson 2

## Authentication

0 - 14 : problem



##  MAC

Message Authentication Code

m： 报文，s：共享秘密；H(m+s)：报文鉴别码MAC。发送拓展报文 H(m+s)

- CBC-MAC

- MD5

- SHA-1


## Digital Signature: MAC+Encription

私钥签署

## Key Distribution

- Diffie-Hellman Key Exchange

- Trusted certification authority (CA)

- Certificate for public key

应用：

1.加密

2.真实性：私钥签名过 摘要 $$K^- (H(m)\ )$$

3.三个钥匙，Alice的私钥签署 --> 生成一次性对称密钥-->Bob的公钥确保只有Bob能收。