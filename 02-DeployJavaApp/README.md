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

After downloading the file, extract it's contents to the project folder by using the following command:

    $ unzip java-tomcat-v3.zip

Now, run the command `eb create` to start the creation of our first environment.

Keep the Environment Name as `eb-workshop-dev` and change the CNAME Prefix to something like `<your_name>-eb-workshop-dev`:

    $ eb create
    Enter Environment Name
    (default is eb-workshop-dev):
    Enter DNS CNAME prefix
    (default is eb-workshop-dev): <your_name>-eb-workshop-dev

For the load balancer type, keep the option `1`. We will be using the classic load balancer:

    Select a load balancer type
    1) classic
    2) application
    3) network
    (default is 1):

The EB CLI will them upload your .zip file to the S3 and will start the deployment of your application into the development environment. When if finishes will should see something like this:

    Creating application version archive "app-180302_111708".
    Uploading eb-workshop/app-180302_111708.zip to S3. This may take a while.
    Upload Complete.
    Environment details for: eb-workshop-dev
      Application name: eb-workshop
      Region: us-east-1
      Deployed Version: app-180302_111708
      Environment ID: e-n93pj2upsa
      Platform: arn:aws:elasticbeanstalk:us-east-1::platform/Tomcat 8 with Java 8 running on 64bit Amazon Linux/2.7.6
      Tier: WebServer-Standard-1.0
      CNAME: <your_name>-eb-workshop-dev.us-east-1.elasticbeanstalk.com
      Updated: 2018-03-02 14:17:19.424000+00:00
    Printing Status:
    INFO: createEnvironment is starting.
    INFO: Using elasticbeanstalk-us-east-1-xxxxxxxxxxxx as Amazon S3 storage bucket for environment data.
    INFO: Created security group named: sg-342de842
    INFO: Created load balancer named: awseb-e-n-AWSEBLoa-1C4S90GVTJ8Z2
    INFO: Created security group named: awseb-e-n93pj2upsa-stack-AWSEBSecurityGroup-KZBMAD119HT9
    INFO: Created Auto Scaling launch configuration named: awseb-e-n93pj2upsa-stack-AWSEBAutoScalingLaunchConfiguration-11G0MITIZ02FJ
    INFO: Created Auto Scaling group named: awseb-e-n93pj2upsa-stack-AWSEBAutoScalingGroup-14NXHSYM2BRDQ
    INFO: Waiting for EC2 instances to launch. This may take a few minutes.
    INFO: Created Auto Scaling group policy named: arn:aws:autoscaling:us-east-1:xxxxxxxxxxxx:scalingPolicy:aa34af95-55cd-4a08-af0b-b162ed104c16:autoScalingGroupName/awseb-e-n93pj2upsa-stack-AWSEBAutoScalingGroup-14NXHSYM2BRDQ:policyName/awseb-e-n93pj2upsa-stack-AWSEBAutoScalingScaleDownPolicy-L7E89GFF9Q6K
    INFO: Created Auto Scaling group policy named: arn:aws:autoscaling:us-east-1:xxxxxxxxxxxx:scalingPolicy:4e811fdb-2961-4b49-bf33-4f69afee2f44:autoScalingGroupName/awseb-e-n93pj2upsa-stack-AWSEBAutoScalingGroup-14NXHSYM2BRDQ:policyName/awseb-e-n93pj2upsa-stack-AWSEBAutoScalingScaleUpPolicy-SENK03AP1T4L
    INFO: Created CloudWatch alarm named: awseb-e-n93pj2upsa-stack-AWSEBCloudwatchAlarmHigh-T7DPB3CF10F
    INFO: Created CloudWatch alarm named: awseb-e-n93pj2upsa-stack-AWSEBCloudwatchAlarmLow-ZCA8Z8LM12D7
    INFO: Successfully launched environment: eb-workshop-dev

>NOTE: when executing this setup, Elastic Beanstalk will create everything that your application need to work, such as the Load Balancer, Auto Scaling Group, Security Group, CloudWatch Alarms and so one. You can see all the information about what was created in this list.

After the deployment, you can use EB CLI to open your application in a web browser with the command:

    $ eb open

It will open a web browser window with your Java Application.

## 4. Creating the Production environment with AWS EB CLI

In order to have another environment running your application, you can follow the same steps described in the previous section, but changing the environment name to `eb-workshop-prod`.

Also, don't forget to change the CNAME prefix to something similar to `<your_name>-eb-workshop-prod`.

After creating the new environment, you will be able to list the current environments with the command:

    $ $ eb list
    \* eb-workshop-dev
    eb-workshop-prod

>NOTE: note that there is a `*` in front of your development environment. It means that every command executed in your terminal will be applied in this environment.

## 5. Playing with the EB CLI
