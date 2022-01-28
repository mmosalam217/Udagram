# Description
Udagram is built based on a three tier archeticture composed of a relational database, an express (node.js) api and an angular frontend web application.

## System Components
- Database: PostgreSQL
- RESTful API: Express/Node.js
- Frontend Web Application: Angular 8+

### PostgreSQL Database
Our choice of a relational database has been postgreSQL. It is a strong, fast, well-known and open-source relational database, [see more](https://www.postgresql.org/).

#### System Specification
- **Cloud Provider**: *AWS RDS*
- **Instance**: *db.t2.micro*
- **RAM**: *1 GB*
- **Storage**: *20 GiB SSD*

### Express (Node.js) API
For our backend servers we have choosen express.js, an open-source http framework built on top of node.js known to be asynchronus, fast and reliable, [more details](https://expressjs.com/).

#### System Specification
- **Cloud Provider**: *AWS Elastic Beanstalk (EB)*
- **Instance**: *t2.micro*
- **RAM**: *1 GiB*
- **Storage**: *AWS S3 (Simple Storage Service*

#### Environment Variables
- AWS_BUCKET: *uploads bucket*
- AWS_REGION
- JWT_SECRET
- POSTGRES_DB
- POSTGRES_HOST
- POSTGRES_USERNAME
- POSTGRES_PASSWORD
- POSTGRES_PORT
- Optional: PORT (can be excluded as EB runs the instance on port 8080)

### Udagram UI: Angular Web Application
We built our frontend web application using Angular framework. Angular is a very strong, feature-rich and well-structured typescript framework, for more info visit the [Angular](https://angular.io) website.

#### System Specification
- **Host**: *AWS S3 Static Website Hosting*
- **URL**: *http://udagramweb.s3-website-us-east-1.amazonaws.com/*