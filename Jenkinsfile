
def delivery
node {

   stage('Load deploy grrovy code')
	{
     	delivery = load 'deploy.groovy'
	}	
  
   stage('Create Archive')
	{
	delivery.jenkins_bkp("jenkins", "jobs/Java-Web-App")
	}

   stage('Backup to S3 Bucket') 
	{
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'mobile-s3-user', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh "aws s3 cp *.tar.gz s3://mybucket-ssp --region ap-south-1"
    	}	
   	}
}	

