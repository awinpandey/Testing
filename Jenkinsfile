pipeline {
    agent any

stages {
    
    stage('Checking Java Version') {
        steps {
            sh "export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-12.0.1.jdk/Contents/Home && java -version"
        }
    }

    stage('Install JHipster') {
        steps {
            sh "/usr/bin/npm install  generator-jhipster yo@latest"
            
        }
    }

    stage('Packaging the Build') {
        steps {
            sh "./mvnw -Pprod clean verify"
        }
    }

   stage ('Sonar Analysis') {
      steps {
	      withSonarQubeEnv('sonarqube')
		{
//		    sh "/opt/sonar_scanner/bin/sonar-scanner -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=admin -Dsonar.password=admin -Dsonar.projectName=$JOB_NAME -Dsonar.projectVersion=1.0 -Dsonar.projectDescription=$JOB_NAME -Dsonar.projectKey=$JOB_NAME  -Dsonar.sources=umsl/ -Dsonar.language=java -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/"
	sh "/opt/sonar_scanner/bin/sonar-scanner -Dsonar.host.url='http://34.221.219.252:9000' -Dsonar.login=admin -Dsonar.password=admin -Dsonar.projectName="jenkins-pipeline" -Dsonar.projectVersion=1.0 -Dsonar.projectDescription="jenkins-pipeline" -Dsonar.projectKey="6d129df9d26c61224e6caca863a7a6478c16c516" -Dsonar.sources=myFirstPipeline/ -Dsonar.language=java -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/" 
        }    
         }
    }

    stage('Execute Java -jar file') {
           steps {
	      sh "export jarjava=`ps -ef | grep java | grep -v grep |  grep 'java -jar' | awk '{print \$2}'` && if ! test -z \${jarjava};then kill -9 \${jarjava};fi"
		  sh "export JENKINS_NODE_COOKIE=dontKillMe;nohup java -jar /var/lib/jenkins/workspace/myFirstPipeline/target/*.jar &"

	         }
	}
    stage('Send Email Notification') {
	    steps {
	          mail bcc: '', body: "This is your Jenkins Build Name ${env.JOB_NAME} and Build Number is [${env.BUILD_NUMBER}] which have result ${currentBuild.currentResult}", cc: '', from: 'Jenkins Server', replyTo: '', subject: 'myFirstPipeline case Study', to: 'a.pandey998182@gmail.com'
	    } 
     }
}
}	

