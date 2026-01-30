# Jenkins User & Permission :

## Create credentials (Username & Password):

Manage Jenkins > Credentials > System > Global Credentials

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/0f947a4f2a03bf039a9f55e50d5b746365369a6b/4%20Jenkins_User_%26_Permission/images/jenkins_credential1.png)
Here we use username = docker token user name, password= token password.

Now, How to use in a pipeline ?


### Create a pipeline :

Pipeline Syntax > withCredentials: Bind credentials to variables > (set username and password for variable) > Generate pipeline script > (Copy the script and paste on pipeline script > 

[ credential2 ]


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



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## User Permission for specific types of  pipeline :

#### Step 1 :
Create a user :
[userPipeline1]

#### Step 2 :
Create a role & give permission :
[userPipeline2]

#### Step 3 :
Assign role (bind user with a role) :
[userPipeline3]

#### Step 4 :
[Settings > Manage & Assign roles > Assign roles > Item roles]


Create a item role (In pattern write pipeline common name, example: "intern.*") :
[userPipeline4]

#### Step 5 :
Assign role(item role) :
[userPipeline5]


#### Step 6 :

Now we login to this user & we only can see "intern' pipelines :
[userpipeline6]
