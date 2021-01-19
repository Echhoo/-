## lab3 Wireshark_DNS

- 学号：1813075 

- 姓名：刘茵

  ---

### 1.nslookup

问题：

1. Run nslookup to obtain the IP address of a Web server in Asia. What is the IP address of that server?

   答：

    ```
   服务器:  baidu.com
   Addresses:  39.156.69.79
             220.181.38.148
   
   DNS request timed out.
       timeout was 2 seconds.
   DNS request timed out.
       timeout was 2 seconds.
   *** 请求 baidu.com 超时
    ```

   服务器的IP地址为 39.156.69.79和 220.181.38.148

2. Run nslookup to determine the authoritative DNS servers for a university in Europe. 

3. Run nslookup so that one of the DNS servers obtained in Question 2 is queried for the mail servers for Yahoo! mail. What is its IP address?
   [注]：2.3电脑链接失败，且网上没有找到对应的解决办法。

### 2.ipconfig

No questions

### 3.Tracing DNS with Wireshark

问题：

4. Locate the DNS query and response messages. Are then sent over UDP or TCP? 

   <img src="D:\software\Typora\iamge\image-20201114170245289.png" alt="image-20201114170245289" style="zoom:67%;" align= "lef"/>
   答：是UDP

5. What is the destination port for the DNS query message? What is the source port of DNS response message? 

   <img src="D:\software\Typora\iamge\image-20201114170438627.png" alt="image-20201114170438627" style="zoom:67%;" align ="left" />![image-20201114170616215](D:\software\Typora\iamge\image-20201114170616215.png)

   <img src="D:\software\Typora\iamge\image-20201114170438627.png" alt="image-20201114170438627" style="zoom:67%;" align ="left" />![image-20201114170616215](D:\software\Typora\iamge\image-20201114170616215.png)

   答：端口号都是53

6. To what IP address is the DNS query message sent? Use ipconfig to determine the IP address of your local DNS server. Are these two IP addresses the same? 

   <img src="D:\software\Typora\iamge\image-20201114170818925.png" alt="image-20201114170818925" style="zoom:67%;" align="left"/>

   答：Destination IP与本地DNS IP相同，都是222.30.45.41

7. Examine the DNS query message. What “Type” of DNS query is it? Does the query message contain any “answers”? 

   <img src="D:\software\Typora\iamge\image-20201114220316672.png" alt="image-20201114220316672" style="zoom:67%;" align="left"/>

   答：type is A ，no answers.

8. Examine the DNS response message. How many “answers” are provided? What do each of these answers contain?

   <img src="D:\software\Typora\iamge\image-20201114221629367.png" alt="image-20201114221629367" style="zoom:67%;" align="left"/>

   答：包含了三个answers。

   ​		第一个type为CNAME，指明了www.ietf.org的另一个域名 www.ieft.org.cdn.cloudflare.net，是由国外 CDN 厂商 Cloudflare 提供的规范 CNAME 的 CDN 加 速（type=cname）地址

   ​		第二个和第三个type为A，class为in，ipv4是104.16.44.99/104.16.45.99

9. Consider the subsequent TCP SYN packet sent by your host. Does the destination IP address of the SYN packet correspond to any of the IP addresses provided in the DNS response message? 

   答：是对应的

10. This web page contains images. Before retrieving each image, does your host issue new DNS queries?

    答：并没有，因为本机 DNS 已经被缓存了，因此不需要发起新的 DNS 查询。

11. What is the destination port for the DNS query message? What is the source port of DNS response message?

    <img src="D:\software\Typora\iamge\image-20201114223320787.png" style="zoom:67%;" align="left"/>
    
    <img src="D:\software\Typora\iamge\image-20201114223408078.png" style="zoom:67%;" align="left"/>
    
    答：端口号都为53。
    
12. To what IP address is the DNS query message sent? Is this the IP address of your default local DNS server?
	
	答：202.113.16.41，是本地默认DNS服务器的IP。
	
13. Examine the DNS query message. What “Type” of DNS query is it? Does the query message contain any “answers”?
	答：Type:A no "answers".
	
14. Examine the DNS response message. How many “answers” are provided? What do each of these answers contain?

    <img src="D:\software\Typora\iamge\image-20201114224458900.png" alt="image-20201114224458900" style="zoom:67%;" align="left"/>

    答：提供了三个answer，包括两个规范主机地址（type=cname），一个规范主机地址指向 IPV4(type=a)

15. Provide a screenshot

    <img src="D:\software\Typora\iamge\image-20201114224704685.png" alt="image-20201114224704685" style="zoom:67%;" align="left"/>

16. To what IP address is the DNS query message sent? Is this the IP address of your default local DNS server?

    答：<使用给定数据包不确定>，但按照报文格式应该是作者的本地默认DNS服务器的IP地址

17. Examine the DNS query message. What “Type” of DNS query is it? Does the query message contain any “answers”?
    答：Type NS 表示查询**权威 DNS 服务器** 查询消息不包含任何"answers"

18. Examine the DNS response message. What MIT nameservers does the response message provide? Does this response message also provide the IP addresses of the MIT namesers?
    答：响应消息没提供 MIT 的域名的 IP 地址。

    <img src="D:\software\Typora\iamge\image-20201114231008763.png" alt="image-20201114231008763" style="zoom:67%;" align="left"/>

19. Provide a screenshot.

    <img src="D:\software\Typora\iamge\image-20201114231111456.png" alt="image-20201114231111456" style="zoom:67%;" align="left"/>

20. To what IP address is the DNS query message sent? Is this the IP address of your default local DNS server? If not, what does the IP address correspond to?

    <img src="D:\software\Typora\iamge\image-20201114231302412.png" alt="image-20201114231302412" style="zoom:67%;" align="left"/>

    答：不是

21. Examine the DNS query message. What “Type” of DNS query is it? Does the query message contain any “answers”?

    答：Type 为 “A”，表示查询 IP 地址，没有任何 "answers"。

    ![image-20201123191158169](D:\software\Typora\iamge\image-20201123191158169.png)

22. Examine the DNS response message. How many “answers” are provided? What does each of these answers contain?

    <img src="D:\software\Typora\iamge\image-20201114231505228.png" alt="image-20201114231505228" style="zoom:67%;" align="left"/>

    答：提供了一个“answers”，为该域名的ip地址。

23. Provide a screens

    <img src="D:\software\Typora\iamge\image-20201114231359568.png" alt="image-20201114231359568" style="zoom:67%;" align="left"/>

    