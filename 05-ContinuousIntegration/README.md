# Creating a CI/CD Pipeline on AWS for Elastic Beanstalk

In this section you will create a CI/CD Pipeline on AWS for your java application using CodeCommit, CodeBuild, CodeDeploy and CodePipeline. This application will be deployed on Elastic Beanstalk.


## 1) Create an AWS CodeCommit repository

AWS CodeCommit is a fully-managed source control service that makes it easy for companies to host secure and highly scalable private Git repositories.

In order to start using it, let's open the AWS Console and in the `CodeCommit` screen click in the `Get started` Button:

![code-commit-gettingstarted](https://github.com/bemer/aws-eb-workshop/blob/master/05-ContinuousIntegration/images/ccgetstarted.png)

Now, choose a repository name and click in `Create repository`:

![create-repository](https://github.com/bemer/aws-eb-workshop/blob/master/05-ContinuousIntegration/images/create-repository.png)

In the `Configure email notifications` screen, just click in `Skip`.

After creating our repository, AWS CodeCommit is going to show how to start working with the repository itself. You will need to follow the steps in this screen, in order to have an IAM user that can use your new repository.

![code-commit-instructions](https://github.com/bemer/aws-eb-workshop/blob/master/05-ContinuousIntegration/images/code-commit-instructions.png)

After executing all these steps, you will clone your repository inside your home folder.

>NOTE: Remember to not clone your repository inside your application folder.

When cloning your repository, you will have a new folder named just as your repository. Now, you will copy all your application files from the directory. You can use the following command:

    cp -r eb-workshop/* eb-workshop-app/

After copying your application files let's run the following commands to execute our first commit:

    cd eb-workshop-app/
    git add --all
    git commit -m 'First commit'
    git push

This will send our source code to the new repository on CodeCommit.
You can check your source code in your repository looking at the AWS Console:

![checking-commit](https://github.com/bemer/aws-eb-workshop/blob/master/05-ContinuousIntegration/images/checking-commit.png)


## 2) Clone the repository

The first time that you enter on the environment page, you will have a tutorial to clone your reposity locally.

Go to your command line tool and do the command as the example:

git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/TESTECICD

## 3) Copy the source code from section 02-DeployJavaApp, add, commit and push.

Localize the files extracted from the java-tomcat-v3.zip file. Copy all the content from the file into the repository folder created on the previous step.

        cp -r ~/Downloads/java-tomcat-v3/* .

after this, you have to push the code to the git repository.

        git add *
        git commit -m "first commit"
        git push

Now the sourcecode is available on your git repo.

## 4) Create a CodePipeline project

Go to the CodeBuild product page in your AWS Console.
Click on the Get Started button.
Choose a Project Name, Select the Source provider as you CodeCommit Repository created on step 03.
On the build provider, create a new project, select CodeBuild, choose the operating system as Ubuntu, the runtime as Java and the runtime version as openjdk-8, leave the remaing values on default and click on the save and build button. Click on Next.
On the Deploy step, select AWS Elastic Beanstalk as the provider and select the environtment and application that you created on section  02-DeployJavaApp.
The the AWS Service Role part, click on the Create Role button, leave all fields default and click on the Allow Button.
Review what you just did and click Create Pipeline.
