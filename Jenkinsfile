pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/maven123.git' 
                    }
                    catch(Exception e1)
                    {
                       mail bcc: '', body: 'Jenkins is unable to download the dev code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.team@gmail.com'
                       exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousBuild_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                           sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Buid Failed', to: 'developers.team@gmail.com'
                        exit(1)
                    }
                }
             
            }
        }
        stage('ContinuousDeployment_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: 'e55d0b96-e001-4563-be38-2c7347078e19', path: '', url: 'http://172.31.21.238:8080')], contextPath: 'testapp', war: '**/*.war' 
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy artifact into tomcat on the QAServers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousTesting_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
               sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium test scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
         stage('ContinuousDelivery_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                         deploy adapters: [tomcat9(credentialsId: 'e55d0b96-e001-4563-be38-2c7347078e19', path: '', url: 'http://172.31.23.131:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
                    }
                }
              
            }
        }
        
    }
}

