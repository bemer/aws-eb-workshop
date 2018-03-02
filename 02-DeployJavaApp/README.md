## 1. Tutorial overview

This tutorial will guide you through the deployment of an Java Application using the AWS Elastic Beanstalk service. We will be using a sample application provided by Amazon Web Services.

In order to run this tutorial, you must have completed the following steps:

* [Setup Environment](https://github.com/bemer/aws-eb-workshop/tree/master/01-SetupEnvironment)

> NOTE: The `ebcli` can use the AWS credentials from your environment. In order to use it, don't forget to properly configure your awscli, using the command `aws configure` as noted here: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html

## 2. Creating an Application with EB CLI

In Elastic Beanstalk, an application is a logical collection of Elastic Beanstalk components, including environments, versions, and environment configurations. In Elastic Beanstalk an application is conceptually similar to a folder.

The first step here is to create a new folder, that will be our working directory. This directory is going to be named `eb-workshop`. In your terminal, run the following command:

    $ mkdir ~/eb-workshop && cd ~/eb-workshop

Now, let's start a new environment, with the EB CLI. Let's do it using the command:

    $ eb init

With this, the EB CLI will start a new environment locally, and will ask you a few questions. The first one is in which do you want to deploy your application. The default option is 3, but we will be using 1. In this step, type `1` and press enter:

    Select a default region
    1) us-east-1 : US East (N. Virginia)
    2) us-west-1 : US West (N. California)
    3) us-west-2 : US West (Oregon)
    4) eu-west-1 : EU (Ireland)
    5) eu-central-1 : EU (Frankfurt)
    6) ap-south-1 : Asia Pacific (Mumbai)
    7) ap-southeast-1 : Asia Pacific (Singapore)
    8) ap-southeast-2 : Asia Pacific (Sydney)
    9) ap-northeast-1 : Asia Pacific (Tokyo)
    10) ap-northeast-2 : Asia Pacific (Seoul)
    11) sa-east-1 : South America (Sao Paulo)
    12) cn-north-1 : China (Beijing)
    13) cn-northwest-1 : China (Ningxia)
    14) us-east-2 : US East (Ohio)
    15) ca-central-1 : Canada (Central)
    16) eu-west-2 : EU (London)
    17) eu-west-3 : EU (Paris)
    (default is 3): 1

Now, it will ask you to enter the application name. You will note that the EB CLI will use the directory name, which is `eb-workshop`. In this case we can leave the defaul, so just press enter:

    Enter Application Name
    (default is "eb-workshop"):

The EB CLI will provide you the information telling that the application has been created:

    Application eb-workshop has been created.

Now, let's choose the platform that we want to use. Since this is a Java Application, we can select the option `5`:

    Select a platform.
    1) Node.js
    2) PHP
    3) Python
    4) Ruby
    5) Tomcat
    6) IIS
    7) Docker
    8) Multi-container Docker
    9) GlassFish
    10) Go
    11) Java
    12) Packer
    (default is 1): 5

Select now the platform version, that will be `Tomcat 8 Java 8`:

    Select a platform version.
    1) Tomcat 8 Java 8
    2) Tomcat 7 Java 7
    3) Tomcat 7 Java 6
    4) Tomcat 7
    5) Tomcat 6
    (default is 1): 1

In this stage, EB CLI will ask you if you want to enable `ssh` to your instances. For this lab, this is not mandatory, so just type `n` and press enter:

    Do you want to set up SSH for your instances?
    (Y/n): n

## 3. Creating an Development Environment with EB CLI

An environment is a version that is deployed onto AWS resources. Each environment runs only a single application version at a time, however you can run the same version or different versions in many environments at the same time. When you create an environment, Elastic Beanstalk provisions the resources needed to run the application version you specified.

Let's them use EB CLI to create the first environment for our application, that will be the `development` environment.

First of all, we will need to get the application that we are going to deploy in this environment. Since we will be using a sample Java application, let's download it to our current directory using the following command:

    $ curl -o java-tomcat-v3.zip 'https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/samples/java-tomcat-v3.zip'

Now, run the command `eb create` to start the creation of our first environment.

Kepp the Environment Name and the CNAME Prefix as `eb-workshop-dev`:

    $ eb create
    Enter Environment Name
    (default is eb-workshop-dev):
    Enter DNS CNAME prefix
    (default is eb-workshop-dev):

For the load balancer type, keep the option `1`. We will be using the classic load balancer:

    Select a load balancer type
    1) classic
    2) application
    3) network
    (default is 1):

The EB CLI will them upload your .zip file to the S3 and will start the deployment of your application into the development environment.
