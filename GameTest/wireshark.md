只保留指定 IP 的非 TCP/UDP 包，比如游戏测试中抓 ARP、ICMP、DNS 等协议包

## 过滤端口

例子:
	tcp.port eq 80 // 不管端口是来源的还是目标的都显示
	tcp.port == 80
	tcp.port eq 2722
	tcp.port eq 80 or udp.port eq 80
	tcp.dstport == 80 // 只显tcp协议的目标端口80
	tcp.srcport == 80 // 只显tcp协议的来源端口80
	udp.port eq 15000
	过滤端口范围
	tcp.port >= 1 and tcp.port <= 80
## 包长度过滤

例子:

	udp.length == 26 这个长度是指udp本身固定长度8加上udp下面那块数据包之和
	tcp.len >= 7   指的是ip数据包(tcp下面那块数据),不包括tcp本身
	ip.len == 94 除了以太网头固定长度14,其它都算是ip.len,即从ip本身到最后
	frame.len == 119 整个数据包长度,从eth开始到最后
	eth —> ip or arp —> tcp or udp —> data

## http模式过滤

例子:

	http.request.method == “GET”
	http.request.method == “POST”
	http.request.uri == “/img/logo-edu.gif”
	http contains “GET”
	http contains “HTTP/1.”
	// GET包
	http.request.method == “GET” && http contains “Host: “
	http.request.method == “GET” && http contains “User-Agent: “
	// POST包
	http.request.method == “POST” && http contains “Host: “
	http.request.method == “POST” && http contains “User-Agent: “
	// 响应包
	http contains “HTTP/1.1 200 OK” && http contains “Content-Type: “
	http contains “HTTP/1.0 200 OK” && http contains “Content-Type: “
	一定包含如下
	Content-Type:

## TCP参数过滤

	tcp.flags 显示包含TCP标志的封包。
	tcp.flags.syn == 0x02     显示包含TCP SYN标志的封包。
	tcp.window_size == 0 && tcp.flags.reset != 1