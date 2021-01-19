## lab1 Web Server 编程作业

- 学号:1813075
- 姓名:刘茵

#### 1. Complete the skeleton code

#### 2. Run Code 

Put an HTML file (e.g., HelloWorld.html) in the same directory that the server is in. Run the server program. Determine the IP address of the host that is running the server (e.g., 128.238.251.26). From another host, open a browser and provide the corresponding URL. For example:

   http://localhost:9000/Web_server.html

#### 3. Require
You will hand in the complete server code along with the screen shots of your client browser

1. complete server code:

   ```python
   # import socket module
   from socket import *
   import sys  # In order to terminate the program
   
   serverSocket = socket(AF_INET, SOCK_STREAM)
   # Prepare a sever socket
   # Fill in start
   HOST = ''
   PORT = 9000
   BUFSIZ = 1024
   ADDRESS = (HOST, PORT)
   serverSocket.bind(ADDRESS)  # 绑定ADDRESS
   serverSocket.listen(1)
   # Fill in end
   while True:
       # Establish the connection
       print('Ready to serve...')
       connectionSocket, addr = serverSocket.accept()  # Fill in
       print('Connected by', addr)
       try:
           message = connectionSocket.recv(BUFSIZ)  # Fill in start          #Fill in end
           print(message.split()[0], ':', message.split()[1])
           filename = message.split()[1]
           print(filename[1:])
           f = open(filename[1:],encoding='utf-8')
           outputdata = f.read()  # Fill in start       #Fill in end
           # Send one HTTP header line into socket
           # Fill in start
           data = 'HTTP/1.1 200 OK\r\n\r\n'
           connectionSocket.send(data.encode('utf-8'))
           # Fill in end
           # Send the content of the requested file to the client
           for i in range(0, len(outputdata)):
               connectionSocket.send(outputdata[i].encode('utf-8'))
           connectionSocket.send("\r\n".encode('utf-8'))
   
           connectionSocket.close()
       except IOError:
           # Send response message for file not found
           # Fill in start
           data = '404 Not Found\r\n'
           print('No file')
           connectionSocket.send(data.encode('utf-8'))
           # Fill in end
           # Close client socket
           # Fill in start
           connectionSocket.close()
           # Fill in end
serverSocket.close()
   sys.exit()  # Terminate the program after sending the corresponding data

   ```

   2. output

      - 失败

        <img src="D:\software\Typora\iamge\image-20201201135507286.png" alt="image-20201201135507286" style="zoom:67%;" align= "left"/>
        
        <img src="D:\software\Typora\iamge\image-20201201140301165.png" alt="image-20201201140301165" style="zoom:67%;" align="left"/>

      - 成功
   
        ![image-20201201143452358](D:\software\Typora\iamge\image-20201201143452358.png)
      
        右下角返回200
        
        <img src="D:\software\Typora\iamge\image-20201201143819362.png" alt="image-20201201143819362" style="zoom:67%;" align="left"/>
        
        