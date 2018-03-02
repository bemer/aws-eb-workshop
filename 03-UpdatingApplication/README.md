## 1. Tutorial overview

In this chapter we are going to execute an update in the application and the deploy of the new version in our development environment.

In order to run this, you must have completed the following steps:

* [Deploy a Java Application](https://github.com/bemer/aws-eb-workshop/tree/master/02-DeployJavaApp)

## 2. Updating the Application

Since we have the application source code in our computer, let's start changing something in it. Since this is a very simple application, let's change something in the frontend layer.

Using a text editor of your choice, open the file `index.jsp` located in the `~/eb-workshop/` directory. Change the line `76` from:

    background-image: -webkit-gradient(radial, 0 0, 1, 0 0, 500, from(`#6ac9f9`), to(#0188cc));

To:

    background-image: -webkit-gradient(radial, 0 0, 1, 0 0, 500, from(`#01cc49`), to(`#01cc49`));


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
