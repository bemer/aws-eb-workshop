# Creating a CI/CD Pipeline on AWS for Elastic Beanstalk

In this section you will create a CI/CD Pipeline on AWS for a java application using CodeCommit, CodeBuild, CodeDeploy and CodePipeline. This application will be deployed on Elastic Beanstalk.


## 1) Create a Git Repository

On the AWS console, go to the CodeCommit page and click on the Create Repository Button.
Choose a repository name and create it. You can skip the next step.

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