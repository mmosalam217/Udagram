# Udagram
Udagram is a new interactive social media platform for different types of users who specially like sharing their photographs for nature, adventures and much more.

## Features
1. Registration.
2. Login.
3. Post a photo with a caption.

## Dependencies
- Node.js V16.13.2 LTS
- NPM version 8.3.1
- Angular 8
- AWS CLI Version 2
- Elastic beanstalk CLI (EB CLI) version 3
- PostgreSQL database running on AWS RDS db.t2.micro instance
- Node.js application running on AWS Elastic beanstalk t2.micro instance
- An S3 public bucket configured with website hosting enabled.
- An S3 bucket for storing uploads from Udagram UI.


## Installation
1. Clone this repository using the following command:
```git clone https://github.com/mmosalam217/Udagram.git```
2. Install the frontend packages using the following command in the project root folder:
``` npm run frontend:install```
3. Install the backend packages using the following command in the project root folder:
``` npm run backend:install```

## Build
1. After installation run the following command to build the node.js application:
```npm run backend:build```
An node.js server will be running on port 8080.
2. Build the angular app by hitting the following command:
```npm run frontend:build```

## Test
1. Make sure the app dependenices are installed:
- For Angular:
```npm run frontend:install```
- For node.js:
```npm run backend:install```
2. Hit the following command to start the tests:
```npm run frontend:test```
**Note**:
- There are no tests for the node.js application at the udagram project yet, that is why there isn't a test script for backend.

## Deployment
1. Install and build the application using the commands described in the previous sections.
2. Run the following commands to deploy the application:
    - For frontend use the following command:
    ```npm run frontend:deploy```
    **Result**: The new build files will replace the existing ones on the S3 bucket.
    - For the node.js server run:
    ```npm run backend:deploy```
    **Result**: A new application version will be running on the EB environment.

**Important**: 
When you initalize the eb cli with the command `eb init`, an .elasticbeanstalk folder will be created with a config.yml file inside. We need to copy this file into the cd_configs folder in the root directory of the project.

**Why do we do that?**
- We need to package the node.js build file into a zip file to be able to upload it to EB.
- Using the command `eb deploy` directly, will package the files in the project root folder.
- The node.js application is a subproject in the Udagram project, thats why we need to tell EB that we   need a specific *artifcat folder*, morde details [HERE](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-configuration.html#eb-cli3-artifact)
- We can configure that by adding the deploy artifact property into the config.yml file to point to the path to our build folder.
- As we use the CircleCi elastic-beanstalk orb, we cannot modify the .circleci/config.yml file on the circleci job container directly, that is why we need to copy to replace the config file on the circleci container with the file on our machine.

## Built with:
- [Angular](https://angular.io): Single Page Application Framework
- [Node.js](https://nodejs.org/): Javascript Runtime
- [Express.js](https://expressjs.com/): REST serverside framework build on node.js
- [PostgreSQL](https://www.postgresql.org/): Relational database