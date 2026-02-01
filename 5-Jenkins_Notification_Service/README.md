# Email Notification via Jenkins With AWS SES :


![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/AWS-SES.jpg)

## Setup SES :
### Steps :
#### 1) Create an EC2 instance & install Jenkins

#### 2) Go to SES dashboard check SMTP settings:

Amazon SES > SMTP Settings > SMTP Endpoint

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/smtp-endpoint.png)

#### 3) Add verified identities:

Amazon SES > Configuration > Identities > Create Identity > email address > create identity.

(Create temporary Email : https://temp-mail.org/en/)

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/identities.png)
[ identities image ]

#### 4) Create SMTP credentials & note it down :


Amazon SES > SMTP Settings > Create SMTP credentials > Create user

## Setup Jenkins :


Settins > System > System admin email address( sender email) > Apply

Test configuration by sending test email:

Settins > System > E-mail Notification > SMTP server > paste SMTP Endpoint here > advanced > use SSL > SMTP port (from SMTP settings) > use SMTP authentication > (Username & Password from SMTP credentials) > test configuration by sending test email > recipient email id > Test configuration

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/jenkins-email.png)



### Setup email in pipeline :

Extended email notification > SMTP server > (paste SMTP endpoint here) > SMTP port > (paste SMTP endpoint here) > Advanced > Credentials > Add > Jenkins > [Add credentials : kind > username with password > ( username and password from SMTP credentials) > Add] > Select the credentials > use SSL > Apply > save



### Create a pipeline :

Pipeline Script > pipeline syntax > sample step > extended email > to ( where you want to send email) > (write subject and body) > Generate pipeline Script > paste it to pipeline script > save

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/email-script.png)



Now build the pipeline.

Email successfully send :

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/email-verification.png)




We can try another pipeline script :

```
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {    
                    // Intentional failure
                    error 'This stage fails on purpose'
            }
        }
    }
    post {
        success {
            // on failure 
            emailext body: 'success', subject: 'success', to: 'gimakij818@gamening.com'
        }
        failure {
            // on failure 
            emailext body: 'pipeline failed', subject: 'failed', to: 'gimakij818@gamening.com'
        }
    }
}
```

This script will fail pipeline and send email.











# Setup Google chat notification :

Reference : https://support.google.com/chat/answer/9632691?hl=en&co=GENIE.Platform%3DDesktop

Go to google chat : chat.google.com 

### Steps :

#### 1) Create a space :
New chat > Create Space > apps and integrations > add apps > Jenkins > Install app 

#### 2) Get the token

#### 3) Download plugin :

 Install Chat plugin on Jenkins server( https://support.google.com/chat/answer/9632691?hl=en&co=GENIE.Platform%3DDesktop )

#### 4) Install plugin to Jenkins :
Jenkins > settings > Plugins > Advanced settings > deploy plugin > choose file > deploy

#### 5) Add google chat credential to Jenkins :

Jenkins > settings > credentials > system > Global credentials > Add credentials > secret text > paste the token from google chat > crate



#### Create a new pipeline :

Add pipeline script :

```
pipeline {
    agent any

    stages {
        stage('CLEANUP WORKSPACE'){
            steps{
                script{
                    cleanWs()
                }
            }
        }
        }
    post{
        success {
            withCredentials([string(credentialsId: 'google_chat_token', variable: 'token')]) {
            hangoutsNotify(
            message: "PIPELINE: $env.JOB_NAME has completed SUCCESSFULLY.<br>BUILD NUMBER: $env.BUILD_NUMBER",
            token: env.token
            )
            }
        }
    }
}
```
or, we can use another script :

```
pipeline {
    agent any

    stages {
        stage('CLEANUP WORKSPACE') {
            steps {
                script {
                    cleanWs()
                }
            }
        }
    }

    post {
        success {
            withCredentials([string(credentialsId: 'google_chat_token', variable: 'token')]) {
                hangoutsNotify(
                    message: """
                        <b><font color="#0F9D58">✅ PIPELINE SUCCESS</font></b><br>
                        <b>Pipeline:</b> $env.JOB_NAME<br>
                        <b>Build Number:</b> $env.BUILD_NUMBER<br>
                        <b>Status:</b> <font color="#0F9D58">COMPLETED SUCCESSFULLY</font><br>
                        <i>Great job! 🎉</i>
                    """,
                    token: env.token
                )
            }
        }
        failure {
            withCredentials([string(credentialsId: 'google_chat_token', variable: 'token')]) {
                hangoutsNotify(
                    message: """
                        <b><font color="#EA4335">❌ PIPELINE FAILURE</font></b><br>
                        <b>Pipeline:</b> $env.JOB_NAME<br>
                        <b>Build Number:</b> $env.BUILD_NUMBER<br>
                        <b>Status:</b> <font color="#EA4335">FAILED</font><br>
                        <i>Please check the logs for details. 🛠️</i>
                    """,
                    token: env.token
                )
            }
        }
    }
}
```

Jenkins pipeline send notification to google chat successfully :

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/gchat-jenkins.png)



# Setup Slack notification :

Login to slack : https://slack.com/get-started#/createnew

Channel > create Channel > go inside channel > : > open channel details > Integrations > Add an app > Jenkins CI > install > Add to slack > post to channel > Add Jenkins CI integrations 


### Add plugin to Jenkins :

 Jenkins > settings > plugins > Available plugin > slack notification > Install 

### Set connection with slack :

Jenkins > settings > system > slack > workspace > paste team subdomain here > credential > add > Jenkins > [secret text < paste the secret from (Add Jenkins CI integrations)  > Add] > select credential >  test > save


#### Create a pipeline :

[pipeline syntax > send slack message > Generate pipeline script]

or

Add the script :

```
pipeline {
    agent any
    stages {
        stage('1st stage') {
            steps {
                sh 'pwd'
            }
        }
    }
    post {
        success {
            script {
                slackSend(channel: "test",color: 'good', message: "my-first-pipeline-slack passed successfully")

            }
        }
    }
}
```

Customize slack message from Jenkins : https://plugins.jenkins.io/slack/

Jenkins send notification to slack successfully :

![Image Alt](https://github.com/sheikhsalmanhossain/jenkins/blob/27be323fefc67556e49c0921f500d8e7121ad022/5-Jenkins_Notification_Service/image/slack-jenkins.png)
