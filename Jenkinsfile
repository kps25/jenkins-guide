#!/usr/bin/groovy


def delivery
pipeline{
  agent none

  stages {
   stage('Load deploy grrovy code')
	{
steps {
	checkout scm
     	delivery = load 'deploy.groovy'
	sh "ls ."
	}	
}
   stage('Create Archive')
	{
steps {
	delivery.jenkins_bkp("jenkins", "jobs/Java-Web-App")
	}
}
   stage('Backup to S3 Bucket')
	{
steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'mobile-s3-user', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh "aws s3 cp *.tar.gz s3://mybucket-ssp --region ap-south-1"
    	}	
   	} }
}
}	
}

