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
            sh 'docker build -t kibana:latest --build-arg ELASTIC_VERSION=8.3.2 -f kibana/Dockerfile .'
            sh 'docker build -t logstash:latest --build-arg ELASTIC_VERSION=8.3.2 -f logstash/Dockerfile .'
               }
            }
        }
      
      stage('Push Docker Images to ACR') {
      steps{
            echo 'loggin to Azure Container registry..'
            sh 'docker login --username edhriacr2022 --password uUqzNWODMutvpcWpFcK2/zvEqT5AMsM4 edhriacr2022.azurecr.io'
         
            echo 'Pushing elasticsearch image to azure container registry...'
            sh 'docker tag elasticsearch edhriacr2022.azurecr.io/elasticsearch:8.3.2'
            sh 'docker push edhriacr2022.azurecr.io/elasticsearch:8.3.2'
         
            echo 'Pushing kibana image to azure container registry..'
            sh 'docker tag kibana edhriacr2022.azurecr.io/kibana:8.3.2'
            sh 'docker push edhriacr2022.azurecr.io/kibana:8.3.2'
            
            echo 'Pushing logstash docker image to azure container registry..'
            sh 'docker tag logstash edhriacr2022.azurecr.io/logstash:8.3.2'
            sh 'docker push edhriacr2022.azurecr.io/logstash:8.3.2'   
      }
    }
      
      
      stage('Deploy Stage..') {
            steps {
                echo 'Deploying App to Kubernetes..'
                   script {
                       kubernetesDeploy(configs: "deployment.yml", kubeconfigId: "kubernetes")
                         }
                  }
        }
   }
}
