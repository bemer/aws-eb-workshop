# Setup Environments

This section describes the hardware and software needed for this workshop, and how to configure them. This workshop is designed for a BYOL (Brying Your Own Laptop) style hands-on-lab.

## Hardware & Software

- Memory: At least 4 GB+, strongly preferred 8 GB
- Operating System: Mac OS X (10.10.3+), Windows 10 Pro+ 64-bit, Ubuntu 12+, CentOS 7+.

> NOTE: An older version of the operating system may be used. The installation instructions may differ slightly in that case and are explained in the next section.

## The Elastic Beanstalk Command Line Interface (EB CLI)

The EB CLI is a command line interface for Elastic Beanstalk that provides interactive commands that simplify creating, updating and monitoring environments from a local repository. Use the EB CLI as part of your everyday development and testing cycle as an alternative to the AWS Management Console.

> NOTE: The current version of the EB CLI has a different base set of commands than versions prior to version 3.0. See EB CLI 2.6 (Deprecated) if you use an older version.

Once you've installed the EB CLI and configured a repository, you can create environments with a single command:

  ~/my-app$ eb create my-env

Previously, Elastic Beanstalk supported a separate CLI that provided direct access to API operations called the Elastic Beanstalk API CLI. This has been replaced with the AWS CLI, which provides the same functionality but for all AWS services' APIs.

With the AWS CLI you have direct access to the Elastic Beanstalk API. The AWS CLI is great for scripting, but is not as easy to use from the command line because of the number of commands that you need to run and the number of parameters on each command. For example, creating an environment requires a series of commands:

  ~$ aws elasticbeanstalk check-dns-availability --cname-prefix my-cname
  ~$ aws elasticbeanstalk create-application-version --application-name my-application --version-label v1 --source-bundle S3Bucket=my-bucket,S3Key=php-proxy-sample.zip
  ~$ aws elasticbeanstalk create-environment --cname-prefix my-cname --application-name my-app --version-label v1 --environment


## Install AWS CLI

During this workshop we will interact with some AWS API's. Having the latest version of the AWS CLI in your computer is appropriated.

Instructions to install the AWS CLI are available here: http://docs.aws.amazon.com/cli/latest/userguide/installing.html

## Install git

Sometimes will be easier if you just clone this repo, instead of copying the files. Having the git installed is not a mandatory requisite, but it may help you.

Download and install here: https://git-scm.com/downloads
You can have more information about git here: https://git-scm.com/book/en/v1/Getting-Started
