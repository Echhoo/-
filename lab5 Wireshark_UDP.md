## Lab5 Wireshark_UDP

- 学号:1813075
- 姓名:刘茵

1. Select one UDP packet from your trace. From this packet, determine how many fields there are in the UDP header. (You shouldn’t look in the textbook! Answer these questions directly from what you observe in the packet trace.) Name these fields. 

   ![image-20201203173344744](D:\software\Typora\iamge\image-20201203173344744.png)

   答：四部分。   

   **Source Port**：源端口号
   **Destination Port**：目的端口号
   **Length**：长度
   **Checksum**：校验和

2. By consulting the displayed information in Wireshark’s packet content field for this packet, determine the length (in bytes) of each of the UDP header fields. 

   <img src="D:\software\Typora\iamge\image-20201203173906375.png" alt="image-20201203173906375"  align="left"/>

   答: 8个字节
   
3. The value in the Length field is the length of what? (You can consult the text for this answer). Verify your claim with your captured UDP packet. 

   <img src="D:\software\Typora\iamge\image-20201203174317400.png" alt="image-20201203174317400" align="left" />

   答：Length 包含 UDP 报文头和 UDP 数据长度。

   UDP 头长度是 8 字节，UDP 数据是 50 字节，Length为 58 字节。

4. What is the maximum number of bytes that can be included in a UDP payload?
    (Hint: the answer to this question can be determined by your answer to 2. above)
    答：有效负载就是可变长度的数据部分。由于 Length 字段占 2byte = 65536 bit，并且其中 8 byte 是 UDP 首部信息。因此有效载荷 = 2^16-1-8=65527bytes

5. What is the largest possible source port number? (Hint: see the hint in 4.)
    答：65535

6. What is the protocol number for UDP? Give your answer in both hexadecimal and decimal notation. To answer this question, you’ll need to look into the Protocol field of the IP datagram containing this UDP segment (see Figure 4.13 in the text, and the discussion of IP header fields).

      ![image-20201203174642790](D:\software\Typora\iamge\image-20201203174642790.png)

    <img src="D:\software\Typora\iamge\image-20201203174706664.png" alt="image-20201203174706664" style="zoom:80%;" align="left"/>

      答： ANS:UDP 协议号是 17（10 进制），16 进制 0x11

7. Examine a pair of UDP packets in which your host sends the first UDP packet and the second UDP packet is a reply to this first UDP packet. (Hint: for a second packet to be sent in response to a first packet, the sender of the first packet should be the destination of the second packet). Describe the relationship between the port numbers in the two packets.
    ![image-20201203174855856](D:\software\Typora\iamge\image-20201203174855856.png)
    
    ![image-20201203174924518](D:\software\Typora\iamge\image-20201203174924518.png)
    
    答：发送者发送端口号在接收返回UDP 时候会变成接收端口号。 

    ​       接收者发送返回UDP 时候接受端口号会变成发送端口号。