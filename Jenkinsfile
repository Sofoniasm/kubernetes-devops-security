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
              withDockerRegistry([credentialsId: "docker", url: ""]) {
                sh 'printenv'
                sh 'sudo docker build -t siddharth67/numeric-app:""$GIT_COMMIT"" .'
                sh 'docker push siddharth67/numeric-app:""$GIT_COMMIT""'
         }
      }
    }
}
