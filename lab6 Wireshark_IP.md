## Lab6 Wireshark_IP

- 学号:1813075
- 姓名:刘茵

1. Select the first ICMP Echo Request message sent by your computer, and expand the Internet Protocol part of the packet in the packet details window.What is the IP address of your computer? 

   ![image-20201209194938882](D:\software\Typora\iamge\image-20201209194938882.png)

  答：10.22.205.0

2. Within the IP packet header, what is the value in the upper layer protocol field?

   ![image-20201209195054355](D:\software\Typora\iamge\image-20201209195054355.png)

   答：上层协议是 ICMP，值是 1 

3. How many bytes are in the IP header? How many bytes are in the payload of the IP datagram? Explain how you determined the number of payload bytes.

   答：从2题图中可以看出 IP 头文件有 20bytes，IP 报的总长度是 56 个 byte，IP 数据长度 （ICMP 协议）就是 36bytes。

4. Has this IP datagram been fragmented? Explain how you determined whether or not the datagram has been fragmented.

   ![image-20201209195659666](D:\software\Typora\iamge\image-20201209195659666.png)

   ![image-20201209200732921](D:\software\Typora\iamge\image-20201209200732921.png)

   答：没有被分片，因为flags=0，fragment offset=0，R、DF、MF未设置

5. Which fields in the IP datagram always change from one datagram to the next within this series of ICMP messages sent by your computer?

   ![image-20201209200311398](D:\software\Typora\iamge\image-20201209200311398.png)

   ![image-20201209200407733](D:\software\Typora\iamge\image-20201209200407733.png)

   答：首部检验和、TTL、标识都在改变。

6. Which fields stay constant? Which of the fields must stay constant? Which fields must change? Why?

   ![image-20201209211326563](D:\software\Typora\iamge\image-20201209211326563.png)

   答：如图蓝色框是保持不变（下次可能改变），绿色框是一定不会改变的（仅指路 由跟踪），红色框是必须改变的。

   必须更改是每次路由跟踪（含有多个不同 TTL 的 PING）的序列号，校验值，以 及每个 PING 的 TTL。注意每次 PING 也有序列号，校验值，因此数据是一定改变的 （上文说过）。 

   保持不变（下次可能改变）的是你这次路由跟踪，有很多的 PING 的目标数据 长度，目标和本地 IP，可选选项，显式拥塞通告(来自维基百科)，标识符，偏移量 这些字段。 但你下次路由跟踪可能会改变目标 IP 和本地 IP，你也会打开一些 IP 的选项， 改变路由跟踪的数据报的大小，造成分片有偏移量这种情况。当然这种情况也可能 不会发生。 

   必须保持的不变的，也就是我们使用 IPV4 的下的路由跟踪，这些协议和版本都 是定死的，你不管什么时候路由跟踪都是这样，所以不会变，因为区分服务已经弃 用，所以也是不会变。

7. Describe the pattern you see in the values in the Identification field of the IP datagram

   答：标识依次增加，如题5图。

8. What is the value in the Identification field and the TTL field?

   ![image-20201209201105414](D:\software\Typora\iamge\image-20201209201105414.png)

   答：TTL:255

   Identification：23912

9. Do these values remain unchanged for all of the ICMP TTL-exceeded replies sent to your computer by the nearest (first hop) router? Why?

   ![image-20201209201721955](D:\software\Typora\iamge\image-20201209201721955.png)

   答：TTL没有改变，因为每一个的路由器都有一个固定的TTL值，ID改变了。（和题8的图对比）

10. Find the first ICMP Echo Request message that was sent by your computer after you changed the Packet Size in pingplotter to be 2000. Has that message been fragmented across more than one IP datagram? 

    ![image-20201209202434254](D:\software\Typora\iamge\image-20201209202434254.png)

    答：分为两段

11. Print out the first fragment of the fragmented IP datagram. What information in the IP header indicates that the datagram been fragmented? What information in the IP header indicates whether this is the first fragment versus a latter fragment? How long is this IP datagram?

    ![image-20201209203607899](D:\software\Typora\iamge\image-20201209203607899.png)

    答：MF为 set 标识还有分片，DF为not set可以分片。offset片偏移为0标识这是初始的ip片。

    这个数据报的长度：1500bytes

12. Print out the second fragment of the fragmented IP datagram. What information in the IP header indicates that this is not the first datagram fragment? Are the more fragments? How can you tell?

    ![image-20201209203658869](D:\software\Typora\iamge\image-20201209203658869.png)

    答：Offset为1480表示不为第一个分片，已经有了偏移量。

    ​		MF为0表示为最后一个分片。

13. What fields change in the IP header between the first and second fragment? Now find the first ICMP Echo Request message that was sent by your computer after you changed the Packet Size in pingplotter to be 3500.

    答：Flags, Header checksum，Totol length（参考10，11题图）

14. How many fragments were created from the original datagram?

    ![image-20201209204648026](D:\software\Typora\iamge\image-20201209204648026.png)

    答：3个

15. What fields change in the IP header among the fragments?

    答：Flags, Header checksum，Totol length