[Topic 3 - GitHub & Git Basics](../git.md) | [Home](../README.md) | [Topic 5 - Production Deployment](../production_deployment.md)

# Topic 4 - Cloud Foundry

## Prerequisite
* Basic GitHub experience
* Git CLI or GitHub client

## Overview  
**Presentation** [Keynote](pcf-intro-immersion.key) | [PowerPoint] (pcf-intro-immersion.pptx) | [PDF](pcf-intro-immersion.pdf)

Some key points regarding Cloud Foundry structure -
* Organizations and Spaces
  * Cloud Foundry has two levels of structure allowing developers to define the environment(s) and provide isolation.
    * Organizations are the top level structure.  Organizations should be used to group like applications together around a common business function.  Resource quotas are set at the organization level.
    * Spaces are groups inside of an organization that provide further granularity and structure.  Applications and services are deployed to a space and can not be directly deployed to an organization.  Spaces can be used to provide lifecycle segmentation, developer sandboxing, application grouping,  etc.
    * At a minimum, your organization must contain one space.
* User Roles
  * Organization Roles
    * Org Manager
    * Org Auditor
  * Space Roles
    * Space Manager
    * Space Developer
    * Space Auditor
  * Please see the [Pivotal Documentation](https://docs.cloudfoundry.org/concepts/roles.html)  for more details on the functionality of these roles.

## Sections
* [Section 1 - CLI](CLI.md)
* [Section 2 - Deploying and Scaling an Application](DeployingBasics.md)
* [Section 3 - Deploying a Backend Application (db, backend app)](BackendService.md)
* [Section 4 - Manifest And Buildpacks](manifest.md)
* [Section 5 - User Provided Services (UPS) and Environment Variables](userprovidedservice.md)
* [Section 6 - Log and Log Management (and NOT Monitoring)](logging.md)
