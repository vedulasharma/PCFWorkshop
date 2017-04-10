[Section 3 - Deploying a Backend Application (db, backend app)](BackendService.md) | [PCF Home](README.md) | [Section 6 - User Provided Services (UPS) and Environment Variables](userprovidedservice.md)

# Section 4 - Manifest And Buildpacks

## Overview

A manifest is an easy way to capture all the needed setup and parameters for an app for deployment and configuration. This lets anybody deploy consistently and fail fast if dependencies are missing.

Open this in another window for reference during this section. [Pivotal Manifest Documentation](http://docs.pivotal.io/pivotalcf/devguide/deploy-apps/manifest.html)

Key commands you will use in this Section

* `cf buildpacks`
  * This command allows you to see the available buildpacks offered by the platform.

## Tear Down and Clean up

We need to begin this section with a *clean slate* so lets use what you have learned so far and delete a few things.

### Exercise

1. Return to each of your spaces and delete any deployed applications. (hint: `cf help` if not sure).  
2. Leave your services in place in both spaces.

NOTE: Deleting an app will unbind the service instance from the app, but leave the service instance in place to be rebound.  We will cover this more in Section 6.

## Create Basic Manifest

You can specify almost 20 different settings via the manifest.  This is much better than specifying these options via flags on the `cf push` command.

### Exercise

1. Target your **development** space
2. Create a file `manifest.yml` in the same directory as the cities-services.jar. and put inside the following content:

  ```
  ---
  applications:
    -
      name: [YOUR-USER-ID]-cities-services
      path: cities-service-cities-service.jar
  ```
3. Now type `cf push` and nothing else and press enter.  
4. YAML is very picky.  If you are having issues, it is good idea to use a YAML Lint check - http://www.yamllint.com
5. Your app will fail because we forgot to bind the service.  Now make the manifest do that for us.
  ```
  ---
  applications:
    -
      name: [YOUR-USER-ID]-cities-services
      path: cities-service-cities-service.jar
      services:
        -
          [YOUR-SERVICE-NAME]

  ```
6. Now type `cf push` again and nothing else and press enter.  
7. Verify that your app is alive by hitting the url.


## Buildpacks

Many different languages can be used with Cloud Foundry:  ruby, python, java, node, even static files. The way this works is through buildpacks.  If you look closely at the output from `cf push` you will see that it takes your code, and merges it with a buildpack that best represents your code.  

If you have python, it uses the python buildpack.  If you have a jar, it uses the java buildpack.  Each of these buildpacks create a runtime.  For instance the java buildpack may contain a tomcat or jetty instance (you do not care).  The static file buildpack contains nginx.

The problem is that if you do not specify a buildpack. Cloud Foundry will download **ALL** buildpacks so it can best determine which one it should use.

To speed up this process, it is **HIGHLY** recommended that you specify a buildpack either via the command line or better, via the manifest.

### Exercise

1. Delete the app from your space (again)
2. Verify your service instance is still available but unbound.
3. What buildpacks are available? (hint: `cf buildpacks`)
4. Modify your manifest to include a proper build pack.
5. Now type `cf push` again and nothing else and press enter.  
6. Look carefully at the output.  Did it skip the buildpack download section?

## Tuning Runtime Environment

Lets now add some additional information to the manifest to tune our application.  You can specify the amount of memory that the application can use and also how many instances should be running by default.


### Exercise

(hint `cf app <app-name>`)

1. How much memory is your app allocated?
2. How much memory is your app currently using?
3. How many instances is your app running?
4. Delete the app from your space (again)
5. Verify your service instance is still available but unbound.
6. Add in the manifest entry for 2 instances.
7. Add into the manifest the entry for less memory than already allocated.  (maybe 800M total)
5. Now type `cf push` again and nothing else and press enter.  
6. Does `cf app <app-name>` validate that your newly requested values were applied?  



### For curious minds, more details here from Pivotal docs

[Deploying with Application Manifests](http://docs.pivotal.io/pivotalcf/devguide/deploy-apps/manifest.html)

[YAML Syntax Validation](http://www.yamllint.com)

[Next Section - User Provided Services (UPS) and Environment Variables ->](userprovidedservice.md)
