[Section 1 - CLI](CLI.md) | [PCF Home](README.md) | [Section 3 - Deploying a Backend Application (db, backend app)](BackendService.md)

# Section 2 - Deploying and Scaling an Application

## Overview

Now that we are comfortable navigating within Cloud Foundry, we can now deploy some sample applications.  Within Cloud Foundry, you may hear the term _**push**_ used. Push refers to the `cf push` command and often replaces the term deploy.  More on the `cf push` command below.

Key commands for interacting with applications

* `cf push`  
  * This command is used to deploy application to Cloud Foundry.  It can be used with either command line flags/arguments or a manifest file (more on that in a later section).  We will be using command line flags / arguments for these exercises.
* `cf scale`  
  * This command allows you to adjust the number of instances of an application you are running.  
*  `cf apps`
  * This command shows the status of your applications based upon your current targeted organization and space.
* `cf app`
  * This command shows details for a given application.  
* `cf start` & `cf stop`
  * This will start or stop a given application
* `cf restage`
  * This will restart an application and cause any environment changes to be applied.

## Deploying your application

### Exercise

As part of the workshop, we have provided a repo of sample applications.  If you have cloned the PCFWorkshop repo, you will find it as a folder, cf-hello-world-sample-apps. If not, now is the time to test your "git" expertise. :-)

1. `cd` into the `cf-hello-world-sample-apps` directory.
2. List the directories (ls -l or dir). What do you see?  What do you think is in each directory?
3. `cd` into the `node` directory.
4. Be sure you are targeting your **development** space in Cloud Foundry.
5. Run a `cf push <application name> -m 512m --random-route`
  * `<application name>` can be anything you want it to be, name your application something memorable!
  * The `-m` flag allows you to set maximum memory allocated.  As we are in a limited environment, please remember to set this
  * `--random-route` causes Cloud Foundry to append a random set of strings to your application name when deploying.  This helps to prevent conflicts with other deployed applications with the same name that may be in a different space.  **Only one route name can exist across an entire Cloud Foundry installation regardless of organization or spaces.**
6. Confirm your application is running by connecting to the application route printed as part of your `cf push` command.  You may use curl or your browser.

  ```
  $cf push <app-name> -m 512m --random-route
  ...

  Showing health and status for app <app-name> in org myorg / space development as user...
  OK

  requested state: started
  instances: 1/1
  usage: 1G x 1 instances
  urls: <app-name>-myopathic-mentalism.cfapps.io/
  last uploaded: Fri March 31 21:31:31 UTC 2017
  stack: cflinuxfs2
  ```
7. Repeat steps 2-5 for another language in the sample applications. (See Step #3 above)

NOTE: If you missed the url that was provided by Cloud Foundry when you pushed your app, try `cf app <app-name>` to describe your app.

### What exactly has happened when you ran `cf push`?

* Cloud Foundry automatically detected  which buildpack is required (Node in this case).

* The buildpack and the application are combined to make  a “droplet” (the Cloud Foundry unit of execution) and is pushed  to the Execution Environment (aka VM).

* Started application on the Execution Environment.

## Interacting with your applications

### Exercise

1. Stop your application by running `cf stop <app-name>`.
2. Confirm that your application is stopped by using the `cf apps` command.
3. Start your application by running `cf start <app-name>`.
4. Confirm that your application is now running using `cf apps`.
5. Determine which buildpack was used for your application by running `cf app <app-name>`.
6. Finally, scale the number of instances of your application to two by using the `cf scale -i 2 <app-name>`.
7. Confirm that two instances are now running using `cf apps` again.

### For curious minds, more details here from Pivotal docs
[Deploy an Application](https://docs.pivotal.io/pivotalcf/devguide/deploy-apps/deploy-app.html)

[About starting applications](https://docs.pivotal.io/pivotalcf/devguide/deploy-apps/app-startup.html)

[Buildpack](https://docs.pivotal.io/pivotalcf/buildpacks/index.html)

[Scaling an application](https://docs.pivotal.io/pivotalcf/devguide/deploy-apps/cf-scale.html)


[Next Section - Deploying a Backend Application ->](BackendService.md)
