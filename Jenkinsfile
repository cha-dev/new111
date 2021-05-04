pipeline{
    
    agent any
 
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
	
	tools{
       maven  "maven"
       }
    
    stages{
        stage('CheckoutCode')
        {
          steps{
            git credentialsId: '97c15c62-4ecd-47e6-a9e7-c4cdd1724f5a', url: 'https://github.com/govardhantech/maven-web-application.git'
        } 
        }
    
    
       stage('Build')
    {
   steps{
    sh "mvn clean package"
   }
   }
   
   
   stage('deploying in tomcat-server')
    {
	  steps{
        sshagent(['ec2-user']) {
            
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application*.war ec2-user@13.235.133.121:/opt/tomcat8/webapps"
           
        }
    }
	}
    
   }
    
}
