# Udagram Pipeline
![CircleCI](https://img.shields.io/circleci/build/github/mmosalam217/Udagram?token=c49a401c089fc00ac820b5806b8acb5ba5ffa7f9)

As CI/CD platform we have choosen CircleCi to run our CI/CD pipline.

Our workflow contains 4 jobs, 2 build and 2 deployment jobs for each of the UI and backend applications.

Each deploy job depends on the build job for the same application, for example; the deploy job for frontend won't run unless the build is succeeded.

The two pairs run in parallel to save time as long as launching the frontend application to production does not depend on the backend status.

## Dependencies (Orbs)
  - node: circleci/node@5.0.0
  - aws-cli: circleci/aws-cli@2.0.6
  - eb (elastic beanstalk cli): circleci/aws-elastic-beanstalk@2.0.1

## Jobs
### Frontend:
1. **build-frontend:**
    The goal of this job is to simply install the dependecies for the Angular application.
    It runs the following two commands and persist the output into the disk so that the deploy job can use them later on as we need the build file generated from that job:
    ```npm run frontend:install```
    ```npm run frontend:build```
2. **deploy-frontend:**
    This job runs after the build job has succeeded. It pushs the build files generated from the *build-frontend* job using the command:
    ```npm run frontend:deploy```
### Backend
1. **build-backend:**
    The goal of this job is to simply install the dependecies for the node.js server.
    It runs the following two commands and persist the output into the disk so that the deploy job can use them later on as we need the build file generated from that job:
    ```npm run backend:install```
    ```npm run backend:build```
2. **deploy-backend:**
    - This job requires the *build-backend* job to be successful.
    - It uses the `eb init` command to initialize the EB env on the running, otherwise EB CLI on the CircleCi container will throw an error that we cannot run `eb deploy` without the init command first.
    - We use then the following command to replace the config file created from the `eb init` command. The reason for that is mentioned in the *README* file of the project under the *Deployment* section.
    - We finally run the `eb deploy env-name` command to push the build artifact into our Elastic beanstalk environment.


## Environment Variables
- AWS_ACCESS_KEY_ID: *your aws access id*
- AWS_DEFAULT_REGION: *your aws region*
- AWS_SECRET_ACCESS_KEY: *your aws access key*
- EB_APPLICATION_NAME: *the name of your application*