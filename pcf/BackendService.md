[Section 2 - Deploying and Scaling an Application](DeployingBasics.md) | [PCF Home](README.md) | [Section 4 - Ready for Acceptance Testing ](spaces.md)

# Section 3 - Deploying a Backend Microservice Application (DB & Application)

## Overview

In this exercise, we will deploy a simple Spring Boot based application and attach it to a MySQL instance.  The application provides information about cities.  For purposes of the class, we have already compiled the application.  

Key commands you will use in this Section

* `cf marketplace`
  * This command allows you to see the available service offerings provided by the platform.
* `cf logs`
  * This command allows you to view logs related to your application.  This can be a logs that your logs that your application emits or platform logs that related your application.
  * `--recent` will dump logs instead of tailing.
* `cf services`
  * This command will list services that you have created for your targeted organization and space.
* `cf create-service`
  * This command will create a service instance based upon an available service from the marketplace.  
* `cf bind-service`
  * This command will associate a specified service instance with a specified application.  This will allow the application to leverage the service instance.
* `cf env`
  * This command will list all environment variables for a given application.

### A word on services

You will hear the word **service** used often going forward.  This word can have several meaning to different people.  In terms of Cloud Foundry, applications access external resources through the use of services.  These can be databases, messaging systems, or other applications that offer REST APIs.  We will go more in depth into the different type of services in Section 6.

## Deploying cities-services

### Exercise

1. Be sure you are targeted to your **development** space.
2. You should have the cities-services.jar, if you have cloned this repo.  
3. Deploy the cities-services application
  * Prepend your application name with your user id. Example: `cf push yourname-cities-services -p cities-services.jar`
  * Since you are deploying a binary artifact, you will need to provide the path to the jar file using the `-p` flag.
  * If you are out of available memory in your organization because of your allocated quota, you can delete some of your other sample applications (hint: `cf help` if unsure).
4. Your application should fail to start.  Using the `cf logs --recent` command, take a look at the logs and look for the error.
5. Remember in the overview, we mentioned that we need to attach the application to a MySQL database.  The application is failing as it is attempting to attach to that database which we haven't created yet.

## Creating a MySQL service instance

We will be using the managed MySQL service provided to you on Cloud Foundry for our application.

### Exercise

1. Using the `cf marketplace` command, investigate available services provided by the platform.
  * You should see something like below
```
service          plans                                                           description
cedexisradar     free-community-edition                                          Free Website and Mobile App Performance Reports
cleardb          spark, boost*, amp*, shock*                                     Highly available MySQL for your Apps.
cloudamqp        lemur, tiger*, bunny*, rabbit*, panda*                          Managed HA RabbitMQ servers in the cloud
```
2. Based on the marketplace results, we have three MySQL plans (listed as, "cleardb" in the results) available to use - **spark, boost*, amp*, shock***.  Let us use the **spark** plan to create a MySQL instance using the `cf create-service` command. 
  * Try to look for the command that will give you a description of each of the options. There is also a short hand for this command.  You can use the help command to discover it.
3. Confirm that your service instance is now available by running `cf services`.
  * Notice that is is not bound to any application yet.  We will be doing that next.

### What happened when you created a service instance?

* Based upon the service and plan you selected, a service broker was engaged to validate that the plan was available and required information was provided.
* The service broker connected with the MySQL data service running on Cloud Foundry
* A new database was provisioned and a user and password created to access that database.
* The MySQL data service provided that information back to the service broker as a service instance.

## Bind MySQL service instance to cities services

### Exercise
1. Bind your MySQL service that you created above with your cities service application.  Run `cf bind-service <app-name> <service-instance-name>`.
2. Restage your application using `cf restage` to pick up your changes.
3. You should notice that your application started successfully this time.  You can validate by connecting to the app in your browser.
4. Confirm the service is bound by running `cf services`.
5. Run `cf env <app-name>` to validate that you see the MySQL service instance as part of your application's environment variables.
  * Notice that there is a lot more information produced from the `cf env` command.  We will talk more about this in Section 6.

### What happened when you bound your application to a service instance?

Your service instance information, which contained the database, user id, and password, was injected into your application's environment.

### For curious minds, more details here from Pivotal docs

[Managing Services](http://docs.pivotal.io/pivotalcf/devguide/services/managing-services.html)

[Binding a Service Instance](http://docs.pivotal.io/pivotalcf/devguide/services/bind-service.html)

[Source code for citites-services microservice](https://github.com/krujos/pcf-workshop/tree/master/dev-experience/cities)

[Next Section - Ready for Acceptance Testing (ie code promotion) ->](spaces.md)
