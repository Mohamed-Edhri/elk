pipeline {
   agent any
   tools{
      maven 'Maven3.8.6'
   }
   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
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
      
      stage('Test Stage') {
            steps {
                echo 'Testing..'
            }
        }
      stage('Deploy Stage') {
            steps {
                echo 'Deploying....'
            }
        }
   }
}
