<<<<<<< HEAD
# realMethods DevOps Project Generator Orb
=======
# realMethods Project Generator Orb
>>>>>>> origin/master

![alt text](http://www.realmethods.com/img/_circleci_realmethods_orb_v2.png)

<<<<<<< HEAD
The realMethods Orb is a simple, yet powerful way for you to leverage CircleCI to automate the generation of DevOps projects to produce MVP-quality applications that can be deployed to, tested, and run through your CircleCI pipeline.
=======
Looking for more than Hello World?  The realMethods Orb is a simple, yet powerful way for you to leverage CircleCI to automate the generation of any DevOps project including MVP-quality source code that can be deployed to, tested, and run through your CI/CD pipeline on CircleCI.
>>>>>>> origin/master


#### Version
    version: 2.1

#### Orb Declaration
    orbs:
    realmethods: realmethods/appgen@2.0.0

#### Job Declaration
    jobs:
      generate-app:
        docker:
          - image: 'circleci/node:latest'
        steps:
          - realmethods/initialize:
              api-token: "Use DsJqTpYht3LcKb80 or PUT_YOUR_API_TOKEN_HERE"

A general CircleCI user account has been created resulting in user token DsJqTpYht3LcKb80.  If you prefer your own token, click [here](platform.realmethods.com) to subscribe then create an account and access your unique generated API token.

#### Workflows
	workflows:
		version: 2
		app-gen-workflow:
			jobs:
			- generate-app

## DevOps Project Generation Configuration Examples 

To invoke project generation, one mandatory YAML file is required . __These files are referenced from the root of your Git repository since they are being accessed from the Orb__.

Visit [https://github.com/realmethods-public/orb](https://github.com/realmethods-public/orb) to view all sample model and YAML configuration files.


#### generation-yaml-file (__mandatory__):
  
This YAML file contains the directives required to generate an application using a model identifier (by id or file_path), technology stack (by id or name), application options file, Git repo params or more.  
  
* Learn more [here](http://www.realmethods.com/cli.html#applicationgenerationconfigurationparameters). 
* See project-as-code examples [here](https://github.com/realmethods-public/orb/blob/master/samples/yamls/project.as.code)

`NOTE: Use one of the project-as-code examples as a starting point.  Fill it out and replace existing values with those relevant to your project.`
  
#### Known Issue
	
During the first run of a build, from time to time the following issues has been observed:
	
``Cannot find a job named build to run in the jobs: section of your configuration file.  If you expected a workflow to run, check your config contains a top-level key called workflows:``

The problem appears to be quickly fixed if the config.yml file in the repository is touched (e.g. by making a whitespace only change).
[Read more](https://discuss.circleci.com/t/if-you-expected-a-workflow-to-run-check-your-config-contains-a-top-level-key-called-workflows/16798) in this related CircleCI thread

#### Stack Specific Examples

Note: If using one of the AWS Lambda tech stacks, you will have to assign the access key and secret key as project level environment variables.  See https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project for more details. Be sure to name the accesskey USER\_AWS\_ACCESSKEY and name the secretkey USER\_AWS\_SECRETKEY.  Equally important, 
make sure you have the correct policies assigned for the related user (_AWSCodeDeployRoleForLambda, AWSLambdaExecute, AWSLambdaRole_, etc..)

#### Apollo GraphQL
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/apollo-project-as-code.yml"

#### Angular7          
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/angular-project-as-code.yml"

#### ASP.NET          
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/aspdotnet-project-as-code.yml"

#### Django
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/django-project-as-code.yml"

#### Spring Boot using MongoDB
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/springboot-mongodb-project-as-code.yml"

           
#### Spring Boot using MySQL          
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/springboot-rdbms-project-as-code.yml"

#### Spring Boot using MongoDB
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/springboot-mongodb-project-as-code.yml"
           
#### Spark Microweb using MySQL
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/sparkmicroweb-project-as-code.yml"

#### Google Functions          
      - realmethods/generate_devops_project:
         generation-yaml-file: "samples/yamls/project.as.code/googlefunctions-project-as-code.yml"


#### Struts2 using MySQL
      - realmethods/generate_devops_project:
          generation-yaml-file: "samples/yamls/project.as.code/struts-rdbms-project-as-code.yml"

