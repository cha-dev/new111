pipeline{
    
    agent any
 
 //properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
	
	tools{
       maven  "maven"
       }
    
    stages{
        stage('CheckoutCode')
        {
          steps{
            git credentialsId: 'ae87449e-f8b2-469c-bd91-bfaf15761db2', url: 'https://github.com/rajeshwarayya/maven-web-application.git'
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
        sshagent(['Tomcat']) {            
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application*.war ec2-user@172.31.35.19:/opt/tomcat8/webapps"
           
        }
    }
	}
    
   }
    
}
