# Updating your Application

**Quick jump:**

* [1. Tutorial overview](https://github.com/bemer/aws-eb-workshop/tree/master/03-UpdatingApplication#1-tutorial-overview)
* [2. Updating the Application](https://github.com/bemer/aws-eb-workshop/tree/master/03-UpdatingApplication#2-updating-the-application)
* [3. Deploying the new application version](https://github.com/bemer/aws-eb-workshop/tree/master/03-UpdatingApplication#3-deploying-the-new-application-version)
* [4. Getting information about the version](https://github.com/bemer/aws-eb-workshop/tree/master/03-UpdatingApplication#4-getting-information-about-the-version)
* [5. Performing a Rollback](https://github.com/bemer/aws-eb-workshop/tree/master/03-UpdatingApplication#5-performing-a-rollback)


## 1. Tutorial overview

In this chapter we are going to execute an update in the application and a deploy of the new application version in our development environment.

In order to run this, you must have completed the following steps:

* [Deploy a Java Application](https://github.com/bemer/aws-eb-workshop/tree/master/02-DeployJavaApp)

## 2. Updating the Application

Since we have the application source code in our computer, let's start changing something in it. Since this is a very simple application, let's change something in the frontend layer.

Using a text editor of your choice, open the file `index.jsp` located in the `~/eb-workshop/` directory. Change the line `76` from:

    background-image: -webkit-gradient(radial, 0 0, 1, 0 0, 500, from(#6ac9f9), to(#0188cc));

To:

    background-image: -webkit-gradient(radial, 0 0, 1, 0 0, 500, from(#01cc49), to(#01cc49));


After this, just save the file.

## 3. Deploying the new application version

Now, let's deploy the new version of our application in the `development` environment.

When working with AWS Elastic Beanstalk, we can create new versions of our applications and tag these versions. It makes easy to perform rollbacks and keep track of the versions that we are deploying in our environments.

To create a new deployment of our application, let's use the command:

    $ eb deploy --label green --message "Changing the color from Blue to Green"

Wait a few seconds until the application is deployed in your development environment. When the update is finished, you should see in your terminar something like this:

    $ eb deploy --label green --message "Changing the color from Blue to Green"
    Creating application version archive "green8".
    Uploading eb-workshop/green8.zip to S3. This may take a while.
    Upload Complete.
    INFO: Environment update is starting.                               
    INFO: Deploying new version to instance(s).                         
    INFO: New application version was deployed to running EC2 instances.
    INFO: Environment update completed successfully.

Now, let's access our new application version with the command:

    $ eb open

Note that the new version of our application is now deployed and the back just changed from the color Blue to Green.

## 4. Getting information about the version

After changing our code and deploying these changes to our environment, we can also get more information about it. In order to see the versions deployed into our environment, we can use the following command:

    $ eb appversion

Here, we will be able to identify all the versions previously deployed in our environment with all the informations:

    Current version # deployed: 2

     #    Version Label       Date Created       Age       Description
     2    green               2018/03/02 14:49   9 mins    Changing the color from Blue to Green  
     1    app-180302_113415   2018/03/02 11:34   3 hours   EB-CLI deploy                          

    (Commands: Quit, Delete, Lifecycle, ▼ ▲ ◀ ▶)

## 5. Performing a Rollback

If you want to execute a rollback in a deploy, you can also use the information provided by the previous command. In our example, we have two version of the same application. The first one has the label `app-180302_113415` and was created when we executed the first deploy, and the second one with the label `green` created in this chapter.

To see how the rollback process works, let's redeploy our blue version. To do that, we need to use the following command:

    $ eb deploy --version app-180302_113445

>NOTE: when using the command `eb deploy` to perform a rollback, you need to use the `--label` option and then inform the `Version Label` of the version that you want to deploy. Because of that, a good practice is always inform a description when executing your deployments.

Let's access our application and see if the rollback went successfully:

    $ eb open

We should see the version with the blue color.

To go back to the `green` version, let's execute the same, changing the `Version Label`:

    $ eb deploy --version green

We should have the `green` version running again.
