pipeline {
   agent any

   tools {
      maven "M3"
   }

   stages {
        stage('Build') {
           steps {
            sh 'mvn package -DsendCredentialsOverHttp=true'
            //sh 'mvn clean deploy -U -Dmaven.test.skip=true'
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
              sh 'ssh -o StrictHostKeyChecking=no nexus@10.0.0.24 -C "podman rm spring-registry && podman image rm registry-service-sba:1.0 && podman run --tls-verify=false -d -p 8762:8762 -v ~/app/:/app/ --replace=true --name spring-registry 10.0.0.24:8083/registry-service-sba:1.0 && podman logs spring-registry"'
           }
        }
   }
}