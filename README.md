# Reading HK Octopus card info
To read HK Octopus card using PN532 NFC module

## What is NFC (Wiki)
NFC is a set of short-range wireless technologies, typically requiring a separation of 10 cm or less. NFC operates at 13.56 MHz on ISO/IEC 18000-3 air interface and at rates ranging from 106 kbit/s to 424 kbit/s. NFC always involves an initiator and a target; the initiator actively generates an RF field that can power a passive target. This enables NFC targets to take very simple form factors such as unpowered tags, stickers, key fobs, or cards. NFC peer-to-peer communication is possible, provided both devices are powered.[55]

NFC tags contain data and are typically read-only, but may be writable. They can be custom-encoded by their manufacturers or use NFC Forum specifications. The tags can securely store personal data such as debit and credit card information, loyalty program data, PINs and networking contacts, among other information. The NFC Forum defines four types of tags that provide different communication speeds and capabilities in terms of configurability, memory, security, data retention and write endurance.

NFC是Near Field Communication缩写，即近距离无线通讯技术。由飞利浦和索尼公司共同开发的NFC是一种非接触式识别和互联技术，可以在移动设备、消费类电子产品、PC 和智能控件工具间进行近距离无线通信。NFC 提供了一种简单、触控式的解决方案，可以让消费者简单直观地交换信息、访问内容与服务。目前，NFC 论坛在全球拥有 70 多个成员，包括：万事达卡国际组织、松下电子工业有限公司、微软公司、摩托罗拉公司、NEC 公司、瑞萨科技公司、三星公司、德州仪器制造公司和 Visa 国际组织。NFC是在RFID的基础上发展而来，NFC从本质上与RFID没有太大区别，都是基于地理位置相近的两个物体之间的信号传输。 近场通信（Near Field Communication或NFC）是由非接触式射频识别（RFID）及互联互通技术整合演变而来，在单一芯片上结合感应式读卡器、感应式卡片和点对点的功能，能在短距离内与兼容设备进行识别和数据交换。工作频率为13.56MHz。但是使用这种手机支付方案的用户必须更换特制的手机。目前这项技术在日韩被广泛应用。手机用户凭着配置了支付功能的手机就可以行遍全国：他们的手机可以用作机场登机验证、大厦的门禁钥匙、交通一卡通、信用卡、支付卡等等[10]。

NFC标准兼容了索尼公司的FeliCaTM标准，以及ISO 14443 A，B，也就是使用飞利浦的MIFARE标准。在业界简称为TypeA，TypeB和TypeF，其中A，B为Mifare标准，F为Felica标准。芯片是除了具有相互通信功能外，还具有计算能力，在Felica标准中还含有加密逻辑电路，MIFARE的后期标准也追加了加密/解密模块(SAM)。为了推动NFC的发展和普及，业界创建了一个非赢利性的标准组织—NFC Forum，促进NFC技术的实施和标准化，确保设备和服务之间协同合作[11]。目前，NFC Forum在全球拥有数百个成员，包括：SONY， Phlips，LG，摩托罗拉， NXP，NEC、三星、Atoam、Intel、其中中国成员有中国移动、华为、中兴、上海同耀和台湾正隆等公司。 与RFID一样，NFC信息也是通过频谱中无线频率部分的电磁感应耦合方式传递，但NFC使用一种近场磁场耦合（通常采用磁性薄膜贴合FPC方式）天线，使用13.56Mhz波长，且读写距离很短。首先，其传输范围比RFID小，RFID的传输范围可以达到几米、甚至几十米，但由于NFC采取了独特的信号衰减技术，相对于RFID来说NFC具有距离近、带宽高、能耗低等特点。 NFC与RFID技术兼容，RFID更多的被应用在生产、物流、跟踪、资产管理上，而NFC则在门禁、公交、手机支付等领域内发挥着巨大的作用。和传统的近距通讯蓝牙、红外相比，近场通讯(NFC)就有天然的安全性，以及连接建立的快速性。

NFC使用的是无线射频技术。在RF层，与之相关的规范是ISO 18092（NFC Interface and Protocol I，简称NFCIP-1，该规范定义了NFC RF层的工作流程）和ISO 14443 Type A，Type B和Felica。ISO 14443全称为非接触式IC卡标准，它从RF层面定义了如何与不同的非接触式IC卡（其实物可以是NFC Tag、RFID Tag、Smart Cards）交互。ISO 14443定义了Type A和Type B两种非接触式IC卡。其中，Type A最早由Philips公司制订（其生产的芯片商标名为MIFARE，现在由从Philips独立出来的NXP公司拥有，目前世界上70%左右的非接触式IC卡都使用了MIFARE芯片，例如北京市的公交卡），Type B（主要用在法国市场）由其他公司制订，二者最终都成为ISO标准。Felica（也被称为Type F）由Sony开发，它最终没有成为ISO标准，而是成为日本工业标准JIS X6319-4，所以Felica主要用于日本市场。Type A、B和F主要区别在于RF层的信号调制解调方法、传输速率及数据编码方式上。关于ISO 14443和Felica之间的区别，请读者阅读参考资料。 RF层之上是Mode Switch，它用于确定对端NFC Device的类型并选择合适的RF层协议与之通信
 　　
## NFC Forum标签平台四种标签类型详细介绍：
类型1基于ISO14443A，目前由Innovision研究和技术公司独家供应 (TopazTM)，具有96字节内存，成本低，应用广泛。
类型2同样基于ISO14443A，目前由Philips独家供应 (MIFARE UltraLight)，内存是1类标签的一半。
类型3基于FeliCa，目前由Sony独家供应，具有较大内存（目前为2千字节）和较高传输速率（每秒212KB），适用于更复杂的应用。
类型4完全兼容ISO14443A/B，很多制造商都有生产，包括Philips（典型产品如MIFAREDESFire）。内存更大，读取速率在每秒106KB和424KB之间，适用于多种应用。
 
值得注意的是，1类和2类标签与3类和4类标签的内存差别很大，因此又构成两个大类。在各种可能的应用类型中基本不存在重叠。

## NDEF及NFC Record
1. NDEF和NFC Record之间的关系
根据NFC Forum的定义，R/W模式下，NFC设备之间每一次交互的数据都会封装在一个NDEF Message中，而一个NDEF Message可以包含多个NFC Record，真正的数据则封装在NFC Record中。图8-5展示了NDEF Message和NFC Record之间的关系。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/4916cf71-c63f-4e03-87e3-db4d479bba00)

由上图可知，一个NDEF Message可包含一个或多个NFC Record。在一个NDEFMessage中，第一个NFC Record需设置其MB位（Message Begin）为1，表示它是该消息中第一个NFC Record，最后一个NFC Record需设置ME位（Message End）位为1，表示它是此消息中最后一个NFC Record。

![image](https://github.com/justinlaw360/octopuscard/assets/4946026/ccc8a06e-eb4b-4d8e-a985-a6e7808f2573)

NFC Record本身的组织结构如图所示。NFC Record分为NFC Record https://so.csdn.net/so/search?q=Header&spm=1001.2101.3001.7020（头部信息）和Payload（数据载荷）两大部分。Record Header中最重要的是其第一字节。该字节有6个标志信息，分别如下。
Record Header第一字节
·MB（Message Begin标志）
·ME（Message End标志）
·CF（Chunk Flag标志，表示该Record是否为分片Record）
·SR（Short Record标志。如果该标志被设置，则图中的4个Payload Length字段仅需一个，这表明Payload数据长度将限制在255字节以内）
·IL（ID_LENGTH标志，它用于指明Header中是否包含ID Length和ID这两个字段）
·TNF（Type Name Format标志，用于指明Payload的类型，NFC Forum定义了一些常用的Payload类型，详情见下文分析）
Record Header其他字节如下
·Type Length指明Record Header中Type字段的长度。
·Payload Length 3～Payload Length 0这4个字段共同指明Payload字段的长度。
如果SR标志被设置，则Record Header仅包含一个Payload length字段。
·ID Length指明ID字段的长度。如图所示IL标志未设置，则ID Length和ID字段都不存在。
·Type字段表明Payload的类型，NFC Forum定义了诸如URI、MIME等类型的Type，其目的是方便不同的应用来处理不同Type的数据，例如URI类型的数据就交给浏览器来处理。
·ID需要配合URI类型的Payload一起使用，它使得一个NFC Record能通过ID来指向另外一个NFC Record。
NFC Record中，常令初学者感到困惑的是TNF字段，其作用是什么？来看下文。
TNF和RTD
TNF用于描述一个NFC Record中数据（Payload）的类型，为了方便应用程序能正确解析NFC Record中的数据，NFC Forum规定了一些常用的数据类型，如下表所示。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/9c8a8736-dba8-4aa5-a291-7804992cbb53)


## 目前NFC支持七种数据类型：
	1. Empty：表示该Record中没有数据，即相当于一个空的NFC Record
	2. NFC Forum Well-Known Type：由NFC Forum定义的一些较为常用的数据类型，包括URI、TEXT等，其格式遵循NFC Forum RTD（Record Type Definition）规范。下文将详细介绍它。
	3. MIME：它是Multipurpose Internet Mail Extensions的缩写，遵循RFC2046规范。例如，当TNF取值为MIME时，其Type字段取值可为"text/plain"或"image/png"等。
	4. Absolute URI：绝对URI，遵循RFC 3986规范。例如某文件的绝对URI为"http:/ http://android.com/robots.txt%22%EF%BC%8C%E8%80%8C%E5%85%B6%E7%9B%B8%E5%AF%B9URI%E5%88%99%E4%B8%BA%22robots.txt"。
	5. NFC Forum External Type：也由NFC Forum的RTD规范定义，下文将介绍它。
	6. Unknown：代表Payload中的数据类型未知，它和MIME类型"application/octet-stream"有些类似，这种类型的数据由相应的应用程序来解析。
	7. Unchanged：这种类型的数据用于NFC Record分片。例如一个大的数据需要通过多个NFC Record来承载，除第一个NFC Record分片外，该数据对应的其他NFC Record分片都必须设置TNF为Unchanged。关于这部分内容，读者可参考NDEF规范的2.3.3节"Record Chunks"

在TNF七大类型中，NFC Forum通过RTD规范定义了其中的WKT（Well-KnownType）和External Type两种类型。虽然RTD规范全长只有20来页，但阅读起来比较枯燥，在此，笔者总结其核心内容。
	- 简单点说，WKT就是NFC Forum自己定义的一些常用数据类型，目前常用类型如下。
	- URI Record Type：用于存储URI数据，对应Type字段取值为"U"。
	- Text Record Type：用于存储文本数据，对应Type字段取值为"T"。
	- Signature Record Type：用于存储数字签名数据，对应Type字段取值为"Sig"。
	- Smart Poster Record Type：智能海报，用于存储与该海报相关的一些资讯信息，如图片、相关介绍等，对应Type字段取值为"Sp"
	- Generic Control Record Type：用于传递控制信息，对应Type字段取值为"Gc"
	- External Type：为第三方组织定义的类型，目前NFC Forum没有定义相关的数据类型。
 
## NFC Record实例
### URI Record Type实例
URI Record Type属于NFC Forum Well-known Type的一种，其对应的Type字段取值为"U"。对于这种类型的NFC Record，其Payload组织结构如表所示。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/56aa493c-7b2f-4a57-9731-26555556b22f)

在URI Record Payload中，第一个字节指明URI的ID码，表8-4为NFC Forum定义的几种ID码。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/c197ecd5-0e27-4afd-b707-f89939bb2c9b)


了解上述信息后，我们来看"http:/ http://www.nfc.com/"这样的信息该如何封装为一个NDEF消息，图8-7所示为NDEF消息各字段的取值情况。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/307b974c-fd89-462d-8d9c-19aa36338e03)


由于该NDEF消息只包含一个NFC Record，所以这个唯一的NFC Record将设置MB和ME标志位为1。另外，由于数据量小于255字节，所以SR标志位为1。最后，该Record携带的数据属于URI类型，它为Well-Known Type的一种，所以TNF取值为0x01。
Type Length字段取值为0x01，对应的Type字段取值为"U"，代表URI RecordType。
根据本节对URI Record的介绍，这种类型Record的Payload包含ID Code和data两个
部分。ID Code取值为0x01占据1字节（代表"http:/ www"），而data为"http://nfc.com/"占据7字节，所以整个Payload长度为8字节，故Payload length字段取值为0x08。
当应用程序获取Payload信息后，将根据ID Code和Data的取值最终计算出对应的URI为"http:/ http://www.nfc.com/"
Text Record Type实例
Text Record Type和URI Record Type类似，其Payload组织结构如表8-5所示。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/33436c90-92f8-4218-a771-76ff282d4874)

![image](https://github.com/justinlaw360/octopuscard/assets/4946026/933aaf46-e41f-4300-837a-2247c7ca2e23)

图所示为携带"Hello World"字符串信息的NDEF消息各字段的取值情况。可参考 URI Record进行解析。


### FeliCa cards
FeliCa cards normally respond to a poll for all System Codes, and polling for Service Codes in a System Code. However some older Octopus cards do not respond to this.
Metrodroid works around this by explicitly polling for Octopus' System Code and then presuming the Octopus Balance Service Code will also be present. This is also applied to first-generation SZT cards -- though we don't have any samples, we presume the bugs will be the same... :)

Card	System Code	Balance Service Code	
Octopus	0x0880
	0x0117
	
SZT (1st gen)	0x8005
	0x0118
	
Balance data (16 bytes)

First	Last	Length	Field description	
0	3	4	(Balance -350)/10	
4	13	10	unused	
14	15	2	unknown	


## Octopus_reader

### PN532 NFC Module
PN532是NXP公司推出的NFC控制器，基于80C51微控制器，可实现13.56 MHz的非接触式通信。此外，对MIFARE Classic 1K/MIFARE Classic 4K卡的支持允许双向传输速度高达424 kbit/s。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/ba532692-4973-48c9-984b-b547b95fcd68)

它带有40 Kb的ROM和1Kb的RAM，并且可以用于模拟ISO14443卡。 ISO/IEC 14443系列标准描述了用于国际交换的身份证或对象的参数。

PN532 NFC模块的主要特点：
●    基于具有40 KB的ROM和1 KB的RAM的80C51微控制器内核
●    高度集成的解调器和解码器
●    集成射频电平检测器
●    支持 ISO/IEC 14443A/MIFARE
●    支持 ISO/IEC 14443B（仅限读写器模式）
●    在读卡器/写卡器模式下工作距离可达50毫米，用于与ISO/IEC 14443A/MIFARE、ISO/IEC 14443B 或 FeliCa 卡通信
●    NFCIP-1 的工作距离可达50毫米，具体取决于天线尺寸、调谐和电源
●    ISO/IEC 14443A/MIFARE 或 FeliCa 卡仿真模式下的操作距离约为 100mm
●    可以使用外部模拟组件在 424 kbit/s 以上的RF接口上进行通信
●    专用主机中断
●    低功耗模式
●    可编程定时器
●    晶振
●    2.7 至 5.5 V 电源工作范围

通信模式的选择
PN532 NFC模块的一大优势是它可以使用不同的协议与Arduino进行通信，例如UART、I2C或SPI。 这些不同的协议使用微控制器的特定引脚和库。
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/79a14ac8-8230-45dd-9f20-b545295455fb)

要选择通信模式，必须使用拨码开关（0-Low，1-High）配置 PN532：

         SEL0	SEL1
UART       0   0
SPI        0   1
I2C        1   0

## PN532 Driver
This is an Arduino library for PN532 to use NFC technology.
https://github.com/elechouse/PN532/

For reading HK Octopus card, the memory buffer of wire.h and twi.h has to be changed 64 instead of the default value 32.  You should find these files in your Arduino library folder.
![image](https://github.com/justinlaw360/octopuscard/assets/4946026/a2abb428-5ec5-4da9-9457-ad580c67fb0d)

![image](https://github.com/justinlaw360/octopuscard/assets/4946026/a563e6fe-a99e-4de4-bd8b-8e48f9b8b6b1)


## Read Octopus Balance with Arduino Nano + PN532 NFC RFID module
Connection Diagram:

![image](https://github.com/justinlaw360/octopuscard/assets/4946026/2427f41a-ad67-4071-8675-72dc5d1cbc8b)

[![Watch the video]](https://github.com/justinlaw360/octopuscard/assets/4946026/2562f1cf-6a37-44a5-bd5b-61013cd5750f)


## Video demo
![image](https://github.com/justinlaw360/octopuscard/blob/main/demo.mp4)

