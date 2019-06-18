---
title: Application Layer
date: 2019-05-24 14:17:03
categories:
- [InterProtocolSuite]
- [OSI Model]
tags:
- osi
- protocol
- protocol suite
- internet
- compuer network
---

# What is Applicaton Layer？

应用层(Application Layer) 是一个抽象层，它指定通信网络中主机使用的共享 通信协议(communications protocols) 和接口方法。应用层抽象用于计算机网络的两种标准模型：Internet Protocol Suite(TCP/IP) 和 OSI Model。虽然两个模型对于各自的最高级别层使用相同的术语，但详细的定义和目的是不同的。

在 TCP/IP 协议中，应用层包含用于跨 Internet Protocols(IP) 计算机网络进行进程间通信的通信协议和接口方法。应用层仅标准化通信，并且依赖底层传输层协议来建立 主机到主机(host-to-host) 的数据传输通道，并在 cilent-server 或 peer-to-peer networking model 中管理数据交换。虽然 TCP/IP 应用层没有描述应用程序在通信时必须考虑的特定规则或数据格式，但是原始规范[(RFC 1123)](https://tools.ietf.org/html/rfc1123)依赖并推荐了应用程序设计的健壮性原则。

> RFC: 请求意见稿（英语：Request For Comments，缩写：RFC）是由互联网工程任务组（IETF）发布的一系列备忘录。文件收集了有关互联网相关信息，以及UNIX和互联网社群的软件文件，以编号排定。当前RFC文件是由互联网协会（ISOC）赞助发行。  
> RFC始于1969年，由当时就读加州大学洛杉矶分校（UCLA）的斯蒂芬·克罗克（Stephen D. Crocker）用来记录有关ARPANET开发的非正式文档，他是第一份RFC文档的撰写者。最终演变为用来记录互联网规范、协议、过程等的标准文件。基本的互联网通信协议都有在RFC文件内详细说明。RFC文件还额外加入许多的论题在标准内，例如对于互联网新开发的协议及发展中所有的记录。

在 OSI Model 中，应用层的定义范围更窄。OSI Model 将应用程序层定义为负责向用户显示接收到的信息的用户界面。相反，Internet Protocol Suite 并不关心这些细节。OSI 还显式地区分了应用程序层之下的其他功能，但在传输层之上还有两层: Seesion Layer(会话层) 和 Persentation Layer(表示层)。OSI在这些层上指定了严格的功能模块化分离，并为每一层提供协议实现。

## Application Layer Protocols Introduces

(OSI Model 下的 会话层)Internet Protocol Suite 中的应用层 [IETF](https://en.wikipedia.org/wiki/Internet_Engineering_Task_Force)定义文档是RFC 1123.它提供了一组初始协议，涵盖了早期Internet功能的主要方面。

> IETF： 互联网工程任务小组（英语：Internet Engineering Task Force，缩写：IETF）负责互联网标准的开发和推动。  
> 它的组织形式主要是大量负责特定议题的工作组，每个都有一个指定主席（或者若干副主席）。工作组再用主题组织为领域（area）；每个领域都有一个领域指导（area director，AD），大多数领域还有两个副AD；AD任命工作组主席。AD和IETF主席构成Internet Engineering Steering Group（IESG），负责IETF的整体运作。

+ Remote login to hosts(远程登录主机)： [Telnet](https://en.wikipedia.org/wiki/Telnet),[Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)(SSH)
+ File transfer(文件传输)： [File Transfer Potocol](https://en.wikipedia.org/wiki/File_Transfer_Protocol)(FTP)，[Trivial File Transfer Protocol](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol)(TFTP)
+ Eletronic mail transport(电子邮件传输)： [Simple Mail Transfer Protocol](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol)(SMTP)
+ Networking support(网络支持)： [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)(DNS)
+ Host initialization(主机初始化)： [BOOTP](https://en.wikipedia.org/wiki/Bootstrap_Protocol),[Dynamic Host Configuration Protocol](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)(DHCP)
+ Remote host management(远程主机管理)： [Simple Network Management Protocol](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol)（SNMP），[Common Management Information over TCP](https://en.wikipedia.org/wiki/Common_Management_Information_Protocol)（CMOT）

### Design patterns for application layer protocols

在通信协议的设计和实现中经常会出现重复出现的问题，这些问题可以通过几种不同模式语言的模式来解决：

+ 应用级通信协议的模式语言([CommDP](http://commdp.serv.usu.edu/))
+ 服务设计模式(R. Daigneau, Service Design Patterns: Fundamental Design Solutions for SOAP/WSDL and RESTful Web Services, 1 edition. Upper Saddle River, NJ: Addison-Wesley Professional, 2011.)
+ 企业应用程序架构模式(M. Fowler, Patterns of Enterprise Application Architecture, 1 edition. Boston: Addison-Wesley Professional, 2002.)
+ 模式导向软件架构：分布式计算的模式语言。(F. Buschmann, K. Henney, and D. C. Schmidt, Pattern-Oriented Software Architecture Volume 4: A Pattern Language for Distributed Computing, Volume 4 edition. Chichester England; New York: Wiley, 2007.)

这些模式语言中的第一种侧重于协议的设计，而不是它们的实现。另一些则涉及这两个领域或只是后者的问题。

## Other protocol examples

+ [9P](https://en.wikipedia.org/wiki/9P_(protocol)), [Plan 9 from Bell Labs(贝尔实验室九号项目)](https://en.wikipedia.org/wiki/Plan_9_from_Bell_Labs) - distributed file system protocol(分布式文件系统协议)
+ AFP, [Apple Filing Protocol(苹果归档协议)](https://en.wikipedia.org/wiki/Apple_Filing_Protocol)
+ APPC, [Advanced Program-to-Program Communication](https://en.wikipedia.org/wiki/IBM_Advanced_Program-to-Program_Communication)
+ **AMQP， [Advanced Message Queuing Protocol(高级消息队列协议)](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol)**
+ [Atom Publishing Protocol(Atom出版协定,用于新增及修改网络资源，基于HTTP的协议。)](https://en.wikipedia.org/wiki/Atom_(Web_standard))
+ [BEEP](https://en.wikipedia.org/wiki/BEEP), Block Extensible Exchange Protocol
+ **[Bitcoin(比特币)](https://en.wikipedia.org/wiki/Bitcoin)**
+ **[BitTorrent(简称BT，俗称比特洪流、BT下载)](https://en.wikipedia.org/wiki/BitTorrent)**
+ CFDP, [Coherent File Distribution Protocol](https://en.wikipedia.org/wiki/Coherent_file_distribution_protocol)
+ CoAP, [Constrained Application Protocol(约束应用程序协议, 该协议专为机器对机器（M2M）应用而设计，如智能能源和楼宇自动化。)](https://en.wikipedia.org/wiki/Constrained_Application_Protocol), [M2M](https://en.wikipedia.org/wiki/Machine_to_machine)
+ DDS, [Data Distribution Service](https://en.wikipedia.org/wiki/Data_Distribution_Service)
+ [DeviceNet](https://zh.wikipedia.org/wiki/DeviceNet)(DeviceNet使用控制器局域网络（CAN）为其底层的通讯协定，其应用层有针对不同设备所定义的行规（profile）。主要的应用包括资讯交换、安全设备及大型控制系统。)
+ ENRP, [Endpoint Handlespace Redundancy Protocol](https://en.wikipedia.org/wiki/Endpoint_Handlespace_Redundancy_Protocol)
+ [FastTrack - peer to peer protocol, file sharing network](https://en.wikipedia.org/wiki/FastTrack)(KaZaa, Grokster, iMesh)
+ [Finger](https://en.wikipedia.org/wiki/Finger_protocol), User Information Protocol
+ [Freenet](https://en.wikipedia.org/wiki/Freenet), Peer to Peer Platform
+ [FTAM](https://en.wikipedia.org/wiki/FTAM), File Transfer Access and Management
+ Gopher, [Gopher protoco](https://en.wikipedia.org/wiki/Gopher_(protocol))(分布型的文件搜集获取网络协议)
+ HL7, [Health Level Seven](https://en.wikipedia.org/wiki/Health_Level_7)(卫生信息交换标准)
+ **HTTP, [HyperText Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)(HTTP是万维网的数据通信的基础)**
+ [H.323](https://en.wikipedia.org/wiki/H.323), Packet-Based Multimedia Communications System
+ [IMAP](https://en.wikipedia.org/wiki/Internet_Message_Access_Protocol), Internet Message Access Protocol，用来从本地邮件客户端（如Microsoft Outlook、Outlook Express、Foxmail、Mozilla Thunderbird）访问远程服务器上的邮件。
+ IRCP, [Internet Relay Chat Protocol](https://en.wikipedia.org/wiki/Internet_Relay_Chat), 主要用于群体聊天，但同样也可以用于个人对个人的聊天。IRC使用的服务器端口有6667（明文传输，如irc://irc.freenode.net）、6697（SSL加密传输，如ircs://irc.freenode.net:6697）等。
+ IPFS, [InterPlanetary File System](https://en.wikipedia.org/wiki/InterPlanetary_File_System), 旨在创建持久且分布式存储和共享文件的网络传输协议。它是一种内容可寻址的对等超媒体分发协议。在IPFS网络中的节点将构成一个分布式文件系统。它是一个开放源代码项目，自2014年开始由Protocol Labs在开源社区的帮助下发展。
+ LDAP, [Lightweight Directory Access Protocol](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol), 通过IP协议提供访问控制和维护分布式信息的目录信息。一个常用用途是单点登录，用户可以在多个服务中使用同一个密码，通常用于公司内部网站的登录中（这样他们可以在公司计算机上登录一次，便可以自动在公司内部网上登录）。
+ LPD, [Line Printer Daemon Protocol](https://en.wikipedia.org/wiki/Line_Printer_Daemon_protocol), 一个网络打印协议提交打印作业到远程打印机
+ [MIME(S-MINE)](https://en.wikipedia.org/wiki/MIME), Multipurpose Internet Mail Extensions and Secure MIME (多用途互联网邮件扩展)
+ [Modbus](https://en.wikipedia.org/wiki/Modbus), 一种串行通信协议，是Modicon公司（现在的施耐德电气 Schneider Electric）于1979年为使用可编程逻辑控制器（PLC）通信而发表。Modbus已经成为工业领域通信协议的业界标准（De facto），并且现在是工业电子设备之间常用的连接方式。
+ [MQTT](https://en.wikipedia.org/wiki/MQTT) Protocol, MQTT消息队列遥测传输(Message Queuing Telemetry Transport)是ISO 标准(ISO/IEC PRF 20922)下基于发布/订阅范式的消息协议。它工作在 TCP/IP协议族上，是为硬件性能低下的远程设备以及网络状况糟糕的情况下而设计的发布/订阅型消息协议，为此，它需要一个消息中间件。
+ [Netconf](https://en.wikipedia.org/wiki/NETCONF), 网络配置协议（NETCONF）是一种网络管理由开发和标准化协议IETF。它是在NETCONF工作组中开发的，并于2006年12月作为RFC 4741发布，后来在2011年6月进行了修订，并作为RFC 6241发布。NETCONF协议​​规范是Internet标准跟踪文档。
+ NFS, [Network File System](https://en.wikipedia.org/wiki/Network_File_System), 网络文件系统（英语：Network File System，缩写作 NFS）是一种分布式文件系统协议，最初由Sun Microsystems公司开发，并于1984年发布。其功能旨在允许客户端主机可以像访问本地存储一样通过网络访问服务器端文件。
+ NIS, [Network Information Service](https://en.wikipedia.org/wiki/Network_Information_Service), 网络信息服务简称 NIS（Network Information Service），时又译为网络数据服务协议，亦即一般简称之“黄页”YP（Yellow Pages），最早由昇阳公司开发出来，为一套用来管理计算机网络中所有与计算机系统管理相关之配置文件，如用户账号、密码、主机名称或组群等的主从式目录服务协议。
+ [...](https://en.wikipedia.org/wiki/Application_layer)

# Application Layer Protocols

## TLS/SSL

传输层安全性协议（Transport Layer Security，TLS） 及其前身安全套接层（Secure Sockets Layer，SSL）是一种加密安全协议，旨在确保计算机网络提供通信安全性。主要目标是提供数据完整性和通信隐私。SSL协议是为此目的而设计的第一个协议，TLS是其后续协议。SSL现在被认为是过时且不安全的（甚至是最新版本），IETF将SSL进行标准化，1999年公布第一版TLS标准文件。随后又公布RFC 5246 （2008年8月）与 RFC 6176 （2011年3月）。在浏览器、电子邮件、即时通信、VoIP、网络传真等应用程序中，广泛支持这个协议。主要的网站，如Google、Facebook等也以这个协议来创建安全连线，发送数据。当前已成为互联网上保密通信的工业标准。

SSL协议最早由Netscape于1994年推出。互联网正在发展，并且需要Web浏览器和各种TCP协议的传输安全性。SSL版本1.0从未发布，因为它存在严重的安全漏洞。SSL的第一个正式版本2.0版本于1995年推出.SSL协议的最终版本SSL 3.0于1996年11月发布。

2011年，互联网工程任务组（IETF）宣布弃用SSL 2.0版。IETF建议完全放弃SSL v2，因为根据他们发布的文档（RFC 6176），该协议有几个主要缺陷。这些包括使用MD5进行消息身份验证，缺乏对握手的保护，使用相同的密钥进行消息完整性和加密，以及轻松的会话终止。2015年6月，IETF还宣布弃用SSL 3.0。正如IETF发布的文件（RFC 7568），任何TLS版本都比所有版本的SSL更安全。SSL也不能使用TLS协议的功能，例如 Authenticated Encryption with Additional Data（AEAD），Elliptic Curve Diffie-Hellman（ECDH） 和 Elliptic Curve Digital Signature Algorithm（ECDSA），stateless session tickets，a datagram mode of operation（DTLS）和 application-layer protocol negotiation。

输层安全性（TLS）协议于1999年首次引入，作为SSL v3的升级。TLS 1.0 RFC文档（RFC 2246）文档指出TLS 1.0和SSL 3.0之间的差异并不显着，但它们足以排除互操作性。TLS 1.1（RFC 4346）是对2006年4月发布的TLS 1.0的一个小更新。此版本中的一些差异包括对 Cipher Block Chaining（CBC）攻击的保护。TLS 1.2（RFC 5246）于2008年8月发布。更改包括添加了 cipher-suite-specified psedorandom functions （PRFs），AES cipher suite，删除了 IDEA 和 DES cipher suiter 以及 其他一些增强功能。

当前版本的TLS，TLS 1.3于2018年8月发布（RFC 8446）。IETF花费了10年时间和28个草稿才能完成。这一次，协议经历了一些重大变化，重点是简单性。删除了一些不安全的技术，包括SHA-1，MD5，RC4，DES 和 3DES。简化了协议以获得更好的性能：握手现在只需要一次往返（在某些情况下甚至为零）。其他变化包括加密SNI信息以获得更好的隐私和新的签名标准（RSA-PSS）。所有现代浏览器都支持 TLS v1.3。

Web浏览器通常使用 SSL 和 TLS 来保护 Web应用程序 和 Web服务器 之间的连接。许多其他基于TCP的协议也使用 TLS/SSL，包括电子邮件（SMTP/POP3），即时消息（XMPP），FTP，VoIP，VPN等。通常，当一个服务如果使用 TLS/SSL ,就会把安全连接字母 S 被附加到协议名称后面，例如，HTTP S，SMTP S，FTP S，SIP S。在大多数情况下，SSL/TLS 实现基于OpenSSL库。

SSL 和 TLS 是使用许多 [不同加密算法](https://www.acunetix.com/blog/articles/tls-ssl-cipher-hardening/) 的框架，例如 RSA 和各种 Diffie-Hellman 算法。双方协商在初始通信期间使用哪种算法。最新的TLS版本（TLS 1.3）在IETF（Internet工程任务组）文档RFC 8446中指定，最新的SSL版本（SSL 3.0）在IETF文档RFC 6101中指定。

TLS协议主要旨在提供两个或更多通信计算机应用程序之间的隐私和数据完整性。当通过TLS保护时，客户端（例如，Web浏览器）和服务器（例如，wikipedia.org）之间的连接应具有以下一个或多个属性：

+ 连接是私有的（或安全的），因为 symmetric cryptography(对称加密) 用于加密传输的数据。键是 symmetric cryptography 针对每个连接唯一生成的，并根据 share secret 在开始协商会话（见 TLS 握手）。服务器和客户端在传输数据的第一个字节之前要协商使用的加密算法和加密密钥的详细信息（参见 Algorithm ）。share secret 的协商是安全的（窃听者无法获得协商的秘密,并且即使是将自己置于连接中间的攻击者也无法获得)且可靠的（攻击者无法在未经检测到的情况下修改协商期间的通信）。
+ 可以使用公钥加密来验证通信方的身份。该认证可以是可选的，但通常需要至少一方（通常是服务器）。
+ 连接是可靠的，因为每个传输的消息都包括使用消息验证码进行的消息完整性检查，以防止在传输过程中出现未检测到丢失或更改数据。

除了上述属性之外，详细配置 TLS 还可以提供其他与隐私相关的属性，例如 forward secrecy ，确保未来任何泄露的加密密钥都不能用于解密过去记录的任何TLS通信。

SSL包含记录层（Record Layer）和传输层，记录层协议确定传输层数据的封装格式。传输层安全协议使用X.509认证，之后利用非对称加密算法来对通信方做身份认证，之后交换对称密钥作为会谈密钥（Session key）。这个会谈密钥是用来将通信两方交换的数据做加密，保证两个应用间通信的保密性和可靠性，使客户与服务器应用之间的通信不被攻击者窃听。

TLS协议包括：TLS record 和 TLS handshake protocols。


### Description

TLS/SSL 协议允许加密两个介质（客户端 - 服务器）之间的连接。加密可以确保没有第三方能够读取数据或篡改数据。未加密的通信可能会暴露敏感数据，如用户名，密码，信用卡号等。如果我们使用未加密的连接并且第三方拦截我们与服务器的连接，他们可以看到以纯文本形式交换的所有信息。例如，如果我们访问没有SSL的网站管理面板，并且攻击者正在嗅探本地网络流量，他们会看到以下信息。

![gcheap](/img/TSL-SSL/image32.png)

我们用于在我们网站上进行身份验证的cookie以纯文本形式发送，任何拦截连接的人都可以看到它。攻击者可以使用此信息登录我们的网站管理面板。从那时起，攻击者的选择范围急剧扩大。但是，如果我们使用 TLS/SSL 访问网站，那么嗅探流量的攻击者会看到一些完全不同的东西。

![gcheap](/img/TSL-SSL/image04-1.png)

这种情况下，该信息对攻击者无用。

TLS/SSL 协议使用公钥加密。除加密外，此技术还用于验证通信方。这意味着，一方或双方确切地知道他们正在与谁沟通。这对于在线交易等应用程序至关重要，因为必须确保将资金转移给他们声称的人或公司。

建立安全连接后，服务器会将其 TSL/SSL 证书发送给客户端。然后，客户端针对可信证书颁发机构检查证书，验证服务器的身份。这样的证书不能被伪造，因此客户可能百分之百确定他们正在与正确的服务器进行通信。

Perfect forward security（PFS）是一种机制，用于在服务器的私钥被泄露时保护客户端。由于PFS，攻击者无法解密任何先前的TLS通信。为了确保完美的 forward security ，我们为每个会话使用新密钥。只要会话处于活动状态，这些密钥就有效。

由于应用程序可以使用或不使用TLS(或SSL)进行通信，因此客户端有必要向服务器表明 TLS 连接的设置。实现此目的的主要方法之一是为TLS连接使用不同的端口号，例如HTTPS的端口443。另一种机制是客户端向服务器发出特定于协议的请求，将连接切换到TLS;例如，在使用邮件和新闻协议时发出 STARTTLS 请求。

一旦客户端和服务器同意使用TLS，它们就通过 handshaking(握手) 过程协商有状态连接。协议使用与非对称密码的握手，不仅建立密码设置，而且建立特定于会话的共享密钥，使用对称密码对进一步的通信进行加密。在这个握手过程中，客户端和服务器就用于建立连接安全性的各种参数达成一致:

+ 当客户端连接到启用TLS的服务器请求安全连接并且客户端提供受支持的密码套件列表（密码和散列函数）时，握手开始。
+ 从该列表中，服务器选择它也支持的密码和散列函数，并通知客户端该决定。
+ 然后，服务器通常以数字证书的形式提供标识。证书包含服务器名称，证明证书真实性的可信证书颁发机构（CA）以及服务器的公共加密密钥。
+ 客户在继续之前确认证书的有效性。
+ 要生成用于安全连接的会话密钥，客户端要么：
  + 使用服务器的公钥加密随机数，并将结果发送到服务器（只有服务器能够使用其私钥解密）; 然后，双方使用随机数生成唯一的会话密钥，用于在会话期间对数据进行后续加密和解密
  + 使用Diffie-Hellman密钥交换来安全地生成用于加密和解密的随机且唯一的会话密钥，该密钥具有前向保密的附加属性：如果将来公开服务器的私钥，则它不能用于解密当前会话，即使会话被第三方截获并记录。

### Terminology

#### Encryption

Encryption(加密) 是将人类可读消息（明文）转换为加密的非人类可读格式（密文）的过程。加密的主要目的是确保只有授权的收件人才能解密和读取原始邮件。当双方之间使用任何媒体交换未加密的数据时，第三方可以拦截并读取所交换的通信。

如果交换包含敏感信息，则意味着失去机密性。此外，如果第三方可以拦截和读取消息，他们可以篡改数据。这意味着他们可以更改正在交换的信息，因此会破坏邮件的完整性。

想象一下，使用未加密的Web浏览器连接发送付款。付款包括您的银行帐户详细信息以及您授权的金额。攻击者可以使用中间人攻击来篡改发送到Web服务器的信息，并将金额从100美元更改为10,000美元。银行接收来自第三方而非您的篡改数据，这意味着没有真实性。如果您使用加密的安全会话，攻击者可能仍然能够拦截流量，但他们将无法读取数据或篡改数据。

![gcheap](/img/TSL-SSL/terminology-encryption.png)

#### Symmetric Encryption

Symmetric Encryption(对称加密) 是使用相同密钥加密和解密数据的过程。如果Thomas想要向Bob发送信息，他将使用共享密钥加密数据，Bob将使用相同的密钥解密数据。

![gcheap](/img/TSL-SSL/terminology-symmetric_encryption.png)

对称密钥加密的最大问题是交换数据的双方必须具有共享密钥。如果公开该共享密钥，攻击者将能够解密使用该密钥加密的所有通信。这就是为什么共享密钥必须使用已经建立的，安全的加密通信信道在各方之间分配的原因。对称加密的另一个缺点是您无法验证邮件的发件人，这会损害真实性。

对称加密的优点：

+ 快速，低资源使用
+ 操作简单
+ 安全

对称加密的缺点：

+ 用于加密/解密的相同密钥
+ 密钥必须使用已建立的安全通道进行分发
+ 不同方的不同关键密钥 - 密钥管理/分配困难
+ 无法验证用户身份

#### Asymmetric Encryption

Asymmetric Encryption(非对称加密,也称为 Public Key Cryptography 公钥加密)使用密钥对：公钥和私钥。这些加密密钥是唯一相关的。这意味着使用密钥对中的一个密钥加密的内容只能使用另一个密钥进行解密。顾名思义，公钥可以与任何人共享。私钥必须仅为所有者所知。

![gcheap](/img/TSL-SSL/terminology-asymmetric_encryption.png)

还可以使用非对称加密通过签名对发件人进行身份验证。如果Bob使用他的私钥签署消息，那么使用Bob的公钥验证签名的人可以确定Bob是发送者。

非对称加密的优点：

+ 密钥分发很容易
+ 真实性
+ 公正
+ 安全

非对称加密的缺点：

+ 比对称加密慢
+ 需要更多资源

#### Ciphers

Ciphers(密码)是用于加密和解密数据的方法/算法。TLS是一种允许使用许多不同方法/算法的协议。它们提供称为 cipher suites(密码套件)的包。这样的包对于每个任务具有不同的方法/算法。

#### Block Ciphers

如果使用 Block Ciphers(分组密码)，则将数据分成固定长度的块（例如64位或128位块），然后进行加密。如果最后一个数据块短于指定的块长度，则算法使用填充来填充空白空间。通常使用随机数据填充块。流行的分组密码包括 AES，Blowfish，3DES，DES 和 RC5。

#### Padding

分组密码具有指定的固定长度，并且大多数密码要求输入数据是其大小的倍数。最后一个块通常包含不符合此要求的数据。在这种情况下，Padding(填充,通常是随机数据)用于使其达到所需的块长度。

#### Initialization Vector (IV)

Initialization Vector(初始化向量) 是加密方法中使用的随机（或伪随机）固定大小的输入。IV的主要目的是启动加密方法。在诸如Cipher Block Chainning（CBC,密码块链接）的密码模式中，每个块与前一个块进行异或(XOR-ed)。在第一个块中，没有先前的块与异或。则初始化向量用作第一个块的输入以开始该过程。

如果IV对于每条消息都是唯一的，则称为 nonce，这意味着它只能使用一次。随机数应该是不可预测的。它还用于防止攻击者通过猜测IV来解密所有消息。如果使用随机数，则可以使用相同的密钥将相同的明文加密成不同的密文。

#### Block Cipher Operation Modes

Block Cipher Operation Modes(分组密码操作模式) 定义使用密码编码的块之间的关系。创建了不同的模式以使攻击者更难以猜测消息的原始内容。

#### Electronic Code Book (ECB)

使用ECB时，每个数据块都是单独加密的，然后按原始顺序连接起来。由于块不相互依赖，因此可以进行并行处理。没有必要进行IV。ECB的主要问题是如果相同的数据块被加密，它将始终生成相同的密文。这使攻击者更容易根据重复模式猜测原始数据。

![gcheap](/img/TSL-SSL/teriminology-ECB.png)

#### Cipher Block Chainning (CBC)

使用CBC时，每个块在加密前与先前的密文进行异或(XOR-ed)。这消除了重复图案的问题。需要IV来加密第一个明文块。由于块是链接的，因此不可能进行并行处理。CBC有一个主要缺点：如果消息的一部分出现乱码或丢失，则消息的其余部分将丢失。

![gcheap](/img/TSL-SSL/teriminology-CBC.png)

#### Cipher Feedback (CFB)

CFB方法将块密码转换为 self-synchronizing stream cipher(自同步流密码)。这意味着如果消息的一部分是乱码或丢失，则密码可以在几个块之后同步，并且消息的其余部分不一定丢失。

![gcheap](/img/TSL-SSL/teriminology-CFB.png)

#### Output Feedback (OFB)

OFB方法创建 synchronous stream cipher(同步流密码)。该技术保留了纠错码。加密和解密过程完全相同。

![gcheap](/img/TSL-SSL/teriminology-OFB.png)

#### Counter Mode (CTR)

CTR方法类似于OFB，因为它还创建了一个 synchronous stream cipher(同步流密码)。但是，它为每个块使用 counter 和 nonce，并且不将块链接在一起。因此，可以并行加密和解密块。

![gcheap](/img/TSL-SSL/teriminology-CTR.png)

#### Stream Ciphers

Stream Ciphers(流密码) 每次只加密一位或一个字节的数据。每一位都用不同的密钥加密。在现代密码术中不经常使用流密码。流密码的一个流行示例是 RC4 cipher。

#### Message Authentication Code (MAC)

Message Authentication Code(MAC,消息认证码) 是一种用于检查消息的真实性和完整性的方法。它接受两个输入参数：密钥和任意长度的消息。结果称为 tag(标签)。收件人还具有密钥，可以使用它来检测邮件内容的任何更改。MAC有时称为 checksum(校验和)， cyptographic checksum(加密校验和) 或 protected checksum(受保护的校验和)。

![gcheap](/img/TSL-SSL/teriminology-MAC.png)

如果发件人的MAC标记与收件人的计算MAC标记匹配，则没有人篡改该消息。如果它们不匹配，则有人在传输过程中更改了消息。

#### Hash-Based Message Authtication Code (HMAC)

HMAC是一种使用散列函数的MAC。以下是使用SHA256哈希算法的HMAC示例:

```
HMAC_SHA256("s3cr3tk3y","Hello World") = 2d9615ee921dab63c7c4c839842703fe338db46fdf17593a681bcee2c52721de
```

下图显示了HMAC功能的工作原理：

![gcheap](/img/TSL-SSL/teriminology-HMAC.png)

### Certificates

#### Certificates Authorities

如果您访问银行的网站并收到由其他实体签名的证书，您可能仍会对网站安全性感到不确定。您可能会担心签署证书的实体是冒名顶替者。公钥基础结构（PKI）解决了这个问题。PKI包括管理数字证书和公钥加密所需的一切。

您可以信任几个PKI实体。它们被称为 Certificates Authorities (CAs, 证书颁发机构)。他们验证其他实体（公司，组织，个人）并确认他们确实是他们所说的人。经过此类验证，CA会使用自己的证书对证书进行签名。CA的证书称为 root certificate(根证书)。

所有CA的 root certificate （以及它们的公钥）都被认为是可信的。它们安装在Chrome，Firefox和Edge等所有浏览器中以及操作系统（包括Windows）中。流行的CA包括IdenTrust，Comodo，DigiCert，GoDaddy，GlobalSign和Symantec。目前有超过200个根证书受到浏览器的信任。

TLS/SSL Web连接需要 TLS/SSL 证书，但该证书可由任何人签名。它甚至可以自签名（由创建证书的实体签名）。访问使用 TLS/SSL 保护的网站时，浏览器会通过检查该网站是否由受信任的根证书签名来检查该网站是否具有有效证书。它还会检查证书是否适用于您正在访问的域，并显示有关证书所有者的信息以供您验证。如果证书未由受信任的根证书签名，则Web浏览器会显示明确的警告。您通常可以选择忽略警告（取决于Web浏览器设置），但您不能错过它。

#### Secure Browsing

容易识别网站是否具有有效证书以及您是否使用安全连接。您需要做的就是查看地址栏（类似于所有主流浏览器）

![gchesp](/img/TSL-SSL/certificates-secure_browsing.png)

绿色锁和HTTPS协议（ https:// ）表示与Web服务器的连接是加密且安全的。

#### Insecure Browsing

识别非安全网站也很容易。没有绿色锁，也没有提到HTTPS。

![gcheap](/img/TSL-SSL/certificates-insecure_browsing1.png)

但是，有些网站使用HTTP来传递部分内容，例如图像。在这种情况下，您将看到类似于此消息的消息：

![gcheap](/img/TSL-SSL/certificates-insecure_browsing2.png)

仅部分受保护的内容称为混合内容。混合内容违背了安全连接的目的。当您从登录的网站请求文件时，Web浏览器会自动发送您的身份验证Cookie以及请求。

因此，如果使用HTTP加载资源，则会通过非加密连接发送您的请求。如果攻击者正在嗅探网络，他们就能以明文形式看到此请求。这会危及会话的安全性，因为攻击者使用cookie登录网站并冒充您。因此，您应该像处理未加密的网站一样处理混合内容的网站。

#### Type of TLS/SSL Certificates

TLS/SSL 证书有不同的版本。从技术角度来看，它们可以分为三组，具体取决于它们适用的域的范围。

##### Sigle-Domain

此类证书仅适用于一个主机名（Full Qualified Domain Name, 完全限定域名 - FQDN）或子域。例如，您可能会获得www.example.com或my.example.com的证书。但是，mail.example.com不会包含在此证书的范围内。证书仅对您在注册期间指定的一个主机名有效。

##### Wildcard 

此类证书适用于包含其所有子域的整个域。例如，如果您注册 *.example.com， 则证书将应用于 mail.example.com， secret.example.com， admin.example.com和所有其他子域。只要域相同，您就可以在不同服务器上托管每个子域，并在多个服务器上使用相同的通配符 TLS/SSL 证书。

##### Muti-Domain

此类证书适用于多个不同的域名。每个域名可以是 Single-Domain 或 Wildcard 。通常，当您获得此类证书时，您可以随时更改域名。此类证书通常也称为 Subject Alternative Name(SAN,主题备用名称) 证书。

#### TLS/SSL Certificates Validation

从身份验证的角度来看，TLS/SSL 证书也有不同的版本。身份验证越多，证书越可信，但获取证书所需的时间越多。

##### Domain Validation

域验证证书仅确认申请证书的人是域名的所有者（或至少可以访问域名）。这种验证通常只需要几分钟到几个小时。

##### Organization Validation

Certification Authority（CA）不仅验证域名所有权，还验证所有者的身份。这意味着可能会要求所有者提供证明其身份的个人信息和身份证明文件。此类验证可能需要几天时间。

##### Extended Validation

这是最高级别的验证。它包括域名所有权和所有者身份的验证，但它也要求企业提供合法注册证明。

#### Certification Generation

如果要从证书颁发机构申请证书，则需要生成 Certificate Signing Request(CSR,证书签名请求)。首先，创建一个用于解密证书的私钥。然后，生成CSR。生成CSR时，系统会要求您指定域名以及有关您组织的详细信息，例如姓名，国家/地区和电子邮件。以下是CSR的示例。

```
-----BEGIN CERTIFICATE REQUEST-----
MIICtzCCAZ8CAQAwUTELMAkGA1UEBhMCQ1kxCjAIBgNVBAgMAWExCzAJBgNVBAcM
Ak1lMQowCAYDVQQKDAFhMQowCAYDVQQLDAFhMREwDwYDVQQDDAh0ZXN0LmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKvFkdX1qwMNu0i0GHW/lotRKYM0I3yvHQmeS5DtYqmnMGsIZaUO7qv+z8CW4cIIqZhR/hlXEsh+ARM/po37OjzzSDo1U7gyKciSf2s+JsuLmlrHoZPto+/4uWgp9xyQW177/MvWtOVejaUnzrjmPnE0
AT9KAZ3w+2uwjrhJG5w52psENUT+tTOMlDgIVlKSbZcvD5bS/X7RvfsOS3Q/y9wG
Q53rbZqK19y5CtM808wGOQhrNfp3M1EA6+m7RRO1Yw2Rp+wLY0aA9UzjzImaL5Sr
/job1EoJWzKClY20GXB6HKn+wJ/n4sz725bF6l6r4yoBY1f4gYBn3QW+sQXLrDsC
AwEAAaAhMB8GCSqGSIb3DQEJBzESDBBkZmpoZ2tqaGpoZGZramhnMA0GCSqGSIb3
DQEBCwUAA4IBAQCFQ7/R+/ioSj7X4gs+GBbDHEcnJHshwoX9vVBDYvOoQ56iER7f
cEtja18yeXu3PNyeOoDLSYd0FhM16XKLlJ0llIy46Vb8RMdS4JNEx2yob3W/bIAS
z2n+p58zp2/Gp7gG2LtH+RwcvRGRGdKhrsU8D+fHGHpSGvGJg++IhS2HZvTs5pkD
3AwMpDojVYtWuJteDVHGc4PH5TeJot7+6lGetkhq1uRhD4KjJDY5KUvCNQIjeoaL
eFf/xGp6JGNE5taK2liBs+QlgLZc8Sm7fTYCi0YXAsEhMm9HjbXX28Ou6zTroDP3
elT3tN9pd1aG6ujGjkrM6T8JiVWxqYFEnFqd
-----END CERTIFICATE REQUEST-----
```

生成CSR后，必须将其提交给CA. 证书准备就绪后，CA通常会将其作为 *.crt 文件发送到您的电子邮件地址。您必须在服务器上安装此文件。

### Establishing a TLS Connection

建立安全 TLS/SSL 连接的过程涉及几个步骤。TLS/SSL 安全协议使用非对称和对称加密的组合。客户端和服务器必须协商使用的算法并交换密钥信息。

为了解释这个复杂的过程，我们使用TLS 1.2连接，而不是最新的TLS 1.3协议。对于所有先前版本的TLS/SSL，TLS 1.2中使用的过程几乎相同。但是，最新版本的传输层安全性大大简化了它。

建立安全连接最重要的部分称为 handshake(握手)。在TLS握手期间，服务器和客户端交换用于确定连接属性的重要信息。此示例基于Web浏览器握手，但这同样适用于所有其他 TLS/SSL 握手。

#### Step 1:Client Hello (Client - Server)

![gcheap](/img/TSL-SSL/tlsConnection-step1.png)

首先，客户端向服务器发送客户端Hello。Client Hello包含以下信息。

**Client Version**

客户端发送它支持的所有 TLS/SSL 协议版本的列表，首选列表中的首选版本通常是最新版本。例如，TL​​S 1.2有一个client_version 3,3。这是因为TLS 1.0被视为 Secure Sockets Layer（SSL 3.0）的次要修订版，因此 TLS 1.0 为 3.1，TLS 1.1 为 3.2，依此类推。

**Client Random**

客户端和服务器随机生成一个32字节的随机数用于后来生成加密密钥。

原始的TLS 1.2规范中，前4个字节应该表示客户端的当前日期和时间（以纪元格式），其余28个字节应该是随机生成的数字。但是，IETF后来建议不使用这个格式。

**Session ID**

这是用于连接的 Session ID。如果session_id不为空，则服务器搜索先前缓存的会话，并在找到匹配时恢复该会话。

**compression_methods**

这是将用于 compression(压缩) SSL 数据包的方法。通过使用压缩，我们可以实现更低的带宽使用率，从而提高传输速度。但是使用压缩是有风险的。

**Cipher Suites**

Cipher Suites 是加密算法的组合。通常，每个 Cipher Suites 都包含一个用于以下任务的加密算法： key exchange(密钥交换)， authentication(身份验证)， bulk encryption (批量数据加密) 和 message authentication(消息身份验证)。客户端按先后顺序发送它支持的所有 Cipher Suites 的列表。这意味着客户端更希望使用发送的第一个 Cipher Suites 建立连接。

Cipger Suites 由字符串标识。示例 Cipher Suites 字符串：

TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256

该字符串包含以下信息：

+ 正在使用的协议是TLS
+ 密钥交换算法是ECDHE（Elliptic Curve Diffie-Hellman）
+ 认证算法是ECDSA（Elliptic Curve Digital Signature Alogrithm）
+ 数据加密算法是AES_128_GCM（Advanced Encryption Standard 128 bit Galois/Counter Mode）
+ 消息验证码（Message Authentication Code,MAC）算法是SHA256（Secure Hash Alogrithm 256 bit）

**Compression Methods**

这是一个用于 Compression(压缩数据) 的方法列表（在加密之前）。如果使用压缩，则可以降低带宽使用率并加快传输速度。但是，压缩是有风险的，建议不要：详情查看下面的 [CRIME and BREACH attacks](#CRIME_and_BREACH_attacks)。

**Extensions**

客户端可以请求连接的其他功能。这可以通过 Extensions(扩展) 来完成，例如 supported groups for elliptic curve cryptography， point formats for elliptic curve cryptography， signature 等。如果服务器无法提供附加功能，则客户端可以在需要时中止握手。

以下是Wireshark捕获中实际的Client Hello的样子。

![gcheap](/img/TSL-SSL/tlsConnection-step1-wireshark.png)

#### Step 2:Server Hello (Server - Client)

在服务器接收到客户端Hello之后，它将使用服务器Hello进行响应。服务器Hello可以包含选定的选项(从客户端Hello期间建议的选项中选择)，也可以是握手失败消息。一般包含以下内容：

**Server Version**

服务器从客户端的提供信息中选择 TLS/SSL 协议的首选版本。

**Server Random**

客户端和服务器随机生成一个32字节的随机数用于后来生成加密密钥。

原始的TLS 1.2规范中，前4个字节应该表示客户端的当前日期和时间（以纪元格式），其余28个字节应该是随机生成的数字。但是，IETF后来建议不使用这个格式。

**Session ID**

如果客户端 Seesion ID 不为空，则服务器搜索先前缓存的 Session ，如果找到匹配，则使用该 Session ID恢复 Session。如果客户端 Session ID为空，则服务器可以创建一个新 Session 并将其发送到服务器 Session ID中。

**Cipher Suites**

服务器从Client Hello中发送的 Cipher Suites 中选择 Cipher Suites。

**Compression Methods**

服务器从Client Hello中发送的压缩方法里中选择压缩方法。

#### Step 3:Server Certificate (Server - Client)

服务器发送签名的 TLS/SSL 证书，证明其身份给客户端。它还包含服务器的公钥。

#### Step 4:Client Certificate (Client - Server,Optional)

在极少数情况下，服务器可能要求客户端使用客户端证书进行身份验证。如果是，则客户端将其签名证书提供给服务器。

#### Step 5:Server Key Exchange (Server - Client)

仅当服务器提供的证书不足以使客户端交换 pre-master sercet 时，才发送服务器密钥交换消息。 （这适用于 DHE_DSS， DHE_RSA和 DH_anon）。

#### Step 6:Server Hello Done (Server - Client)

服务器将此发送到客户端以确认服务器Hello消息已完成。

Wireshark捕获中的服务器Hello看起来是这样子。

![gcheap](/img/TSL-SSL/tlsConnection-step6.png)

#### Step 7:Client Key Exchange (Server - Client)

从服务器收到服务器Hello Done后立即发送客户端密钥交换消息。如果服务器请求客户端证书，则在此之后发送客户端密钥交换。在此阶段，客户端创建 pre-master key。

**Pre-Master Sercet**

Pre-Master Sercet 由客户端创建（创建方法取决于 cipher suites），然后与服务器共享。

在将 Pre-Master Sercet 发送到服务器之前，客户端使用从服务器提供的证书中提取的服务器公钥对其进行加密。这意味着只有服务器才能解密消息，因为非对称加密（密钥对）用于 pre-master sercet 交换。

这就是Wireshark捕获中的密钥交换（使用Diffie-Hellman）。

![gcheap](/img/TSL-SSL/tlsConnection-step7.png)

**Master Sercet**

服务器接收到 pre-master sercet key 后，使用其私钥对其解密。现在，客户机和服务器使用伪随机函数(PRF)根据前面交换的随机值(客户机随机值和服务器随机值)计算主密钥。PRF是一个函数，用于生成任意数量的伪随机数据。

```
master_secret = PRF(pre_master_secret, "master secret", ClientHello.random + ServerHello.random) [0..47];
```

然后，客户端和服务器将使用长度为48字节的主密钥对对称地加密用于剩余通信的数据。

客户端和服务器各创建一组3个密钥：

+ client_write_MAC_key: Authentication and Integrity check(身份验证和完整性检查)
+ server_write_MAC_key: Authentication and Integrity check(身份验证和完整性检查)
+ client_write_key: Message encryption using symmetric key(使用对称密钥进行消息加密)
+ server_write_key: Message encryption using symmetric key(使用对称密钥进行消息加密)
+ client_write_IV: Initialization Vector used by some AHEAD ciphers(一些前置密码使用的初始化向量)
+ server_write_IV: Initialization Vector used by some AHEAD ciphers(一些前置密码使用的初始化向量)

客户端和服务器都将使用 master sercet 生成将加密/解密数据的 session keys。


#### Step 8:Client Change Cipher Spec (Client - Server)

此时，客户端已准备好切换到安全的加密环境。 Change Cipher Spec 协议用于更改加密。客户端从现在开始发送的任何数据都将使用对称共享密钥进行加密。

这是Change Cipher Spec在Wireshark捕获中的样子。

![gcheap](/img/TSL-SSL/tlsConnection-step8.png)

#### Step 9:Client Handshake Finished (Client - Server)

来自客户端的握手过程的最后一条消息表示握手已完成。这也是安全连接的第一个加密消息。

![gcheap](/img/TSL-SSL/tlsConnection-step9.png)


#### Step 10:Server Change Cipher Spec (Server - Client)

服务器也准备切换到加密环境。服务器从现在开始发送的任何数据都将使用对称共享密钥进行加密。

#### Step 11:Server Handshake Finished (Server - Client)

来自服务器的握手过程的最后一条消息（已加密发送）表示握手已完成。

![gcheap](/img/TSL-SSL/tlsConnection-step11_1.png)

回顾一下，以下说明了典型的握手

![gcheap](/img/TSL-SSL/tlsConnection-step11_2.png)

### The TLS Handshake in TLS 1.3

在TLS 1.2及更早版本中，TLS握手需要完成两次往返。第一次往返是交换hellos，第二次是密钥交换和更改密码规范。在TLS 1.3中，这个过程简化了，只需要往返一次。 TLS 1.3也不再支持 TLS Compression(压缩)

![gcheap](/img/TSL-SSL/tlsConnection-tls13_handshake.png)

在TLS 1.3中，当客户端发送hello时，它会立即自动判断处服务器最有可能选择的密钥协商协议。同时，它使用判断出的协议共享其密钥。服务器的hello消息还包含共享密钥，证书和服务器完成消息。不需要密码更改，因为在交换了hellos之后，双方已经拥有加密通信所需的全部内容。

### TLS Vulnerabilitis and Attacks

Secure Sockets Layer（SSL）和 Transport Layer Security（TLS）加密协议像其他所有技术一样存在缺陷。以下是 TLS/SSL 协议中的主要漏洞。它们都会影响协议的旧版本（TLSv1.2及更早版本）。在发布时，只发现了一个影响TLS 1.3的主要漏洞。但是，与此处列出的许多其他攻击一样，此漏洞也基于强制降级攻击。(由于它们利用的攻击和漏洞的复杂性，示例简化了描述并基于Web示例（Web客户端和Web服务器）)

#### POODLE

Padding Oracle On Downgraded Legacy Encryption（POODLE）攻击于2014年10月发布，并利用了两个因素。第一个因素是某些服务器/客户端仍支持SSL 3.0，以实现与旧系统的互操作性和兼容性。第二个因素是SSL 3.0中存在的漏洞，该漏洞与块填充有关。 POODLE漏洞在NIST NVD数据库中注册为CVE-2014-3566。

客户端启动握手并发送支持的 SSL/TLS 版本列表。攻击者拦截流量，执行中间人（MITM）攻击，并模拟服务器，直到客户端同意将连接降级到SSL 3.0。

![gcheap](/img/TLS-SSL/POODLE.png)

SSL 3.0漏洞处于 Cipher Block Chaining（CBC）模式。分组密码需要固定长度的块。如果最后一个块中的数据不是块大小的倍数，则通过填充填充额外的空间。服务器忽略填充的内容。它仅检查填充长度是否正确并验证明文的Message Authentication Code（MAC）。这意味着服务器无法验证是否有人修改了填充内容。

攻击者可以通过修改填充字节和观察服务器响应来解密加密块。解密单个字节最多需要256个SSL 3.0请求。这意味着每256个请求一次，服务器将接受修改后的值。攻击者不需要知道加密方法或密钥。使用自动化工具，攻击者可以逐个字符地检索明文。这可以很容易地是密码，cookie，session或其他敏感数据。

**Prevention**

+ 完全禁用服务器上的SSL 3.0（强烈建议,除非您必须支持Internet Explorer 6.0）。
+ 将浏览器（客户端）升级到最新版本。如果必须使用旧版本，请禁用SSLv2和SSLv3。大多数当前的浏览器/服务器使用TLS_FALLBACK_SCSV。如果客户端请求的TLS协议版本低于服务器（和客户端）支持的最高版本，则服务器会将其视为故意降级并断开连接。
+ 一些 TLS 1.0/1.1 实现也容易受到POODLE的攻击，因为它们在解密后接受不正确的填充结构。

#### BEAST

Browser Exploit Against SSL/TLS（BEAST）攻击于2011年9月披露。它适用于SSL 3.0和TLS 1.0，因此它会影响支持TLS 1.0或更早版本协议的浏览器。攻击者可以利用TLS 1.0中 Cipher Block Chaining （CBC）模式实施中的漏洞来解密双方之间交换的数据。 BEAST漏洞在NIST NVD数据库中注册为CVE-2011-3389。

这是一种使用中间人技术的客户端攻击。攻击者使用MITM将数据包注入TLS流。这允许他们猜测与注入消息一起使用的初始化向量（IV），然后简单地将结果与他们想要解密的块进行比较。

为了使BEAST攻击成功，攻击者必须对受害者的浏览器有一些控制权。因此，攻击者可以选择更容易的攻击向量而不是这个。

**Prevention**

+ Use TLS 1.1 or TLS 1.2
+ + 最初，建议用于缓解BEAST攻击的方法之一是使用RC4密码。但是，后来发现RC4加密协议不安全。 PCI DSS（支付卡行业数据安全标准）禁止使用此密码，Microsoft也强烈建议不要在Windows中使用它。

#### CRIME (CVE-2012-4929)

Compression Ratio Info-leak Made East（CRIME）漏洞影响TLS压缩。压缩方法包含在Client Hello消息中，并且是可选的。您可以在不压缩的情况下建立连接。压缩被引入 SSL/TLS 以减少带宽。 DEFLATE是最常用的压缩算法。 CRIME漏洞在NIST NVD数据库中注册为CVE-2012-4929。

这是一个Wireshark捕获服务器Hello消息（响应客户端Hello）。服务器选择NULL压缩方法，这意味着不使用压缩。

![gcheap](/img/TLS-SSL/CRIME1.png)

压缩算法使用的主要技术之一是用指向该序列的第一个实例的指针替换重复的字节序列。重复的序列越大，压缩比越高。

![gcheap](/img/TLS-SSL/CRIME2.png)

让我们假设攻击者想要获得受害者的cookie。他们知道目标网站（examplebank.com）为名为adm的会话创建了一个cookie。攻击者知道DEFLATE压缩方法替换重复的字节。因此，攻击者将 Cookie：adm = 0 注入受害者的cookie中。服务器只会在压缩响应中附加0，因为 Cookie：adm = 已经在受害者的cookie中发送，因此会重复。

![gcheap](/img/TLS-SSL/CRIME4.png)

攻击者必须做的就是注入不同的字符，然后监视响应的大小。如果响应比初始响应短，则注入的字符包含在cookie值中，因此它被压缩。如果字符不在cookie值中，则响应将更长。

![gcheap](/img/TLS-SSL/CRIME3.png)

使用此方法，攻击者可以使用从服务器获得的反馈来重建cookie值。

**Prevention**

+ 将浏览器升级到最新版本

#### BREACH

通过 Browser Reconnasance（BREACH）漏洞进行浏览器侦察和泄漏与CRIME非常相似，但BREACH的目标是HTTP压缩，而不是TLS压缩。即使关闭TLS压缩，也可以进行此攻击。攻击者强制受害者的浏览器连接到启用TLS的第三方网站，并使用中间人攻击监视受害者与服务器之间的流量。 BREACH漏洞在NIST NVD数据库中注册为CVE-2013-3587。

易受攻击的Web应用程序必须满足以下条件:

+ 从使用HTTP级压缩的服务器提供服务
+ 反映HTTP响应正文中的用户输入
+ 在HTTP响应主体中反映一 sercet（例如CSRF令牌）（因此使用 HTTP Header 中的值，例如cookie，可以免受此攻击）

**Prevention**

+ Disable HTTP compression
+ Separate secrets from user input
+ Randomize secrets per request
+ Mask secrets (effectively randomize by XORing with a random secret per request)
+ Protect pages against CSRF
+ Hide the length (by adding random numbers of bytes to responses)
+ Limit the rate of requests

#### Heartbleed

Heartbleed是一个重要的漏洞，可以在流行的OpenSSL库的 Heartbleed 扩展中找到。只要双方仍在那里，此扩展用于保持连接存活。 Heartbleed 漏洞在 NIST NVD数据库中注册为 CVE-2014-0160。

客户端使用包含数据和数据大小（以及填充）的有效负载向服务器发送心跳消息。服务器必须使用相同的心跳请求进行响应，该请求包含客户端发送的数据和数据大小。

![gcheap](/img/TLS-SSL/Heartbleed.png)

Heartbleed漏洞基于以下事实：如果客户端发送了错误的数据长度，服务器将使用客户端接收的数据和来自其内存的随机数据来响应，以满足发送方指定的长度要求。

![gcheap](/img/TLS-SSL/Heartbleed1.png)

从服务器内存中获取未加密的数据可能是灾难性的。已经存在此漏洞的概念验证漏洞，其中攻击者将获取服务器的私钥。这意味着攻击者可以解密到服务器的所有流量。服务器内存可能包含任何内容：凭据，敏感文档，信用卡号，电子邮件等。

**Prevention**

+ 更新到最新版本的OpenSSL。如果无法做到这一点，请使用-DOPENSSL_NO_HEARTBEATS重新编译已安装的版本

**Conclusion**

TLS/SSL 协议用于保护数据传输，但配置错误的服务器可能会暴露数据而不是保护数据。

在大多数情况下，保护自己免受 TLS/SSL 相关攻击的最佳方法是禁用较旧的协议版本。这甚至是某些行业的标准要求。例如，2018年6月30日是根据PCI数据安全标准禁用对SSL和早期版本的TLS（包括TLS 1.0）的支持的截止日期。互联网工程任务组（IETF）发布了有关SSL安全性的建议：RFC 6176和RFC 7568.IETF很快就会对TLS 1.0和1.1进行弃用。

# 参考资料

+ [Wikipedia - Application layer](https://en.wikipedia.org/wiki/Application_layer)
+ [acunetix - What Is SSL/TLS](https://www.acunetix.com/blog/articles/tls-security-what-is-tls-ssl-part-1/)
+ [acunetix - Recommendations for TLS/SSL Cipher Hardening](https://www.acunetix.com/blog/articles/tls-ssl-cipher-hardening/)