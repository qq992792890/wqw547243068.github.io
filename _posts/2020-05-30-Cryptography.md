---
layout: post
title:  "密码学-Cryptography"
date:   2020-05-30 00:13:00
categories: 密码学
tags: 密码学 同态加密
excerpt: 密码学知识，常见的加密、解码算法，对称密钥、非对称密钥和Hash散列
author: 鹤啸九天
mathjax: true
---

* content
{:toc}

# 密码学

## 历史

- 古代密码：凯撒密码，20多个罗马字母简单替换，一直用到二战（日本）
    - `凯撒密码`：凯撒密码是通过将明文中所使用的字母表按照一定的字数“平移”来进行加密和解密的。
        - ![](https://upload-images.jianshu.io/upload_images/2990730-495421d41bf4b8ab.png)
    - `简单替换密码`：简单替换密码是将明文中所使用的的字母表替换为另一套字母表的密码。
    - `Enigma`：Enigma是第二次世界大战中德国使用的一种密码机，它是一种由键盘、齿轮、电池、和灯泡所组成的机器，通过这一台机器就可以完成加密和解密两种操作。
        - 现代计算机之父阿兰•图灵曾是破译德国密码机团队的一员。图灵在1940年研制出了用于破译Enigma的机器。
- 艾伦·麦席森·图灵在二战期间主要负责破译德国人的密码系统Enigma，破解密码需要大量的计算，图灵深知工欲善其事必先利其器的道理，于是一台叫作CO-LOSSUS的计算机在1943年被研制出来，后来这种电子计算机总共生产了10台，他们出色完成了密码破译工作。
- 图灵机的诞生确实加快了二战的结束
- 图灵机也就是战胜了对称加密算法。
- 电影《模仿游戏》，影片改编自安德鲁·霍奇斯编著的传记《艾伦·图灵传》

![](https://img-blog.csdn.net/2018061821395310)


## 分类

- 加密算法可以分成三类：`对称加密`算法，`非对称加密`算法和`Hash`算法。
- 注意：
    - Base64编码只是一种编码格式并不是加密算法，它可用于在HTTP环境下传递较长的标识信息。
- 加密算法的选择
    - 对称加密算法不能实现签名，因此签名只能非对称算法。
    - 验证文件或字符一致性用hash算法
    - 数据量大用对称加密算法、小则可以用非对称加密
    - 还可以非对称与对称集成，参考https请求原理
    - RSA建议采用1024位的数字，ECC建议采用160位，AES采用128为即可

### 对称加密

- 1976年以前，所有的加密方法都是同一种模式即对称加密，特点是加密和解密使用相同的密钥
    - 用相同的密钥进行加密和解密的技术，用于确保消息的机密性
    - ![](https://upload-images.jianshu.io/upload_images/1546230-27a7ad9c072c0b9a.png)
![](https://img-blog.csdn.net/20180618214056767)

- 优点：对称加密算法的优点是算法公开、计算量小、加密速度快、加密效率高。
- 缺点：在数据传送前，发送方和接收方必须商定好秘钥，然后双方保存好秘钥。如果一方的秘钥被泄露，那么加密信息也就不安全了
- 使用场景：本地数据加密、https通信、网络传输等
- 常见算法：AES、DES、3DES、DESX、Blowfish、IDEA、RC4、RC5、RC6
    - 目前主要使用的是AES，因为它安全、快速、而且能够在各种平台上工作。尽管对称密码能够确保消息的机密性，但需要解决将解密秘钥配送给接收者的密钥配送问题。
    - DES和AES都属于`分组密码`，它们只能加密固定长度的明文。如果需要加密任意长度的明文，就需要对分组密码进行迭代，而分组密码的迭代方法就称为分组密码的模式。

#### 一次性密码本

- 只要通过暴力破解法对密钥空间进行遍历，无论什么密文总有一天也都能够被破译。然而一次性密码本却是一个例外，即便使用暴力破解法遍历整个密钥空间，一次性密码本也绝对无法被破译。
- 一次性密码本是一种非常简单的密码，它的原理是“将明文与一串随机的比特序列进行XOR(异或)运算”。
- 在一次性密码本中，由于我们无法判断得到的是不是正确的明文，因此一次性密码本是无法破译的。
- 由于一次性密码本存在配送、保存、重用、同步等方面的问题，所以几乎没有人应用一次性密码本，因为它是一种非常不实用的密码。

#### DES

- DES（Data Encryption Standard）是1977年美国联邦信息处理标准中所采用的一种对称码。
- DES是一种将64比特的明文加密成64比特的密文的对称密码算法，它的密钥长度是56比特。尽管从规格上来说，DES的密钥长度是64比特，但由于每隔7比特会设置一个用于错误检查的比特，因此实质上其实密钥长度是56比特。
- 由于DES的密文可以在短时间内被破译，因此除了用它来解密以前的密文以外，现在我们不应该使用DES了。

#### 三重DES

- 三重DES是为了增加DES的强度，将DES重复3次所得到的一种密码算法，也称为TDEA,通常缩写为3DES。
- 尽管三重DES目前还被银行等机构使用，但其处理速度不高，除了特别重视向下兼容性的情况以外，很少被用于新的用途。

#### AES

 AES（Advanced Encryption Standard）是取代其前任标准（DES）而成为新标准的一种对称密码算法（Rijndael）。
- Rijndael是由比利时密码学家Joan Daemen和Vincent Rijmen设计的分组密码算法，于2000年被选为新一代的标准密码算法——AES。
- Rijndael的分组长度和密钥长度可以分别以32比特为单位在128比特到256比特的范围内进行选择。不过在AES的规格中，分组长度固定为128比特，密钥长度只有128、192、和256比特三种。



### 非对称加密

![](https://img-blog.csdn.net/20180618214208603)

- 1976年，两位美国计算机学家Whitfield Diffie 和 Martin Hellman，提出了一种崭新构思，可以在不直接传递密钥的情况下，完成解密。这被称为“Diffie-Hellman密钥交换算法”。这个算法启发了其他科学家。人们认识到，加密和解密可以使用不同的规则，只要这两种规则之间存在某种对应关系即可，这样就避免了直接传递密钥。这种新的加密模式被称为”非对称加密算法”。
    - 公钥密码（非对称密码）中，密钥分为加密密钥和解密密钥两种。发送者用加密密钥对消息进行加密，接收者用解密密钥对密文进行解密。
    - ![](https://upload-images.jianshu.io/upload_images/1546230-553d0cc72e21488a.png)
![](https://img-blog.csdn.net/20180704143158193)

- 优点：非对称加密与对称加密相比其安全性更好
- 缺点：加密和解密花费时间长、速度慢，只适合对少量数据进行加密。
- 使用场景：https会话前期、CA数字证书、信息加密、登录认证等
- 常见算法：RSA、ECC（移动设备用）、Diffie-Hellman、El Gamal、DSA（数字签名用）

#### RSA

- RSA是一种公钥密码算法，它的名字是由它的三位开发者，即Ron Rivest、Adi Shamir和Leonard Adleman的姓氏的首字母组成的(Rivest-Shamir-Adleman)。
    - RSA利用了质因数分解的困难度
    - EIGamal方式则利用了mod N 下求离散对数的困难度
    - Rabin方式是由M.O.Rabin设计的公钥算法，利用了mod N下求平方根的困难度。
- 加密：求“E次方的 mod N”
- 解密：求“D次方的 mod N”

#### 椭圆曲线密码

- 椭圆曲线密码（Elliptic Curve Cryptography，ECC）是最近备受关注的一种公钥密码算法。它的特点是所需的密钥长度比RSA短。

### Hash

- Hash算法特别的地方在于它是一种单向算法，用户可以通过Hash算法对目标信息生成一段特定长度的唯一的Hash值，却不能通过这个Hash值重新获得目标信息。因此Hash算法常用在不可还原的密码存储、信息完整性校验等。

![](https://img-blog.csdn.net/20180618214402978)

- 优点：不可逆、易计算、特征化
- 缺点：可能存在散列冲突
- 使用场景：文件或字符串一致性校验、数字签名、鉴权协议
- 常见算法：MD2、MD4、MD5、HAVAL、SHA、SHA-1、HMAC、HMAC-MD5、HMAC-SHA1

#### 单向散列函数

- 单向散列函数有一个输入和一个输出，其中输入称为消息（message），输出称为散列值（hash code）。单向散列函数可以根据消息的内容计算出散列值，而散列值就可以被用来检查消息的完整性。
    - ![](https://upload-images.jianshu.io/upload_images/1546230-7d2097afb31c36fd.png)
- 散列值的长度和消息的长度无关。无论消息是1比特，还是100MB，甚至是100GB，单向散列函数都会计算出固定长度的散列值。
- 以SHA-256单向散列函数为例，它所计算出的散列值的长度永远是256比特（32字节）。
- 为了能够确认完整性，消息中哪怕只有1比特的改变，也会产生不同的散列值。
- 单向散列函数输出的散列值也称为消息摘要（message digest）或者指纹（fingerprint）

#### MD4、MD5

- MD（Messge Digest）4是由Rivest于1990年设计的单向散列函数，能够产生128比特的散列值。现在它已经不安全了。
- MD（Messge Digest）5是由Rivest于1991年设计的单向散列函数，能够产生128比特的散列值。MD5的强抗碰撞性已经被攻破。也就是说，现在已经能够产生具备相同散列值的两条不同的消息，因此它也不安全了。

#### SHA-1、SHA-256、SHA-384、SHA512

- SHA-1是由NIST（美国国家标准技术研究所）设计的一种能够产生160比特的散列值的单向散列函数。现在已不推荐使用。
- SHA-256、SHA-384、SHA512都是由NIST设计的单向散列函数，它们的散列值长度分别为256比特、384比特、和512比特。这些单向散列函数合起来统称SHA-2。
- SHA-1的强抗碰撞性已于2005年被攻破，不过，SHA-2还尚未被攻破。

#### RIPEMD-160

- RIPEMD-160是于1996年由Hans Dobbertin、Antoon Bosselaers和Bart Preneel设计的一种能够产生160比特的散列值的单向散列函数。RIPEMD-160是欧盟RIPE项目所设计的RIPEMD单向散列函数的修订版。
- RIPEMD的强抗碰撞性已经于2004年被攻破，但RIPEMD-160还尚未被攻破。比特币中使用的就是RIPEMD-160。

#### SHA-3

- SHA-3（Secure Hash Algorithm-3）是一种作为新标准发布的单向散列函数算法，用来替代在理论上已被找出攻击方法的SHA-1算法。
- SHA-3的标准是Keccak算法。

#### Keccak

- Keccak是一种被选定为SHA-3标准的单向散列函数算法。
- Keccak可以生成任意长度的散列值，但为了配合SHA-2的散列值长度，SHA-3标准中共规定了SHA3-224、SHA3-256、SHA3-384、SHA3-512这4种版本。


### 消息认证码

- 消息认证码（Message Authentication Code）是一种确认完整性并进行认证的技术，简称为MAC。
- 消息认证指的是“消息来自正确的发送者”这一性质。
- 消息认证码的输入包括任意长度的消息和一个发送者与接受者之间共享的密钥，它可以输出固定长度的数据，这个数据成为MAC值。
- 要计算MAC必须持有共享密钥，没有共享密钥的人就无法计算MAC值，消息认证码正是利用这一性质来完成认证的。此外，和单向散列函数的散列值一样，哪怕消息中发生1比特的变化，MAC值也会产生变化，消息认证码正是利用这一性质来确认完整性的。
- 消息认证码可以说是一种与密钥相关联的单向散列函数。
- 消息认证码可以使用单向散列函数和对称密码等技术来实现。
- 消息认证与单向散列的对比
    - ![](https://upload-images.jianshu.io/upload_images/1546230-761524bbf86e85ce.png)
- 消息认证使用步骤
    - ![](https://upload-images.jianshu.io/upload_images/1546230-1699375397c0eb10.png)

#### HMAC

- HMAC是一种使用单向散列函数来构造消息认证码的方法，其中HMAC的H就是Hash的意思。
- 消息认证码也不能解决所有的问题，例如“对第三方证明”，和“防止否认”，这两个问题就无法通过消息认证码来解决。


### 数字签名

- 消息认证码之所以无法防止否认，是因为消息认证码需要在发送者和接收者两者之间共享一个密钥。
- 数字签名是一种能够对第三方进行消息认证，并能够防止通信对象作出否认的认证技术。
- 数字签名中也同样会使用公钥和私钥组成的密钥对，不过这两个密钥的用法和公钥密码是相反的，即用私钥加密相当于生成签名，而用公钥解密则相当于验证签名。

### 证书

- 公钥证书（Public-Key Certificate，PKC）其实和驾照很相似，里面记有姓名、组织、邮箱、地址等个人信息，以及属于此人的公钥，并由认证机构（Certification Authority，CA）施加数字签名。只要看到公钥证书，我们就可以知道认证机构认定该公钥的确属于此人。公钥证书也简称为证书。
- 认证机构就是能够认定“公钥确实属于此人”并能够生成数字签名的个人或者组织。
- ![](https://upload-images.jianshu.io/upload_images/1546230-d4b0b7bda05e8610.png)


## 典型密码

### RSA密码

- 主要概念
    - 欧拉函数
    - 欧拉定理
    - 费马小定理
- RSA密码诞生

![](https://upload-images.jianshu.io/upload_images/2990730-1e446769f7fd0fa2.png)

## 资料

- [常见加密算法简介](https://blog.csdn.net/u014044812/article/details/80723009)
- [RSA原理探究](https://www.jianshu.com/p/ca659dbc6f46)
- [RSA算法基础详解](https://www.cnblogs.com/hykun/p/RSA.html)
- [密码学入门总结](https://www.jianshu.com/p/a8070920810d)
- [密码技术那些事儿](https://www.jianshu.com/p/8d7c8f59ea21)
- [密码学 2015版（斯坦福大学）](https://www.bilibili.com/video/BV1wt411V79d)

<iframe src="//player.bilibili.com/player.html?aid=59014949&bvid=BV1wt411V79d&cid=102869806&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="600" width="100%"> </iframe>

- [MIT密码学 MIT 6.875, Cryptography Sp 2018](https://www.bilibili.com/video/BV1qt411L74p)
<iframe src="//player.bilibili.com/player.html?aid=58961353&bvid=BV1qt411L74p&cid=102774363&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="600" width="100%"> </iframe>

- [《模仿游戏》人工智能之父阿兰图灵的一生](https://www.bilibili.com/video/BV1fW411F7AM)
<iframe src="//player.bilibili.com/player.html?aid=25026545&bvid=BV1fW411F7AM&cid=42296927&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="600" width="100%"> </iframe>

# 结束


