[Section 3 - Deploying a Backend Application](BackendService.md) | [PCF Home](README.md) | [Section 5 - Manifest And Buildpacks](manifest.md)

# Section 4 - Ready for Acceptance Testing (ie code promotion)

## Overview

If you remember from our overview, we setup two spaces, development and acceptance.  Now that we have our application ready, we are ready to deploy it to the acceptance space.  

## Code promotion

### Exercise

1. Target your **acceptance** space
2. Using the cities-services.jar file that you downloaded in Section 3, deploy that application to your **acceptance** space.
  * Remember to prepend your user id to the application name.
  * If you get a route conflict, remember what we mentioned about routes in Section 2.
3. Seeing a familiar pattern with the application failing?  Remember to check your logs.
4. The error message in the logs should look familiar.  It is the same error message that you got when deploying to your development space.  
5. Check to see if you have a MySQL service in your **acceptance** space.
  * You should notice that you don't have any services.  This is because like applications, services are bound to a particular space.  
6. Create a MySQL instance in your **acceptance** space.
7. Bind your MySQL instance to your application and restage.
8. Confirm that your application is now working by hitting the URL in your browser.

[Section 5 - Manifest And Buildpacks ->](manifest.md)
