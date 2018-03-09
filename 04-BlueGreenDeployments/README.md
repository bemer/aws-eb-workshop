## 1. Tutorial Overview

Now, let's use what we've learned in the previous steps to create a blue/green deployment


In order to run this, you must have completed the following steps:

* [Setup Environment](https://github.com/bemer/aws-eb-workshop/tree/master/01-SetupEnvironment)
* [Deploy a Java Application](https://github.com/bemer/aws-eb-workshop/tree/master/02-DeployJavaApp)
* [Updating your Application](https://github.com/bemer/aws-eb-workshop/tree/master/03-UpdatingApplication)

>NOTE: Since we will execute the blue/green deployment, you will need at least two environments in your application. Please don't forget to create the `prod` environment described [here](https://github.com/bemer/aws-eb-workshop/tree/master/02-DeployJavaApp#4-creating-the-production-environment-with-aws-eb-cli).

## 2. Creating a new application version

Since have two environments (`dev` and `prod`) our goal is to keep these environments with different versions of our application, so we will be able to validate the deployment itself.

In that case, we will need to follow these steps:

* In your `eb-workshop` directory, edit the file `index.jsp`. Go to the line number 76 and change the colors to `6ac9f9`. This is the original color that came with the application. This will be our blue environment.
* Deploy this change with the command `eb deploy` in your production environment.
* After deploying this, change the color back to `01cc49`. This will be our `green` application version. You should now deploy the green into your development environment.

After following this, we will have our `blue` (production) and our `green` (development) environments.

Use the command `eb open` to validate both colors.

>NOTE: Remember that when using the `eb open` command, you can also specify the environment name.

## 3. Listing the URL's

When using the command `eb open` with your environment name, please take note on the URL that it is going to point to.

Your production environment should point to something like `http://<your_name>eb-workshop-prod.us-east-1.elasticbeanstalk.com/` while your development will point to something like `http://<your_name>eb-workshop-dev.us-east-1.elasticbeanstalk.com/`.

## 4. Swapping URL's

In order to run a Blue/Green deployment, we will swap the URL for both environments. To do so, let's use the command `eb swap`.

Note that if we just have two environments, the command will not ask for anything else, but if we have more, it will ask us to point what is the environment that we want to change the URL with.

After executing this command, try to access both URL's again. You should see a different version of the application when using the same link.

You can also check that the URL's were changed using the AWS Console.
