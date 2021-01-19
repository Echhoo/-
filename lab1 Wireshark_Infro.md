## lab1 Wireshark_Infro 

- 学号:1813075
- 姓名:刘茵

### 1.Getting Wireshark

[wireshark官网](http://www.wireshark.org/download.html)获取wireshark软件。

### 2.Running Wireshark

<img src="D:\software\Typora\iamge\image-20201111184122407.png" alt="运行界面" style="zoom:60%;" align="left" />

### 3.Taking Wireshark for a Test Run

<img src="D:\software\Typora\iamge\image-20201111191730190.png" alt="http抓包" style="zoom:60%;" align="left" />

### 4.回答以下问题：

1. List 3 different protocols that appear in the protocol column in the unfiltered packet-listing window in step 7 above. 

​       答：DHCP协议 | HTTP协议 | TCP协议

2. How long did it take from when the HTTP GET message was sent until the HTTP OK reply was received? (By default, the value of the Time column in the packetlisting window is the amount of time, in seconds, since Wireshark tracing began. To display the Time field in time-of-day format, select the Wireshark View pull down menu, then select Time Display Format, then select Time-of-day.)

​        答：需要0.275670秒

3. What is the Internet address of the gaia.cs.umass.edu (also known as wwwnet.cs.umass.edu)? What is the Internet address of your computer?

​       答：the Internet address of my computer 10.22.80.131

​		       the Internet address of the gaia.cs.umass.edu 128.119.245.12



4. Print the two HTTP messages (GET and OK) referred to in question 2 above. To do so, select Print from the Wireshark File command menu, and select the “Selected Packet Only” and “Print as displayed” radial buttons, and then click OK.

   答:
   
   - GET消息：
   
   <img src="D:\software\Typora\iamge\image-20201111202023908.png" alt="image-20201111202023908" style="zoom:80%;" align = "left "/>
   
   - OK消息：
   
   <img src="D:\software\Typora\iamge\image-20201111202213644.png" alt="image-20201111202213644" style="zoom:80%;" align="left"/>