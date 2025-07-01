pipeline {
  agent any
  stages{
    stage('checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/johnclimie/DjangoDevOPs'
      }
    }
    stage('Login to ECR'){
      steps{
        withAWS(region: 'ap-south-1', credentials: 'aws-creds'){
          powershell '''
          aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 451947743265.dkr.ecr.us-east-2.amazonaws.com
          '''
        }
      }
    }
    stage('Build docker image'){
      steps{
        powershell '''
        docker build -t test:django
        docker tag test:django 451947743265.dkr.ecr.us-east-2.amazonaws.com/test:django
        '''
      }
    }
    stage('PUshing image to ECR') {
      steps{
        powershell '''
        docker push 451947743265.dkr.ecr.us-east-2.amazonaws.com/test:django
        '''
      }
    }
  }    
}
