Steps for email-integration with jenkins

1. Install Email Extension Plugin. 
Jenkins dashboard --> Manage jenkins --> Plugin -->Email Extension Plugin 

2. Configure E-mail extention plugin. 
Jenkins dashboard --> Manage plugin --> System --> Jenkins location [Add Jenkins URL and System Admin e-mail address (e.g Jenkins <bhagyashritupe96@gmail.com>)] ,  --> Extended E-mail Notification [ SMTP server (smtp.gmail.com) SMTP Port (465) ] --> E-mail Notification [SMTP server (smtp.gmail.com)] --> Advanced --> Use SMTP Authentication 
--> username and password

Note: Set up App password for your google account and use it as a password for this plugin.
Manage Google Account --> Security --> Two step verification --> App Passwords 

3. Save and apply.

4. Create freestyle job and script:
```
pipeline {
    agent any
     
    stages {
        stage('Ok') {
            steps {
                echo "Ok"
            }
        }
    }
    post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
}
```
5. Save and build.
