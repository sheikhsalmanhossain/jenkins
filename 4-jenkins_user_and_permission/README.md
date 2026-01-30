# Jenkins User & Permission :

## Create credentials (Username & Password):

Manage Jenkins > Credentials > System > Global Credentials

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/jenkins_credential1.png)
Here we use username = docker token user name, password= token password.

Now, How to use in a pipeline ?


### Create a pipeline :

Pipeline Syntax > withCredentials: Bind credentials to variables > (set username and password for variable) > Generate pipeline script > (Copy the script and paste on pipeline script > 

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/jenkins_credential2.png)


# User Management In Jenkins :


Plugin Required :

1) Role-Based authorization strategy plugin.
2) Enable it from security section.


Install Plugin :

Settings > plugins > Available Plugins > Role-based authorization strategy > Install


Enable from security section :

1) Settings > security > Authorization > Role based > Role-based strategy > Save


2) Settings > Manage and Assign roles


### Create user :

Settings > users > Create User

### Add permission to user :

Settings > Manage & Assign roles > Create a role( Roll to add)  > Global roles > Check permissions > save


### Assign role to user :

Settings > Manage & Assign roles > Assign roles > Global roles > Add user > Check role(box) > Save



-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## User Permission for specific types of  pipeline :

#### Step 1 :
Create a user :
![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/userpipeline1.png)

#### Step 2 :
Create a role & give permission :
![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/userpipeline2.png)

#### Step 3 :
Assign role (bind user with a role) :
![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/userpipeline3.png)

#### Step 4 :
[Settings > Manage & Assign roles > Assign roles > Item roles]


Create a item role (In pattern write pipeline common name, example: "intern.*") :
![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/userpipeline4.png)

#### Step 5 :
Assign role(item role) :
![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/userpipeline5.png)


#### Step 6 :

Now we login to this user & we only can see "intern' pipelines :
![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/d4568575f8bbb4c907d6e25d83cb4f9aab0ebdd2/4-jenkins_user_and_permission/images/userpipeline6.png)
