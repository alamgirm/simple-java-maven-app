env.DOCKERHUB_USERNAME = 'alamgirm'
pipeline {
    //agent  any
     agent { 
         node { 
             label 'jkslave' //Jenkins Slave  
         } 
     }
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/alamgirm/simple-java-maven-app.git'
            }
        }
        
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
        // Build docker iamge
        stage('BuildDockerImage') {
            sh "docker build -t ${DOCKERHUB_USERNAME}/myapp:${BUILD_NUMBER} ."
        }
        // push the built image
        stage("DockerPush") {
            withDockerRegistry([credentialsId: 'DockerHub']) {
            sh "docker push ${DOCKERHUB_USERNAME}/myapp:${BUILD_NUMBER}"
      }
    }
    }
}
