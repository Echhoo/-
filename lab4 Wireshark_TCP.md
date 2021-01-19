## lab4 Wireshark_TCP 

- 学号:1813075
- 姓名:刘茵

### 1. Capturing a bulk TCP transfer from your computer to a remote server.

### 2. A first look at the captured trace
1. What is the IP address and TCP port number used by the client computer (source) that is transferring the file to gaia.cs.umass.edu? To answer this question, it’s probably easiest to select an HTTP message and explore the details of the TCP packet used to carry this HTTP message, using the “details of the selected packet header window” (refer to Figure 2 in the “Getting Started with Wireshark” Lab if you’re uncertain about the Wireshark windows.

   ![image-20201203145434025](D:\software\Typora\iamge\image-20201203145434025.png)

   答：IP地址：192.168.1.102

   ​		TCP发送端口号：1161
   
2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending
and receiving TCP segments for this connection?
   答：IP地址：128.119.245.12

   ​		TCP接收端口号：80
   
3. What is the IP address and TCP port number used by your client computer (source) to transfer the file to gaia.cs.umass.edu? 

   ![image-20201203151426703](D:\software\Typora\iamge\image-20201203151426703.png)

   答：IP地址：10.41.213.197

   ​		TCP发送端口号：56749
   
### 3. TCP Basics

（用官方文档）

4. What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? What is it  in the segment that identifies the segment as a SYN segment?

   ![image-20201209232731645](D:\software\Typora\iamge\image-20201209232731645.png)

   答：SYN=1 seq=0（相对序列号） SYN报文负责建立连接，选择客户端初始的序列号.

5. What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is the value of the Acknowledgement field in the SYNACK segment? How did gaia.cs.umass.edu determine that value? What is it in the segment that identifies the segment as a SYNACK segment?

   ![image-20201209233015536](D:\software\Typora\iamge\image-20201209233015536.png)

   答：seq=0 Acknowledgment=1 Acknowledgment=X（SYN中的seq）+1，确认客户端的连接，选择服务器端初始的序列号。

6. What is the sequence number of the TCP segment containing the HTTP POST command? Note that in order to find the POST command, you’ll need to dig into the packet content field at the bottom of the Wireshark window, looking for a segment with a “POST” within its DATA field.

   ![image-20201209233159723](D:\software\Typora\iamge\image-20201209233159723.png)

   答：seq= 1 PSH 标志表示有数据传输。

7. 答:前六个TCP报文的具体信息：

   EstimatedRTT = (1 - a) × EstimatedRTT + a × SampleRTT

   | 计数 | 序列号 | 发送时间 | ACK时间  | RTT值    | EstimatedRTT值      |
   | ---- | ------ | -------- | -------- | -------- | ------------------- |
   | 1    | 1      | 0.026477 | 0.053937 | 0.02746‬  | 0.02746             |
   | 2    | 566    | 0.041737 | 0.077294 | 0.035557‬ | 0.028472125         |
   | 3    | 2026   | 0.054026 | 0.124085 | 0.070059‬‬ | 0.033670484375      |
   | 4    | 3486   | 0.054690 | 0.169118 | 0.114428‬‬ | 0.043765173828125   |
   | 5    | 4046   | 0.077405 | 0.217299 | 0.139894‬‬ | 0.05578127709960937 |
   | 6    | 6406   | 0.078157 | 0.267802 | 0.189645‬‬ | 0.07251424246215821 |

   ![image-20201210001429316](D:\software\Typora\iamge\image-20201210001429316.png)

8. What is the length of each of the first six TCP segments?

    答： 前6个TCP报文的长度分别为：565，1460，1460，1460，1460，1460

9. What is the minimum amount of available buffer space advertised at the received for the entire trace? Does the lack of receiver buffer space ever throttle the sender?

    答：

    对于服务器而言，收到的最小可用缓冲区空间量为 6780。

    ![image-20201210001608096](D:\software\Typora\iamge\image-20201210001608096.png) 

    对于主机而言，收到的最小可用缓冲区空间量为 5840。

    ![image-20201210001655836](D:\software\Typora\iamge\image-20201210001655836.png)缺少接收器缓冲区空间会限制发送方传送 TCP 区段，这是因为 TCP 的**流量控制服务**，能够消除发送方使接收方缓存溢出的可能性，使得发送方的发送速率与接收方应用程序的读取速率相匹配。实现的方式是**滑动窗口协议**。

10. Are there any retransmitted segments in the trace file? What did you check for (in the trace) in order to answer this question?

    ![image-20201210000242165](D:\software\Typora\iamge\image-20201210000242165.png)

    答： 没有重传报文。在过滤器中输入ip.src==192.168.1.102，发现序列号一直在增加。

11. How much data does the receiver typically acknowledge in an ACK? Can you identify cases where the receiver is ACKing every other received segment

     ![image-20201209235831751](D:\software\Typora\iamge\image-20201209235831751.png)

     答：一般都是1460。

     64005-61085=2920=1460*2.接收方收到一个报文即发送一个ACK，没有报多个确认合并，可以确认，根据 ACK 序列号的顺序来推测。

12. What is the throughput (bytes transferred per unit time) for the TCP connection? Explain how you calculated this value.

     **平均吞吐量 = 传输数据的比特数 F ÷ 接收方接收所有数据所用时间 T**

     答:数据量：164091-1 = 164090 bytes

     时间：5.455830-0.026477 = 5.4294

     结果：164090/5.4294 = 30.222Kbytes/sec