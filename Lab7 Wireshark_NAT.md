## Lab7 Wireshark_NAT

- 学号:1813075
- 姓名:刘茵

1. What is the IP address of the client?

   ![image-20201216190755035](D:\software\Typora\iamge\image-20201216190755035.png)
   
   答：192.168.1.100
   
2. The client actually communicates with several different Google servers in order to implement “safe browsing.” (See extra credit section at the end of this lab). The main Google server that will serve up the main Google web page has IP address 64.233.169.104. In order to display only those frames containing HTTP messages that are sent to/from this Google, server, enter the expression “http && ip.addr == 64.233.169.104” (without quotes) into the Filter: field in Wireshark . 
   答：![image-20201216190916560](D:\software\Typora\iamge\image-20201216190916560.png)

3. Consider now the HTTP GET sent from the client to the Google server (whose IP address is IP address 64.233.169.104) at time 7.109267. What are the source and destination IP addresses and TCP source and destination ports on the IP datagram carrying this HTTP GET? 

   ![image-20201216191027994](D:\software\Typora\iamge\image-20201216191027994.png)

   答：源IP：192.168.1.100 端口：4335

   ​	   目的IP：64.233.169.104 端口：80

4. At what time4 is the corresponding 200 OK HTTP message received from the Google server? What are the source and destination IP addresses and TCP source and destination ports on the IP datagram carrying this HTTP 200 OK message? 

   ![image-20201216191322592](D:\software\Typora\iamge\image-20201216191322592.png)

   答：时间：7.158797

   ​	   源IP：64.233.169.104 端口：80

   ​	   目的IP：192.168.1.100 端口：4335

5. Recall that before a GET command can be sent to an HTTP server, TCP must first set up a connection using the three-way SYN/ACK handshake. At what time is the client-to-server TCP SYN segment sent that sets up the connection used by the GET sent at time 7.109267? What are the source and destination IP addresses and source and destination ports for the TCP SYN segment? What are the source and destination IP addresses and source and destination ports of the ACK sent in response to the SYN. At what time is this ACK received at the client? (Note: to find these segments you will need to clear the Filter expression you entered above in step 2. If you enter the filter “tcp”, only TCP segments will be displayed by Wireshark).

   ![image-20201216191916048](D:\software\Typora\iamge\image-20201216191916048.png)

   答：SYN 报文：

   ​	   发送时间：7.075657 s 

   ​	   源IP: 192.168.1.100 端口: 4335 

   ​	   目的IP：64.233.169.104 端口:80 

   ​	   SYN ACK 报文： 

   ​	   收到时间：7.108986 s 

   ​	   源IP：64.233.169.104 端口：80 

   ​	   目的IP：192.168.1.100 端口：4335 

6. In the NAT_ISP_side trace file, find the HTTP GET message was sent from the client to the Google server at time 7.109267 (where t=7.109267 is time at which this was sent as recorded in the NAT_home_side trace file). At what time does this message appear in the NAT_ISP_side trace file? What are the source and destination IP addresses and TCP source and destination ports on the IP datagram carrying this HTTP GET (as recording in the NAT_ISP_side trace file)? Which of these fields are the same, and which are different, than in your answer to question 3 above?![image-20201216192318454](D:\software\Typora\iamge\image-20201216192318454.png)
   
    答：出现时间：6.069168 s
  
    ​	   源IP：71.192.34.104 端口：4335 
  
    ​	   目的IP：64.233.169.104 端口：80 
  
    ​	   目的地址和端口相同，源地址不同。
  
7. Are any fields in the HTTP GET message changed? Which of the following fields in the IP datagram carrying the HTTP GET are changed: Version, Header Length, Flags, Checksum. If any of these fields have changed, give a reason (in one sentence) stating why this field needed to change.

     ![image-20201216193048144](D:\software\Typora\iamge\image-20201216193048144.png)

     ![image-20201216193330744](D:\software\Typora\iamge\image-20201216193330744.png)

       答：HTTP消息没有更改。
          	IP数据报中的源IP地址、校验和、TTL发生改变。

8. In the NAT_ISP_side trace file, at what time is the first 200 OK HTTP message received from the Google server? What are the source and destination IP addresses and TCP source and destination ports on the IP datagram carrying this HTTP 200 OK message? Which of these fields are the same, and which are different than your answer to question 4 above?

   ![image-20201216194144600](D:\software\Typora\iamge\image-20201216194144600.png)

   答：时间：6.117570

   ​	   源IP：64.233.169.104 端口：80

   ​	   目的IP：71.192.34.104 端口：4335

   ​	   源地址和端口相同，目的地址不同。

9. In the NAT_ISP_side trace file, at what time were the client-to-server TCP SYN segment and the server-to-client TCP ACK segment corresponding to the segments in question 5 above captured? What are the source and destination IP addresses and source and destination ports for these two segments? Which of these fields are the same, and which are different than your answer to question 5 above?

     ![image-20201216194545582](D:\software\Typora\iamge\image-20201216194545582.png)
     
     答：SYN 报文：
     
     ​	   发送时间：6.035475 s 
     
     ​	   源IP: 71.192.34.104 端口: 4335 
     
     ​	   目的IP：64.233.169.104 端口:80 
     
     ​	   SYN ACK 报文： 
     
     ​	   收到时间：6.06775 s  
     
     ​	   源IP：64.233.169.104 端口：80 
     
     ​	   目的IP：71.192.34.104 端口：4335 
     
     ​	   SYN的源目的IP不同，SYN ACK的目的IP不同。
     
10.    Using your answers to 1-8 above, fill in the NAT translation table entries for HTTP connection considered in questions 1-8 above

     答：

     |      | WAN side      | LAN side      |
     | ---- | ------------- | ------------- |
     | IP   | 71.192.34.104 | 192.168.1.100 |
     | PORT | 4355          | 4355          |

     

