[Section 4 - Manifest And Buildpacks](manifest.md) | [PCF Home](README.md) | [Section 6 - Log and Log Management (and NOT Monitoring)](logging.md)

# Section 5 - User Provided Services (UPS) and Environment Variables

## Overview

Lets take a minute to talk about app configuration.  From 12factor.net
>An app’s config is everything that is likely to vary between deploys (staging, production, developer environments, etc). This includes:

> * Resource handles to the database, Memcached, and other backing services
> * Credentials to external services such as Amazon S3 or Twitter
> * Per-deploy values such as the canonical hostname for the deploy

Historically, application would have stored their configurations in a resource file packaged with application.  That file could then leverage a life cycle environment variable to determine what values should be used.  This causes conflicts because you have to change your code in order to change the configuration.  

We can alleviate this issue by moving our configuration to the environment itself.  These values are stored in environment variables that the application can then consume.  Configurations change without the need to change the source code of an application. You may have noticed this type of configuration if you have worked with Amazon Web Service, Google Cloud, or Azure.  Cloud Foundry follows the same methodology.  

Cloud Foundry has three methods to inject environment variables - managed services, user provided services, and environment variables.

### Services

Services can be shared across multiple applications within space.  Additionally, they can be created independently from an application.  

**Managed Services** are services that are provided by the Cloud Foundry platform via a service broker.  An example of this would be the  MySQL service we used earlier for our cities-service application.  

**User Provided Services** allows developers to use services that are not offered by Cloud Foundry.  This type of service can be used to connect to external databases (e.g. DB2) or connect to a syslog drain (more on this in Section 7).  User provided services provide information in a JSON object.

### Environment Variables

Where services can be bound to multiple applications, environment variables are specific to the application that they are set on.  They behave exactly like an OS environment variable and provide a key value pair.  Examples of environment variable uses would be to set a log level or app specific token.

Key commands that you will use in this section
* `cf create-user-provided-service`
  * This command will create user provided service.  
  * Using the `-l` flag will create the user provided service as a syslog drain (more in Section 7).  
  * Using `-p` will create a credential user provided service.  Information can be entered either via a JSON string or interactively by providing the keys.  See the help examples (remember `-h`).
* `cf set-env`
  * This command will set an environment variable for application.  

## Creating a User Provided Service

While our cities-service application provides a good API endpoint, it would be really helpful if we could attached it to a UI.  In fact, we've already compiled a UI for you.  It is called cities-ui (how creative).  

We need to be able to connect our UI to our cities-services endpoint.  Since the routes might (more like will) change between different environments, hard coding this route in the application would be a bad idea (as well as breaking 12 Factor).  So let's create a user provided service to tell our UI about the cities-services application.

### Exercise
1. Be sure you are targeted to your **development** space.
2. Look for the cities-ui.jar in this repo.
3. Deploy the cities-ui application.
  * Your application will fail to start - remember we need to tell it about our API service.
4. Our cities-ui application is looking for a user provided service containing two parameters: **uri** and **tag**.  
  * The **uri** is the fully formed route of your cities-services application.
    * HINT: `cf apps` is your friend for finding the routes of your apps  
    * HINT: The route you provide needs to be well formed - http://[route-path-goes-here]
  * The **tag** is literally the word `cities`, no magic there.  
  * The `cf create-user-provided-service` can be run interactively or by providing well formed json.  **Windows users should use interactive mode**
    * Interactive mode: `-p "uri, tag"` (exactly as written)
    * Non-Interactive mode: `-p '{"uri":"<route>","tag":"cities"}'` with the complete JSON string with your route.
5. Remember to bind the user provide service to your UI application
6. Restage your UI application to pick up the changes.  
7. You should be able to validate by connecting to the UI app's route in your browser.
8. Check out the environment variables for your application to see what the user provide service looks like (hint: we talked about this in Section 3).

## Creating an environment variable

### Exercise
1. Be sure you are targeted to your **development** space.
2. Set an environment variable of `LOG_LEVEL=debug` using the `cf set-env` command.
3. `cf push` your application again.
4. Take a look at your application's environment to see what the environment variable looks like.

### Extra Credit Exercise

Add in all the information to the existing manifest for the cities-ui application and needed service.  This way both apps can be pushed with a single `cf push` command.

[pivotal.io - Describing Multiple Applications with One Manifest](http://docs.pivotal.io/pivotalcf/devguide/deploy-apps/manifest.html#multi-apps)

### Would you like to know more?  

[12 Factor : Config](http://12factor.net/config)

[User Provided Services](http://docs.pivotal.io/pivotalcf/devguide/services/user-provided.html)

[Source code for citites-ui app](https://github.com/krujos/pcf-workshop/tree/master/dev-experience/cities)

[Section 7 - Log and Log Management (and NOT Monitoring) ->](logging.md)
