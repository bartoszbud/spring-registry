pipeline {
   agent any

   tools {
      maven "M3"
   }

   stages {
        stage('Build') {
           steps {
            sh 'mvn clean deploy -U -Dmaven.test.skip=true'
           }
        }
        stage('Test') {
           steps {
              echo 'Testing application'
           }
        }
        stage('Deploy') {
           steps {
              echo 'Deploying application'
           }
        }
   }
}