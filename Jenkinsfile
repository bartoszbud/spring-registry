 pipeline {
    agent any

    environment {
        def pom = readMavenPom file: 'pom.xml'
        def yml = readYaml file: 'ct.yml'
        def artifactId = "${pom.artifactId}"
        def version =   "${pom.version}"
        def ct_port = "${yml.port}"
        def log_file = "${yml.log}"
        def env = "${yml.env}"
    }

    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '14'))
    }

    tools {
       maven "M3"
    }

    stages {
         /*stage('Static Code Analysis') {
            steps {
               sh 'mvn sonar:sonar -Dsonar.host.url=http://sonarqube.lab.pl -Dsonar.login=sqa_cd42f692c2723795ea0ea43e8b07592dc888e6b8'
            }
         }*/
         stage('Build') {
            steps {
               sh 'mvn clean package -Dmaven.test.skip=true -DsendCredentialsOverHttp=true'
            }
         }
         /*stage('Test') {
            steps {
               echo 'Testing application'
            }
         }
         stage('Prepare') {
            steps {
               catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh 'sh /var/jenkins_home/pipe_prepare.sh ${env} ${artifactId} ${version}'
               }
            }
         }
         stage('Deploy') {
            steps {
               sh 'sh /var/jenkins_home/pipe_deploy.sh ${env} ${artifactId} ${version} ${ct_port} ${log_file}'
            }
         }*/
    }
 }