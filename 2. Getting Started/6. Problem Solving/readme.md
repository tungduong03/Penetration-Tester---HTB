# Problem - Solve

## Vấn đề liên quan VPN HTB

Đây là nguyên nhân phổ biến nhất khi:

- Không ping được machine.
- Không SSH được.
- Không scan được bằng Nmap.
- Không truy cập được IP mục tiêu.

Kiểm tra VPN đã kết nối chưa

`sudo openvpn htb.ovpn`

Nếu thấy:

`Initialization Sequence Completed`

=> VPN đã kết nối thành công.

### Lấy địa chỉ VPN

Một cách khác để kiểm tra xem chúng ta đã kết nối với mạng VPN hay chưa là kiểm tra địa chỉ tun0 của VPN, mà ta có thể tìm thấy bằng lệnh sau:

```bash
reDrose18@htb[/htb]$ ip -4 a show tun0

6: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 500
    inet 10.10.10.1/23 scope global tun0
       valid_lft forever preferred_lft forever
```

### Checking Routing Table

Một cách khác để kiểm tra kết nối là sử dụng lệnh `sudo netstat -rn` để xem bảng định tuyến của chúng ta:

```bash
reDrose18@htb[/htb]$ sudo netstat -rn

[sudo] password for user: 

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.195.2   0.0.0.0         UG        0 0          0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG        0 0          0 tun0
192.168.1.0   0.0.0.0         255.255.255.0   U         0 0          0 eth0
```

### Pinging Gateway

Từ đây, ta có thể thấy rằng mình đã kết nối với mạng 10.10.14.0/23 trên bộ điều hợp tun0 và có quyền truy cập vào mạng 10.129.0.0/16, đồng thời có thể ping cổng mặc định 10.10.14.1 để xác nhận quyền truy cập.

```bash
reDrose18@htb[/htb]$ ping -c 4 10.10.14.1
PING 10.10.14.1 (10.10.14.1) 56(84) bytes of data.
64 bytes from 10.10.14.1: icmp_seq=1 ttl=64 time=111 ms
64 bytes from 10.10.14.1: icmp_seq=2 ttl=64 time=111 ms
64 bytes from 10.10.14.1: icmp_seq=3 ttl=64 time=111 ms
64 bytes from 10.10.14.1: icmp_seq=4 ttl=64 time=111 ms

--- 10.10.14.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3012ms
rtt min/avg/max/mdev = 110.574/110.793/111.056/0.174 ms
```

VPN HTB không thể kết nối đồng thời với nhiều hơn một thiết bị. Nếu bạn đang kết nối trên một thiết bị và cố gắng kết nối từ một thiết bị khác, lần kết nối thứ hai sẽ thất bại.

## Burp Suite Proxy Issues

### Not Disabling Proxy

Nhớ xem extention xem có bắt qua burp ko 

## Changing SSH Key and Password

