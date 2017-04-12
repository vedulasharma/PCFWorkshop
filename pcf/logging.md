[Section 5 - User Provided Services (UPS) and Environment Variables](userprovidedservice.md) | [PCF Home](README.md)

# Section 6 - Log and Log Management (and NOT Monitoring)

## Overview

Through out this workshop, we have referred to the `cf logs` command several times to troubleshoot our applications.  In this section, we will take a deeper look into logging within Cloud Foundry and cloud architecture overall.  

Per 12 Factor, logs should be treated as event streams.  This contrasts with the Tomcat Grid where logs are written to a file on the file system.  Logs on Cloud Foundry are written to `stdout` and/or `stderr`.  These are captured by the execution environment and sent to a system called *loggregator* (you may also hear it called _doppler_).  Loggregator will store logs locally in a ring buffer which can be accessed via the `cf logs` command.  Logs are aggregated between various system components to provide holistic view of your application.

Additionally, logs can be sent off platform for longer storage and enhanced querying.  This is done by leveraging a **syslog drain**.  The syslog drain attaches to loggregator and emits your application logs via tcp to the specified endpoint.  

Since logs are treated as an event stream, Cloud Foundry will not sacrifice application performance in favor of logs.  If loggregator gets overloaded, it will simply drop log messages and log the amount of messages it dropped and for what application.  Because of this handling, **logs should not be used as a monitoring tool.**  It is recommended to leverage an application performance monitoring tool such as New Relic or App Dynamics or an exception handling tool like Airbrake.

Typically, a user provided service is created for the syslog drain.  Once you create it, you can bind this service to all your services.  You can verify this by looking at your service's application's environment variables, after it has been bound.


### More information

[12 Factor : Logs](http://12factor.net/logs)

[Application Logging](https://docs.pivotal.io/pivotalcf/devguide/deploy-apps/streaming-logs.html)

[Log Management](http://docs.pivotal.io/pivotalcf/devguide/services/log-management.html)

[App Log Streaming](http://docs.cloudfoundry.org/services/app-log-streaming.html)

[Back to Workshop Home](../README.md)
