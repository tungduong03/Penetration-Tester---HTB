# Introduction

Mục tiêu của Web recon: 

- `Xác định assets`: Khám phá tất cả các thành phần có thể truy cập công khai của mục tiêu, chẳng hạn như trang web, tên miền phụ, địa chỉ IP và công nghệ được sử dụng. Bước này cung cấp cái nhìn tổng quan toàn diện về sự hiện diện trực tuyến của mục tiêu.

- `Discovering Hidden Information`: Xác định vị trí các thông tin nhạy cảm có thể bị lộ ngoài ý muốn, bao gồm các tệp sao lưu, tệp cấu hình hoặc tài liệu nội bộ. Những phát hiện này có thể tiết lộ những thông tin quan trọng và các điểm xâm nhập tiềm tàng cho các cuộc tấn công.

- `Analysing the Attack Surface`: Kiểm tra bề mặt tấn công của mục tiêu để xác định các lỗ hổng và điểm yếu tiềm tàng. Điều này bao gồm đánh giá các công nghệ được sử dụng, cấu hình và các điểm xâm nhập có thể bị khai thác.

- `Gathering Intelligence:` Thu thập thông tin có thể được tận dụng để khai thác thêm hoặc thực hiện các cuộc tấn công kỹ thuật xã hội. Điều này bao gồm việc xác định các nhân sự chủ chốt, địa chỉ email hoặc các kiểu hành vi có thể bị lợi dụng.

## Type

### Active recon 

- Port scanning: Nmap, Masscan, Unicornscan

- Vulnerability Scanning: Nessus, OpenVAS, Nikto

- Network mapping: Traceroute, Nmap - Lập bản đồ mạng của máy mục tiêu và các máy khác

- Banner grabbing: Netcat, curl

- OS fingerprinting: Nmap, Xprobe2

- Service Enum: nmap

- Web spidering: Burp Suite Spider, OWASP ZAP Spider, Scrapy

### Passive Recon

- Search Engine Queries: Google, DuckDuckGo, Bing, and specialised search engines (e.g., Shodan)

- WHOIS Lookups

- DNS: dig, nslookup, host, dnsenum, fierce, dnsrecon

- Web Archive Analysis: Wayback Machine

- Social Media Analysis: LinkedIn, Twitter, Facebook, specialised OSINT tools

- Code Repositories: GitHub, GitLab

