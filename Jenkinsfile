pipeline {
    agent  any
// I am not using a docker/maven image, rather a dedicated slave
// to be controlled and used by the Jenkins Master
/*
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
*/
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
