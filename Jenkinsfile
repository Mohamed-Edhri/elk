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
               sh 'cd elasticsearch/'
               sh 'docker build -t elasticsearch .'
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








      

