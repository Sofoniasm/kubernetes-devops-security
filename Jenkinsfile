pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
               archive 'target/*.jar' 
            }
        }
      stage('Unit Tests - JUnit and JaCoCo') {
            steps {
              sh "mvn test"
         }
       }
      stage('Docker Build and Push') {
            steps {
              withDockerRegistry([credentialsId: "docker-hub", url: "https://login.docker.com/u/login/"]) {
                sh 'printenv'
                sh 'sudo docker build -t sofoniasm/numeric-app:""$GIT_COMMIT"" .'
                sh 'docker push sofoniasm/numeric-app:""$GIT_COMMIT""'
         }
      }
      }
    }
}
