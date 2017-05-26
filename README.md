# [FOS] OWASP CRS 3 & COMODO WAF Patch rules
![picsart_05-26-12 42 26](https://cloud.githubusercontent.com/assets/22318677/26484647/f8728c7c-4210-11e7-822d-7d3a19ca95e5.jpg)
## How to write Custom WAF rule to block new attacks on web application?
   1. At first, try to identify the security issue i.e payload or process which normally  WAF failed to detect. 
   2. Based on that develope regex pattern to match that payload. 
   3. Follow the modsecurity syntax to  write a new rule.
   4. Save the rule as .conf and include in the default rules directory.
   5. Restart the Apache server and start testing the WAF rules. 


## Security Issue Overview:
When i started testing normal injection technique on both OWASP CRS 3 & Comodo WAF Ruleset  separately with vulnerable app i.e [SQLI-LABS](https://github.com/Audi-1/sqli-labs), WAF works well. But when I tried injection payloads with different encoding techniques i.e Base64,urlencoded  (any other encoding method that support on application back-end) , it failed to detect  which lead to all possible injection attack.
   

## Demo WAF rule Writing 

1. Start testing the WAF rule i.e Comodo free WAF rules or OWASP crs rules with vulnerable web application and identifying the security issue in their rules.

2. While testing the OWASP CRS 3 &  Comodo WAF rules, I  have found  some loop hole which allow user to bypass sql injection rules. i.e OWASP CRS & Comodo Rules failed to detect base64 encoded payload or anyother encoding method that works on the application back-end.
 
3. Let see why ? OWASP CRS 3 and Comodo WAF rule does include rules to detect base64 encoded payloads.

 `Demo Video :Testing OWASP CRS 3 & Comodo WAF rules`

[![Alt text](https://img.youtube.com/vi/_CgNY9u94LU/0.jpg)](https://www.youtube.com/watch?v=_CgNY9u94LU)


4. These are the following payload which OWASP CRS 3 && comodo WAF rules failed to detected. <br>

`Normal Payload in base64 encoding:`

**admin') order by 3# :- YWRtaW4nKSBvcmRlciBieSAzIw==  <br /> 
 -admin') union select 1,2,3# :- LWFkbWluJykgdW5pb24gc2VsZWN0IDEsMiwzIw== <br />
 -admin') union select 1,database(),3# :- LWFkbWluJykgdW5pb24gc2VsZWN0IDEsZGF0YWJhc2UoKSwzIwo= <br />
 -admin') union select 1,group_concat(username),group_concat(password) from users# :-    LWFkbWluJykgdW5pb24gc2VsZWN0IDEsZ3JvdXBfY29uY2F0KHVzZXJuYW1lKSxncm91cF9jb25jYXQocGFzc3dvcmQpIGZyb20gdXNlcnMj**
 
 5. Start writing regex to match the payload
 6. Fixing the identified security issue  bywriting custom WAF rule.

`Demo Video :Writing  custom rule to block above mentioned payloads using regex expression`

[![Alt text](https://img.youtube.com/vi/e248UPpkca0/0.jpg)](https://www.youtube.com/watch?v=e248UPpkca0)


## Updates
If you want new rules, create an issue report and label it as enhancement Or start a pull request on our repositories.

## :scroll:Changelog
I will update new rules with  improvements i.e with out any false positive detection . Be sure to check out the [Changelog](https://github.com/umarfarook882/WAF-Rule-Writing-part-2/wiki/Change-Log)

## :octocat:Credits:
* Umar Farook: [Security Engineer | Researcher](https://www.linkedin.com/in/umar-farook-a45603101)

## :octocat:How to contribute
All contributions are welcome, from code to documentation, to design suggestions, to bug reports.
Please use GitHub to its fullest. submit pull requests, contribute tutorials or other wiki content, whatever 
you have to offer, we can use it!

## Support !
Email address: umarfarookmech712@gmail.com  for more details.

## Useful links:
 1. [Modsecurity](www.modsecurity.com/)
 2. [Kali](https://www.kali.org/)
 3. [Debuggex](https://www.debuggex.com/)
 4. [OWASP Mutillidae Vulnerable App](https://www.owasp.org/index.php/OWASP_Mutillidae_2_Project)
 5. [SQLi LABS](https://github.com/Audi-1/sqli-labs)
