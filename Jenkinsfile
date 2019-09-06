pipeline {
    agent any

stages {
    
    stage('Check Java') {
        steps {
            sh "export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-12.0.1.jdk/Contents/Home && java -version"
        }
    }

    stage('Install jhipster') {
        steps {
            sh "/usr/bin/npm install  generator-jhipster yo@latest"
            
        }
    }

    stage('Packaging the build') {
        steps {
            sh "./mvnw -Pprod clean verify"
        }
    }
	
	stage('Send email notification ') {
		steps {
		     mail(subject: 'Build', body: 'New Deployment Status of Jhipster Prod', to: 'vdkthakur@gmail.com')
		}
	}
	
	post {  
          always {  
             echo 'This will always run'  
         }  
         success {  
             echo 'This will run only if successful'  
         }  
         failure {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "vdkthakur@gmail.com";  
         }  
         unstable {  
             echo 'This will run only if the run was marked as unstable'  
         }  
         changed {  
             echo 'This will run only if the state of the Pipeline has changed'  
             echo 'For example, if the Pipeline was previously failing but is now successful'  
         }  
     } 
}
//    stage('Test URL of webpage') {
//        steps {
//            sh "export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-12.0.1.jdk/Contents/Home && java -jar $WORKSPACE/target/*.jar"
//        }
//    }
}

}

//    stage('Upload to S3') {
//        steps {
//            withAWS(region:'region=ap-south-1',credentials:'teacher') {
//            s3Upload(bucket: 'case000', workingDir:'$WORKSPACE/target/', includePathPattern:'**/*');
//	    }
//		mail(subject: 'Build', body: 'New Deployment to Prod', to: 'vdkthakur@gmail.com')
//	}
//    }

    /*        pwd(); //Log current directory

            withAWS(region:'ap-south-1',credentials:'iamuser-student') {

                 def identity=awsIdentity();//Log AWS credentials

                // Upload files from working directory 'dist' in your project workspace
                s3Upload(bucket:"case000", workingDir:'dist', includePathPattern:'');
            }

        }
    }*/
	
   /*stage('Downlaod and Deploy on Ec2 server is final step') {
        steps {
            sh "export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-12.0.1.jdk/Contents/Home && java -jar $WORKSPACE/target/*.jar"
        };
    }*/

