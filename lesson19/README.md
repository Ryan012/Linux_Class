# TCP编程总结
## 一、服务器端
1. 首先建立一个套接字，使用socket函数，它的作用只是建立了套接字类型，并没有与具体的端口产生关系，所以不能使用。
2. 要想使用就必须将具体的IP地址与端口绑定，使用bind函数
3. 在实际的端口号上进行侦听，就是看有没有连接请求。如果有连接请求说明有一个客户程序在工作，且向服务器发出了连接请求
4. 接到连接请求之后，要使用ACCEPT函数，建立一个新的套接字，与请求方进行通信。
	以上四步是通讯前的准备工作
5. 接收对方的数据使用READ函数，该函数要指名读的套接字。读来的数据和读到字节的数量放到内存缓冲区。
6. 如果有信息发送给对方，使用WRITE函数。要指名发送给的套接字，发送数据的数据缓冲区地址，还有发送数据的数量。这两步是实际的通讯步骤可以同时进行，因为TCP连接是全双工的。
7. 最后关闭套接字，以释放套接字占用的内存。

## 二、客户端
1. 同服务器1
2. 使用connect与服务器进行连接，连接完成后进行绑定。
3. 同服务器端5.6
4. 同服务器端7

> 注意：在绑定之前需要初始化结构体sockaddr，用具体的IP地址与端口号，还要使用相关的数据格式转换函数。将主机的地址与端口号转换成网络的格式。

## 三、使用键盘进行通讯的过程描述：
1. 从键盘输入数据，写入数据缓冲区。使用例如scanf函数。
2. 从数据缓冲区将数据读出，写入socket。使用write函数。
3. 从socket读数据，写入内存缓冲区。使用read函数。

## 四、将一个文件通过socket发送给对方的过程：
1. 打开一个文件。使用fopen函数。
2. 将文件的数据读入内存缓冲区。使用fscanf,fread函数。
3. 从数据缓冲区将数据读出，写入socket。使用write函数。
4. 从socket读数据，写入内存缓冲区。使用read函数。
5. 如果是把从socket读到的数据写入文件，使用fprintf函数，把读入的内存缓冲区的数据放入文件。
6. 关闭socket和文件。