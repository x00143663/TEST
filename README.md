# Google Maps Safest Route
This repository contains overview documentation and project management materials
for the *Google Maps Safest Route* product.
#### In this README
- [Product Overview](#product-overview)
- [Architecture Description](#architecture-description)
- [Deveoper Guide](#developer-guide)
## Product Overview
*Google Maps Safest Route* is a product to help users to display dangerous point on the map and find the distance betwen a provided address and all that dangerous zones.
The product is used by users whitout necesity of sign in so, we have not
created separate applications for diferent user type.
## Architecture Description
### API First Approach
All functionality of the system will be implemented using an API first approach. Back end functionality
is implemented in a REST API that is then called from a smart front end client.
### API Security
JSON Web Token (JWT) will be used to provide API security. Users must login to the system and at login
the app in their device is given a token that must be used for all future interactions. The server
reads the token and only responds to requests that contain a valid token.
### Dashboards and Reports
The System Administrator and the Admin users will have dashboards that allow them to review activity
for the inventory.
### Technology Choices
Technolgy choices are guided by using best of breed, catering for future scalability
and supporting a scalable micro-services architecture. An API first approach is used whereby all services
are initially implemented as REST APIs over which higher level features (including UI) are built.
#### Amazon Web Services
All services and applications are designed to be be deployed to AWS. This facilitates scalability, security and
third party infrastructure management. Within AWS, we make extensive use of AWS higher level services.
Lambda - AWS Lambda allows us to build scalable micro-services, which scale massively while implementing
a useage based charging model.
API Gateway - This is the natural companion to Lambda in terms of exposing services via REST API.
Cognito - This provides user management and security.
Dynamo DB (TBD) - This AWS key value store is used for persistent storage of structured data.
Aurora (TBD) - This is an AWS managed SQL database that may be used instead of or as well as Dynamo DB.
S3 - S3 is a low cost storage option used to store larger artefacts, such as mp3 files.
Polly - Polly is an Amazon service that turns text into lifelike speech,
allowing us to create applications that talk.
![Architectue](diagrams/nualangArch.png)
#### ReactJS
The [React](!https://reactjs.org) framework is used to develop the front end User Interface of
the Nualang product. React is one of the leading Javscript UI frameworks and offers a modular
approach to building User Interfaces. UI components are developed separately and assembled
into a hierarchy to provide the overall user interface.
Generally, our web applications are developed as progressive web apps, so that they render
and behave correctly on both mobile and desktop devices.
#### Storybook
[Storybook](!https://storybook.js.org) is an open source tool for developing UI components in
isolation, that suits the approach used by Fathom in developing UI components separately. With
Storybook, the UI components can be viewed and evaluated in a component gallery prior to being
incorporated into the application.
#### Gatsby
As well as the Apps themselves, there is a static web site that users can visit to learn
more about the product and how to use it. There, we host blogs and tutorials as well as
providing links to the app. By using [Gatsby](!https://www.gatsbyjs.org) as a static site
generator, we provide a very fast site for users while maintaing a familiar development
environment for developers - Gatsby is developed using React and uses React components.
### Environments
As well as the *production* system, there is a *staging* system, so that new
features can be evaluated and tested before being deployed to *production*.
### CI / CD
Continuous Integration / Continuous Deployment will be used to support fast deployment
of new features to production, as they are developed.
## Developer Guide
The NuaLand product source code is stored in a series of `git` repositories hosted by
[gitlab](!https://gitlab.com). As well as providing storage for git repositories, gitlab
has the concept of `groups` that allows related projects to be grouped together. We use
this feature to group all of the NuaLang source code repositories together in the
NuaLang group.
### Repository Organisation
#### Management
The Management repository, where this README lives, contains overview documentation for
the entire product and is the only repsitory that does not contain source code. 
We use gitlab issues to track planned future functionality and bugs. Generally, we use
gitlab issues in the Management repo to track all isues for the product centrally, rather
than using gitlab issue in each of the source code repositories.
#### APIs
Fathom uses an API first methodolgy. What this means in practice is that when we are
adding new functioality, an API is usually the first thing that we define. Our APIs
are developed in NodeJS and implemented as AWS Lambda functions. AWS API gateway is
used to provide a REST API in front of the Lambda function. Each of our APIs is stored
in its own separate git repository. Our naming convention is to use the suffix "-api"
for all API repositories (e.g. courses-api).
#### Static Web Site
The `nualang.com` repository contains the gatsby static web site.
#### User Interface Components
The `ui-compnents` repository is where we independently develop our user interface
components, using storybook to showcase them.
