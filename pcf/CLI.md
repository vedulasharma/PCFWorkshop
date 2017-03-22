[PCF Home](README.md) | [Section 2 - Deploying](DeployingBasics.md)

# Section 1 - CLI

## Overview

The preferred method of interacting with Cloud Foundry is the command line interface (CLI).  This method provides the user all the functionality that is available to them.  While you may interact with Pivotal Cloud Foundry using the developer console UI, this course will focus on using the CLI to help reenforce its functions.

## Creating an Organization

* Log into [https://login.run.pivotal.io/](https://login.run.pivotal.io/)
* Click on, "Pivotal Web Services"
* On the left side of the screen, you will see a header called **ORG** under which is a link to **Create a New Org**.  
* Enter organization name and click **Ok**.

## Installing CLI and Logging In

If you don't have the CLI already installed, you can download and install it from [here](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html).

Some key commands that you need to get familiar with that will make your experience with Cloud Foundry easier.

* `cf help`
  * This command will list all the commands available in the CLI.  Note - based upon your access level, you may not have the rights to run specific commands.  
* `cf <command> -h`
  * Based on the command given, this will give help for the specific command you selected such as flags or arguments required.
* `cf login`
  * This is how log into Cloud Foundry.  Any commands ran after logging in will be executed against the API host provided in the login command using your session credentials.
* `cf target`
  * This allows you to specify an organization and/or space you would like to work in.  

### Exercise
1. Log into your PCF environment - the API host is `api.run.pivotal.io`. 
2. Run a `cf target` to confirm that you are in the organization that you created earlier.  
  1. If you are already part of another organization, use `cf target` to target the organization you created earlier.

## Creating Spaces

As we discussed earlier, spaces allow an application team to define their organizations.  Additionally, you can only deploy applications and services to a space.

For our example, we will structure our organization into a **development** space and **acceptance** space.  Our **development** space is where you as a developer will rapidly develop and deploy to test your code.  Once a feature is ready for Product Owner sign off, it should be pushed to the **acceptance** space.  This allows the Product Owner validation not to impact developer productivity as they are working in separate spaces.

### Exercise

1. Verify the **development** space exists using the `cf spaces` command.
2. Create a **acceptance** space using the `cf create-space` command.
  * If you are curious about the required arguments, remember the `-h` flag to get help.
2. Run a `cf spaces` to confirm that your new spaces were created. (You should have a development and acceptance space)

[Next Section - Deploying ->](DeployingBasics.md)
