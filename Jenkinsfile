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
            sh 'mvn clean install -f elasticsearch/pom.xml'
            sh 'mvn clean install -f kibana/pom.xml'
            sh 'mvn clean install -f logstash/pom.xml'
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
