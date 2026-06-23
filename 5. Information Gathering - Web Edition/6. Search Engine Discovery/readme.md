# Search Engine Discovery

Search Engine Discovery là kỹ thuật sử dụng các công cụ tìm kiếm (Google, Bing, DuckDuckGo...) để thu thập thông tin công khai về:

- Website
- Tổ chức
- Cá nhân
- Hệ thống CNTT

## Search Operators

- site: Giới hạn kết quả trong một domain. `site:example.com`

- inurl: Tìm chuỗi trong URL. `inurl:login`

- filetype: Tìm loại file cụ thể. `filetype:pdf`

- intitle: Tìm trong tiêu đề trang. `intitle:"confidential report"`

- intext: Tìm trong nội dung trang. `intext:"password reset"`

- cache: Xem bản cache của Google. `cache:example.com`

- link: Tìm website đang link tới mục tiêu. `link:example.com`

- related: Tìm website tương tự. `related:example.com`

- info: Thông tin tổng quan về website. `info:example.com`

### Các toán tử logic

- AND

Bắt buộc chứa tất cả từ khóa.

Ví dụ:

`site:example.com AND inurl:admin`

- OR

Chứa một trong các từ khóa.

Ví dụ:

`linux OR ubuntu OR debian`

- NOT

Loại bỏ kết quả.

Ví dụ:

`site:example.com NOT inurl:login`

- Dấu ngoặc kép

Tìm chính xác cụm từ.

Ví dụ:

`"information security policy"`

- Dấu *

Wildcard.

Ví dụ:

`user* manual`

Có thể khớp:

user guide\
user handbook\
user manual

- Dấu -

Loại bỏ từ khóa.

Ví dụ:

`site:news.com -sports`
