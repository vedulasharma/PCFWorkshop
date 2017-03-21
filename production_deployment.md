[Topic 4 - PCF](pcf/README.md) | [Home](README.md)

#### Topic 5 - Production Deployment

How do I make my new code live?

* As of Feb 1, 2016, all normal SRB processes are still in place such as ARB and IRB. 
* You will need an approved CHG in ServiceNow.  This no different.  ServiceNow will be the "System of Records" for all Home Depot changes. 
* The recommended deployment path is to use a automated deployment pipeline that will pull the code, compile, run tests, and deploy if passes. 
* The Operations and Monitoring team is currently working on a Production pipeline that will be used when Encrypted passwords are needed for databases. 
* Use the #cloudfoundry channel or the #ci-cd for any additional questions. 
