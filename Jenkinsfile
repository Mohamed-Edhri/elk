pipeline {
   agent any

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
               sh 'docker images -a'
               sh 'cd /var/lib/jenkins/workspace/Elastic_Stack_App_qa/elasticsearch'
               sh 'docker build -t elasticsearch:latest --build-arg ELASTIC_VERSION=8.3.1 .'
               sh 'docker images -a'
               sh 'cd ..'
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
