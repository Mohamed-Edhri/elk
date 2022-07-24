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
            sh 'docker build -t elasticsearch:latest --build-arg ELASTIC_VERSION=1.0 -f elasticsearch/Dockerfile .'
            sh 'mvn clean install -f kibana:latest --build-arg ELASTIC_VERSION=1.0 kibana/Dockerfile .'
            sh 'mvn clean install -f logstash:latest --build-arg ELASTIC_VERSION=1.0 logstash/Dockerfile .'
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
