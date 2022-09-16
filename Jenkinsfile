pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
               sh 'scp /home/ubuntu/.jenkins/workspace/Scriptedpipeline/webapp/target/webapp.war ubuntu@172.31.10.25:/var/lib/tomcat9/webapps/testapp.war'

            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /home/ubuntu/.jenkins/workspace/Scriptedpipeline/testing.jar'
            }
        }
       
    }
 
    post {
       
       success{
           
     sh 'scp /home/ubuntu/.jenkins/workspace/Scriptedpipeline/webapp/target/webapp.war ubuntu@172.31.12.210:/var/lib/tomcat9/webapps/prodapp.war' 
            
      
       } 
        failure
        {
            mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'failure of CICD process', to: 'abhilashreddy977@gmail.com'
        }
        
    }
    
    
}
