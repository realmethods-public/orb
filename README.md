# realMethods Application Generator Orb

![alt text](http://www.realmethods.com/img/circleci_realmethods_orb_.png)

The realMethods Orb is a simple, yet powerful way for you to leverage CircleCI to automate the generation of MVP-quality applications that can be deployed to, tested, and run through your CI/CD pipeline on CircleCI.


#### Version
    version: 2.1

#### Orb Declaration
    orbs:
    realmethods: realmethods/appgen@1.0.1

#### Job Declaration
    jobs:
      generate-app:
        docker:
          - image: 'circleci/node:latest'
        steps:
          - realmethods/initialize:
              api-token: "PUT_YOUR_API_TOKEN_HERE"

Click [here](http://www.realmethods.com/developer.html) to create an account and access a unique API token.

#### Workflows
	workflows:
		version: 2
		app-gen-workflow:
			jobs:
			- generate-app

## Application Generation Configuration Examples 

To invoke application generation, one mandatory file is required, along with three optional files the mandatory file can reference.  If any of the option files is included as an input argument, the related internal reference of the mandatory is ignored. __These files are referenced from the root of your Git repository since they are being accessed from the Orb__.

Visit [https://github.com/realmethods-public/orb](https://github.com/realmethods-public/orb) to view all sample model and config files.

[Click here](https://www.realmethods.com/cli.html#config-files) to learn more about configuration files and settings.


#### generation-yaml-file (__mandatory__):
  
This YAML file contains the directives required to generate an application using a model identifier (by id or file_path), technology stack (by id or name), application options file, Git repo params or more.  
  
* Learn more [here](http://www.realmethods.com/cli.html#applicationgenerationconfigurationparameters). 
* See an example [here](https://github.com/realmethods-public/orb/blob/master/samples/yamls/generate-django.yml)
  
#### git-params-file (__optional__):
    
This optional YAML file contains one or more groupings of parameters to control committing an application's files (language   specific source code, build files, config files, CI/CD files, etc..) to a Git repository. If this argument is not provided, the _gitParams-->file_ param of the _generation-yaml-file_ is used.  
  
* Learn more [here](http://www.realmethods.com/cli.html#http://www.realmethods.com/cli.html#githubconfigurationparameters).
* See an example [here](https://github.com/realmethods-public/orb/blob/master/samples/git/test.git.yml)

#### app-options-file (__optional__):  
  
This optional JSON file contains one or more groupings of parameters to control application generation flow and actual output. This file is where you would provide such things as database access params, application params (name, description, etc..), and so forth. If this argument is not provided the _appOptionsFile_ param of the _generation-yaml-file_ is used.  
  
* Learn more [here](http://www.realmethods.com/cli.html#http://www.realmethods.com/cli.html#appconfigurationparameters).
* See an example [here](https://github.com/realmethods-public/orb/blob/master/samples/options/Django.options.json)

#### model-identifier (__optional__):  
A model identifier can be a model file ([see supported models](http://www.realmethods.com/api.html#supportedmodels)) or the realMethods identifier of a previously used/published model. If this argument is not provided the _modelId_ param of the  _generation-yaml-file_ is used.  
  
* Learn more [here](http://www.realmethods.com/cli.html#applicationgenerationconfigurationparameters).
* Learn about [supported models](http://www.realmethods.com/models.html).
* See an example [here](https://github.com/realmethods-public/orb/blob/master/samples/models/reference_management.xmi)


#### Stack Specific Examples

Note: If using one of the AWS Lambda tech stacks, you will have to assign the access key and secret key as project level environment variables.  See https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project for more details. Be sure to name the accesskey USER\_AWS\_ACCESSKEY and name the secretkey USER\_AWS\_SECRETKEY.  Equally important, 
make sure you have the correct policies assigned for the related user (_AWSCodeDeployRoleForLambda, AWSLambdaExecute, AWSLambdaRole_, etc..)

##### Django
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-django.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/Django.options.json"
          model-identifier: "samples/models/reference_management.xmi"
          
##### Angular7          
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-angular.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/Angular7MongoDB.options.json"
          model-identifier: "samples/models/reference_management.xmi"          

##### ASP.NET          
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-aspdotnet.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/ASPNETCore.options.json"
          model-identifier: "samples/models/reference_management.xmi"
          
##### Google Functions          
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-googlefunctions.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/GoogleFunctions.options.json"
          model-identifier: "samples/models/reference_management.xmi"
           
##### AWS Lambda using MySQL       
   
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-lambdacore.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/Lambda.options.json"
          model-identifier: "samples/models/reference_management.xmi"
           
##### AWS Lambda using MongoDB
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-lambdanosql.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/LambdaNoSQL.options.json"
          model-identifier: "samples/models/reference_management.xmi"
           
##### Spring Boot using MySQL          
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-springcore.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/SpringCore.options.json"
          model-identifier: "samples/models/reference_management.xmi"
            
##### Spring Boot using MongoDB
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-springnosql.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/SpringMongoDB.options.json"
          model-identifier: "samples/models/reference_management.xmi"
 
##### Struts2 using MySQL
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-struts2.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/Struts2.options.json"
          model-identifier: "samples/models/reference_management.xmi"
 
##### Spark Microweb using MySQL
      - realmethods/generate_app:
          generation-yaml-file: "samples/yamls/generate-sparkmicroweb.yml"
          git-params-file: "samples/git/test.git.yml"
          app-options-file: "samples/options/remote/SparkMicroWeb.options.json"
          model-identifier: "samples/models/reference_management.xmi"
 
