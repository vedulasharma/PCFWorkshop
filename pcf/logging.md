[Section 5 - User Provided Services (UPS) and Environment Variables](userprovidedservice.md) | [PCF Home](README.md)

# Section 6 - Log and Log Management (and NOT Monitoring)

**Note - as of 02/03/2016, there is a known issue with application logs not being received by THD Splunk.  Multiple Home Depot teams and Pivotal are working to resolve - please refer to the #pcf-splunk channel for updates.**

## Overview

Through out this workshop, we have referred to the `cf logs` command several times to troubleshoot our applications.  In this section, we will take a deeper look into logging within Cloud Foundry and cloud architecture overall.  

Per 12 Factor, logs should be treated as event streams.  This contrasts with the Tomcat Grid where logs are written to a file on the file system.  Logs on Cloud Foundry are written to `stdout` and/or `stderr`.  These are capture by the execution environment and sent to a system called *loggregator* (you may also hear it called _doppler_).  Loggregator will store logs locally in a ring buffer which can be accessed via the `cf logs` command.  Logs are aggregated between various system components to provide holistic view of your application.

Additionally, logs can be sent off platform for longer storage and enhanced querying.  This is done by leveraging a **syslog drain**.  The syslog drain attaches to loggregator and emits your application logs via tcp to the specified endpoint.  

Since logs are treated as an event stream, Cloud Foundry will not sacrifice application performance in favor of logs.  If loggregator gets overloaded, it will simply drop log messages and log the amount of messages it dropped and for what application.  Because of this handling, **logs should not be used as a monitoring tool.**  It is recommend to leverage an application performance monitoring tool such as New Relic or App Dynamics or an exception handling tool like Airbrake.   

## Creating a syslog drain

### Exercise
1. Be sure you are targeted to your **development** space.
2. Create a user provided service for the syslog drain `syslog://syslogx.homedepot.com:514`
  * Remember the `-l` flag and use `-h` if you need help.
3. Bind your new service to your services and UI applications.
  * Remember to restage to pick up the changes.
4. Look at your services application's environment variables to see the syslog drain entry.  
5. Get your app guid using the `cf app` command.
**If PCF->Splunk is working**
6. Log into [_splunk.homedepot.com_](http://splunk.homedepot.com) and select **Search**.
7. Run a query for your app guid over the last 15 minutes.  You should see the same log message that you see in the `cf logs` command.


### More information

[12 Factor : Logs](http://12factor.net/logs)

[Application Logging](https://docs.pivotal.io/pivotalcf/devguide/deploy-apps/streaming-logs.html)

[Log Management](http://docs.pivotal.io/pivotalcf/devguide/services/log-management.html)

[App Log Streaming](http://docs.cloudfoundry.org/services/app-log-streaming.html)

[Back to Workshop Home](../README.md)
