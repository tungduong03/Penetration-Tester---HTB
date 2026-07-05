# File Transfers

Giới thiệu

Trong quá trình Pentest, Red Team hoặc Privilege Escalation, việc chuyển file (File Transfer) giữa máy tấn công và máy mục tiêu là thao tác rất phổ biến.

Ví dụ cần chuyển:

- Upload web shell.
- Upload exploit.
- Upload công cụ leo thang đặc quyền (PrintSpoofer, JuicyPotato...).
- Download dữ liệu thu thập được.
- Download log.
- Upload script PowerShell hoặc Bash.
- Chuyển payload của Cobalt Strike, Metasploit...

Do đó, người làm Pentest cần biết nhiều kỹ thuật truyền file khác nhau, vì không phải môi trường nào cũng cho phép dùng một phương pháp duy nhất.

| Cách truyền | Có thể bị chặn |
| ----------- | -------------- |
| PowerShell  | AppLocker      |
| Certutil    | Proxy          |
| FTP         | Firewall       |
| HTTP        | Proxy          |
| SMB         | Firewall       |
| SCP         | SSH Disabled   |
