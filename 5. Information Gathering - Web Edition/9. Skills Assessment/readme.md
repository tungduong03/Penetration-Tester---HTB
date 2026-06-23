# Lab 

```bash
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ whois inlanefreight.com
   Domain Name: INLANEFREIGHT.COM
   Registry Domain ID: 2420436757_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.registrar.amazon
   Registrar URL: http://registrar.amazon.com
   Updated Date: 2026-05-13T08:57:09Z
   Creation Date: 2019-08-05T22:43:09Z
   Registry Expiry Date: 2026-08-05T22:43:09Z
   Registrar: Amazon Registrar, Inc.
   Registrar IANA ID: 468
   Registrar Abuse Contact Email: trustandsafety@support.aws.com
   Registrar Abuse Contact Phone: +1.2024422253
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Name Server: NS-1303.AWSDNS-34.ORG
   Name Server: NS-1580.AWSDNS-05.CO.UK
   Name Server: NS-161.AWSDNS-20.COM
   Name Server: NS-671.AWSDNS-19.NET
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
```

```bash
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ whatweb 154.57.164.71:30460
http://154.57.164.71:30460 [200 OK] Country[UNITED STATES][US], HTML5, HTTPServer[nginx/1.26.1], IP[154.57.164.71], Title[inlanefreight], nginx[1.26.1]
```

Tìm VHOSTS 

```bash
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ gobuster vhost -u http://154.57.164.71:30460 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain --domain inlanefreight.htb
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:             http://154.57.164.71:30460
[+] Method:          GET
[+] Threads:         10
[+] Wordlist:        /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt
[+] User Agent:      gobuster/3.6
[+] Timeout:         10s
[+] Append Domain:   true
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: web1337.inlanefreight.htb Status: 200 [Size: 104]
Progress: 114442 / 114443 (100.00%)
===============================================================
Finished
===============================================================
```

Truy cập web 

`http://web1337.inlanefreight.htb:30460/robots.txt`

Ta được 

```
User-agent: *
Allow: /index.html
Allow: /index-2.html
Allow: /index-3.html
Disallow: /admin_h1dd3n
```

Truy cập 

`http://web1337.inlanefreight.htb:30460/admin_h1dd3n/`

```
Welcome to web1337 admin site
The admin panel is currently under maintenance, but the API is still accessible with the key e963d863ee0e82ba7080fbf558ca0d3f
```

Cài đặt reconspider 

`pip3 install scrapy`

```bash
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
--2026-06-22 23:51:28--  https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
Resolving academy.hackthebox.com (academy.hackthebox.com)... 109.176.239.69, 109.176.239.70
Connecting to academy.hackthebox.com (academy.hackthebox.com)|109.176.239.69|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1706 (1.7K) [application/zip]
Saving to: ‘ReconSpider.zip’

ReconSpider.zip                                 100%[=====================================================================================================>]   1.67K  --.-KB/s    in 0s      

2026-06-22 23:51:29 (22.7 MB/s) - ‘ReconSpider.zip’ saved [1706/1706]

┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ unzip ReconSpider.zip
Archive:  ReconSpider.zip
  inflating: ReconSpider.py 
```

chạy 

`python3 ReconSpider.py http://inlanefreight.htb:30460`

-> ko tìm thấy mail 

CHạy tìm thêm vhost 

```bash
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ gobuster vhost -u http://154.57.164.71:30460 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain --domain web1337.inlanefreight.htb
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:             http://154.57.164.71:30460
[+] Method:          GET
[+] Threads:         10
[+] Wordlist:        /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt
[+] User Agent:      gobuster/3.6
[+] Timeout:         10s
[+] Append Domain:   true
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: dev.web1337.inlanefreight.htb Status: 200 [Size: 123]
```

ta tìm được thêm dev.web1337.inlanefreight.htb

THêm lại vào /etc/hosts 

```bash
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ python3 ReconSpider.py http://dev.web1337.inlanefreight.htb:30460
2026-06-22 23:56:27 [scrapy.utils.log] INFO: Scrapy 2.16.0 started (bot: scrapybot)
2026-06-22 23:56:27 [scrapy.utils.log] INFO: Versions:
{'lxml': '5.4.0',
 'libxml2': '2.9.14',
 'cssselect': '1.3.0',
 'parsel': '1.11.0',
 'w3lib': '2.4.1',
 'Twisted': '26.4.0',
 'Python': '3.13.5 (main, Jun 25 2025, 18:55:22) [GCC 14.2.0]',
 'pyOpenSSL': '25.0.0 (OpenSSL 3.5.5 27 Jan 2026)',
 'cryptography': '43.0.0',
 'Platform': 'Linux-6.19.6+parrot7-amd64-x86_64-with-glibc2.41'}
2026-06-22 23:56:27 [scrapy.addons] INFO: Enabled addons:
[]
2026-06-22 23:56:27 [scrapy.extensions.telnet] INFO: Telnet Password: f1fa0acbcf7e73af
2026-06-22 23:56:27 [scrapy.middleware] INFO: Enabled extensions:
['scrapy.extensions.corestats.CoreStats',
 'scrapy.extensions.logcount.LogCount',
 'scrapy.extensions.telnet.TelnetConsole',
 'scrapy.extensions.memusage.MemoryUsage',
 'scrapy.extensions.logstats.LogStats']
2026-06-22 23:56:27 [scrapy.crawler] INFO: Overridden settings:
{'LOG_LEVEL': 'INFO'}
2026-06-22 23:56:27 [py.warnings] WARNING: /usr/lib/python3.13/importlib/__init__.py:88: UserWarning: You have brotli installed. But 'br' encoding support now requires brotli's or brotlicffi's version >= 1.2.0. Please upgrade brotli/brotlicffi to make Scrapy decode 'br' encoded responses.
  return _bootstrap._gcd_import(name[level:], package, level)

2026-06-22 23:56:27 [scrapy.middleware] INFO: Enabled downloader middlewares:
['scrapy.downloadermiddlewares.offsite.OffsiteMiddleware',
 'scrapy.downloadermiddlewares.httpauth.HttpAuthMiddleware',
 'scrapy.downloadermiddlewares.downloadtimeout.DownloadTimeoutMiddleware',
 'scrapy.downloadermiddlewares.defaultheaders.DefaultHeadersMiddleware',
 'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware',
 '__main__.CustomOffsiteMiddleware',
 'scrapy.downloadermiddlewares.retry.RetryMiddleware',
 'scrapy.downloadermiddlewares.redirect.MetaRefreshMiddleware',
 'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware',
 'scrapy.downloadermiddlewares.redirect.RedirectMiddleware',
 'scrapy.downloadermiddlewares.cookies.CookiesMiddleware',
 'scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware',
 'scrapy.downloadermiddlewares.stats.DownloaderStats']
2026-06-22 23:56:27 [scrapy.middleware] INFO: Enabled spider middlewares:
['scrapy.spidermiddlewares.start.StartSpiderMiddleware',
 'scrapy.spidermiddlewares.httperror.HttpErrorMiddleware',
 'scrapy.spidermiddlewares.referer.RefererMiddleware',
 'scrapy.spidermiddlewares.urllength.UrlLengthMiddleware',
 'scrapy.spidermiddlewares.depth.DepthMiddleware']
2026-06-22 23:56:27 [scrapy.middleware] INFO: Enabled item pipelines:
[]
2026-06-22 23:56:27 [scrapy.core.engine] INFO: Spider opened
2026-06-22 23:56:27 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min)
2026-06-22 23:56:27 [scrapy.extensions.telnet] INFO: Telnet console listening on 127.0.0.1:6023
2026-06-22 23:56:53 [scrapy.core.engine] INFO: Closing spider (finished)
2026-06-22 23:56:53 [scrapy.statscollectors] INFO: Dumping Scrapy stats:
{'downloader/request_bytes': 31699,
 'downloader/request_count': 100,
 'downloader/request_method_count/GET': 100,
 'downloader/response_bytes': 34117,
 'downloader/response_count': 100,
 'downloader/response_status_count/200': 100,
 'elapsed_time_seconds': 26.08891732400025,
 'finish_reason': 'finished',
 'finish_time': datetime.datetime(2026, 6, 23, 3, 56, 53, 293498, tzinfo=datetime.timezone.utc),
 'items_per_minute': 0.0,
 'log_count/INFO': 3,
 'memusage/max': 71651328,
 'memusage/startup': 71651328,
 'request_depth_max': 99,
 'response_received_count': 100,
 'responses_per_minute': 230.76923076923077,
 'scheduler/dequeued': 100,
 'scheduler/dequeued/memory': 100,
 'scheduler/enqueued': 100,
 'scheduler/enqueued/memory': 100,
 'start_time': datetime.datetime(2026, 6, 23, 3, 56, 27, 204576, tzinfo=datetime.timezone.utc)}
2026-06-22 23:56:53 [scrapy.core.engine] INFO: Spider closed (finished)
┌─[eu-academy-3]─[10.10.15.11]─[htb-ac-1384230@htb-mubqpjm6ky]─[~]
└──╼ [★]$ cat results.json
{
    "emails": [
        "1337testing@inlanefreight.htb"
    ],
    "links": [
        "http://dev.web1337.inlanefreight.htb:30460/index-909.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-944.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-687.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-989.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-641.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-105.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-948.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-329.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-403.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-795.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-248.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-760.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-292.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-888.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-964.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-555.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-166.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-437.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-379.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-326.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-737.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-553.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-939.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-728.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-224.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-755.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-463.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-949.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-977.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-626.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-254.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-302.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-643.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-615.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-631.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-585.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-714.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-114.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-577.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-408.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-799.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-660.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-727.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-431.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-815.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-226.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-350.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-789.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-342.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-531.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-247.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-384.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-933.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-465.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-798.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-862.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-918.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-925.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-895.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-77.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-80.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-581.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-332.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-291.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-204.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-504.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-165.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-769.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-785.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-203.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-459.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-335.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-334.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-134.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-189.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-513.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-458.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-748.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-734.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-807.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-635.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-24.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-300.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-220.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-202.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-364.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-244.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-567.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-472.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-561.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-525.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-817.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-938.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-947.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-988.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-733.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-1000.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-385.html",
        "http://dev.web1337.inlanefreight.htb:30460/index-574.html"
    ],
    "external_files": [],
    "js_files": [],
    "form_fields": [],
    "images": [],
    "videos": [],
    "audio": [],
    "comments": [
        "<!-- Remember to change the API key to ba988b835be4aa97d068941dc852ff33 -->"
    ]
}
```

Ta có mail và key cho 2 câu hỏi cuối 




