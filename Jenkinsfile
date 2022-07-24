pipeline {
   agent any
   tools{
      maven 'Maven3.8.6'
   }
   
   environment {
       registryName = 'edhriacr2022'
       registryUrl = 'edhriacr2022.azurecr.io'
       registryCredential = 'ACR'
       dockerImage = ''
    }
    
   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
       }
      
      stage('Test Stage') {
            steps {
                echo 'Testing..'
            }
        }
      
      stage('Build Stage') {
            steps {
            echo 'Building..'
            script { 
            sh 'docker build -t elasticsearch:latest --build-arg ELASTIC_VERSION=8.3.1 -f elasticsearch/Dockerfile .'
            sh 'docker build -f kibana:latest --build-arg ELASTIC_VERSION=8.3.1 -f kibana/Dockerfile .'
            sh 'docker build -f logstash:latest --build-arg ELASTIC_VERSION=8.3.1 -f logstash/Dockerfile .'
               }
            }
        }
      
     stage('Upload Image to ACR') {
     steps{   
         script {
           docker.withRegistry( "http://${registryUrl}", registryCredential ) {
           dockerImage.push()
           // sh 'docker push edhriacr2022.azurecr.io/shopfront:1.0'
           // docker tag shopfront:1.0 edhriacr2022.azurecr.io/shopfront:1.0
         // docker push edhriacr2022.azurecr.io/shopfront:1.0
        }
      }
    }
      
      
      stage('Deploy Stage') {
            steps {
                echo 'Deploying....'
            }
        }
   }
}
