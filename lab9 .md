## Lab9 Wireshark_ Ethernet and ARP

- 学号:1813075
- 姓名:刘茵

---

1. What is the 48-bit Ethernet address of your computer?

   ![image-20201230185216414](D:\software\Typora\iamge\image-20201230185216414.png)

   ![image-20201230185459815](D:\software\Typora\iamge\image-20201230185459815.png)

   答：地址为00:d0:59:a9:3d:68

2. What is the 48-bit destination address in the Ethernet frame? Is this the Ethernet address of gaia.cs.umass.edu? (Hint: the answer is no). What device has this as its Ethernet address? [Note: this is an important question, and one that students sometimes get wrong. Re-read pages 468-469 in the text and make sure you understand the answer here.]

   ![image-20201230185551278](D:\software\Typora\iamge\image-20201230185551278.png)

   答：目的地址：00:06:25:da:af:73，不是gaia.cs.umass.edu的以太网地址。拥有这个以太网地址的设备是作者的路由器的地址。

3. Give the hexadecimal value for the two-byte Frame type field. What upper layer protocol does this correspond to?

   ![image-20201230185813059](D:\software\Typora\iamge\image-20201230185813059.png)

   答：十六进制数值：0x0800。代表上层协议是 IPV4

4. How many bytes from the very start of the Ethernet frame does the ASCII “G” in “GET” appear in the Ethernet frame?

   ![image-20201230190607230](D:\software\Typora\iamge\image-20201230190607230.png)

   答：有 16 × 3 + 7 = 55 Byte（包含G）

5. What is the value of the Ethernet source address? Is this the address of your computer, or of gaia.cs.umass.edu (Hint: the answer is no). What device has this as its Ethernet address?

   ![image-20201230190941548](D:\software\Typora\iamge\image-20201230190941548.png)

   答：源地址：00:06:25:da:af:73，这个应该是作者的路由器的地址。

6. What is the destination address in the Ethernet frame? Is this the Ethernet address of your computer?

   ![image-20201230191049639](D:\software\Typora\iamge\image-20201230191049639.png)

   答：目的地址：00:d0:59:a9:3d:68，这个是计算机的以太网地址。

7. Give the hexadecimal value for the two-byte Frame type field. What upper layer protocol does this correspond to?

   ![image-20201230191126465](D:\software\Typora\iamge\image-20201230191126465.png)

   答：十六进制数值：0x0800。代表上层协议是 IPV4

8. How many bytes from the very start of the Ethernet frame does the ASCII “O” in “OK” (i.e., the HTTP response code) appear in the Ethernet frame?

   ![image-20201230191227025](D:\software\Typora\iamge\image-20201230191227025.png)

   答：有 16 × 4 + 4 = 68 Byte（包含O）

9. Write down the contents of your computer’s ARP cache. What is the meaning of each column value?

   ![image-20201230192251097](D:\software\Typora\iamge\image-20201230192251097.png)

   答：红色：网卡

   绿色：路由IP和MAC地址

   浅蓝色：广播地址

   紫色：组播地址（使用）

   深蓝色：组播地址（管理）

10. What are the hexadecimal values for the source and destination addresses in the Ethernet frame containing the ARP request message?![image-20201230192631619](D:\software\Typora\iamge\image-20201230192631619.png)

    答：源地址：00:d0:59:a9:3d:68

    ​       目的地址：ff:ff:ff:ff:ff:ff

11. Give the hexadecimal value for the two-byte Ethernet Frame type field. What upper layer protocol does this correspond to?

    ![image-20201230192646069](D:\software\Typora\iamge\image-20201230192646069.png)

    答：0x0806，表示上层协议是 ARP。

12. Download the ARP specification from
    ftp://ftp.rfc-editor.org/in-notes/std/std37.txt. A readable, detailed discussion of ARP is also at http://www.erg.abdn.ac.uk/users/gorry/course/inet-pages/arp.html.
    a) How many bytes from the very beginning of the Ethernet frame does the ARP opcode field begin?

    ![image-20201230192834819](D:\software\Typora\iamge\image-20201230192834819.png)

    答：20字节（不包含）21字节（包含第一个）

    b) What is the value of the opcode field within the ARP-payload part of the Ethernet frame in which an ARP request is made?

    答：操作码的值为 1。

    c) Does the ARP message contain the IP address of the sender?

    ![image-20201230193106931](D:\software\Typora\iamge\image-20201230193106931.png)

    答：ARP 消息包含发送方的 IP 地址。

    d) Where in the ARP request does the “question” appear – the Ethernet address of the machine whose corresponding IP address is being queried?

    ![image-20201230193218516](D:\software\Typora\iamge\image-20201230193218516.png)

    答：Target IP address

13. Now find the ARP reply that was sent in response to the ARP request.
    a) How many bytes from the very beginning of the Ethernet frame does the ARP opcode field begin?

    ![image-20201230193336136](D:\software\Typora\iamge\image-20201230193336136.png)

    答：20字节（不包含）21字节（包含第一个）

    b) What is the value of the opcode field within the ARP-payload part of the Ethernet frame in which an ARP response is made?

    答：操作码的值为 2。

    c) Where in the ARP message does the “answer” to the earlier ARP request appear – the IP address of the machine having the Ethernet address whose corresponding IP address is being queried?

    ![image-20201230193808579](D:\software\Typora\iamge\image-20201230193808579.png)

    答：发送方IP地址和发送方MAC地址

14. What are the hexadecimal values for the source and destination addresses in the Ethernet frame containing the ARP reply message?

    ![image-20201230194113520](D:\software\Typora\iamge\image-20201230194113520.png)

    答：源地址：00:06:25:da:af:73  

    ​       目的地址：00:d0:59:a9:3d:68 

15. Open the ethernet-ethereal-trace-1 trace file in
    http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip. The first and second ARP packets in this trace correspond to an ARP request sent by the computer running Wireshark, and the ARP reply sent to the computer running Wireshark by the computer with the ARP-requested Ethernet address. But there is yet another computer on this network, as indicated by packet 6 – another ARP request. Why is there no ARP reply (sent in response to the ARP request in packet 6) in the packet trace?

    答：因为 ARP 广播信息是广播的，所有该网段内所有的电脑均可收到，而 ARP 广播回 复是单播的，只有请求的那台电脑才能收到，因此抓不到另外一台电脑的 ARP 请求。