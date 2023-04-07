pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }
      }   
   stage('Unit testing') {
            steps {
              sh "mvn test"
            }
            post {
              always {
                junit 'target/surefire-reports/*.xml'
                jacoco execPattern: 'target/jacoco.exec'
              }
            }
        }   
stage('Docker build and Push') {
            steps {
              sh 'printenv'
              sh 'docker build -t tamarah/numeric-app:""$GIT_COMMIT"" .'
              sh 'docker push tamarah/numeric-app:""GIT_COMMIT""'
            }
      }   
    }

}