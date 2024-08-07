---
title: 'Computer Networks ： A Systems Approach(chapter 2 : 2.2 encoding)'
date: 2024-07-01 23:27:20
tags:
- 计算机网络
categories: 
- code 
---



最近在看 [《Computer Networks ： A Systems Approach》](https://book.systemsapproach.org/index.html)这本书，感觉前边讲的都还蛮通俗易懂的，但第二章第二节 [Encoding](https://book.systemsapproach.org/direct/encoding.html#) 感觉看的不是很懂，于是研究了一下这里做个总结。

这一章主要讲了怎么将二进制信息进行重新编码从而在更好的在物理层使用电磁波进行传输。

举个例子，我们现在要传输 bit序列 0010111101000010



### NRZ

按照NRZ （不归零码）方式进行传输，即如下图所示将数据值 1 映射到高信号，将数据值 0 映射到低信号。

![image-20240705121119337](https://raw.githubusercontent.com/akaakking/pic/master/image-20240705121119337.png)

这是比较容易想到的映射方式，但是这种方式在实际传输的时候会造成两种问题即基线漂移和时钟漂移。

先来说说基线漂移，接收方在接受信号的时候，会根据接受到的连续的高低电平计算一个电平的平均值，这个平均值就是基线，显著高于基线的电平会被认为是高电平，同样显著低于基线的电平会被认为是低电平。那么当接受到连续的低电平的，或者连续的高电平的时候，这个基线就会偏大或偏小，那么就可能导致电平的误判，这个就叫基线漂移。了解了基线漂移，我们很自然的就可以想到解决基线漂移问题的思路。即减少连续的高低电平。

说完基线漂移再来说说时钟漂移，我们知道电平的跳变是由时钟控制的，因而我们需要一种机制，让接收方和发送方之间的时钟频率保持一致，我们采用使用自适应算法来动态调整接收方的时钟频率，但是如果发送方持续发送高电平或低电平，接收方的自适应算法可能会受到干扰。这是因为自适应算法通常依赖于跳变频率来调整时钟，而连续电平不会提供足够的变化来进行准确的调整。因此会出现发送/接受 时钟频率不一致的情况。

### NRZI

NRZI 不归零反转，即在编码0时电平不变，在编码1时发生电平的跳变，这显然解决了连续1的问题但是对于连续0的问题没有解决，反而还降低了编码效率

![image-20240705165156127](https://raw.githubusercontent.com/akaakking/pic/master/image-20240705165156127.png)

### 曼彻斯特

向一个时钟周期后，向上跳变为0,向下跳变为1。也可以理解为 前低后高为0,前高后低为1。

![image-20240705165156127](https://raw.githubusercontent.com/akaakking/pic/master/image-20240705165156127.png)

### 差分曼彻斯特

![img](https://bkimg.cdn.bcebos.com/pic/54fbb2fb43166d2230048e764d2309f79152d2e5?x-bce-process=image/format,f_auto/resize,m_lfit,limit_1,w_416)

数字为1,则在临界不跳变，否则跳变，相对于曼彻斯特编码，差分曼彻斯特的好处是变化较少适合传输高速信息，但是曼彻斯特和差分曼彻斯特码编码效率都为50%左右

### 4B/5B

可以简单理解为利用 一个映射表，将4个比特表示为5个比特。这样的话编码效率为80%

我们只要保证

每个5bit码组中不多于3个"0"且5bit码组中不少于2个"1"

即可满足跳变比较频繁的要求。
