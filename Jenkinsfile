pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
                sh 'pwd'
            }
        }
    stage('Test') {
            steps {
                sh 'mvn -B test'
                echo "Test successful"
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }      
    stage('Artifactory'){
        steps {
              sh "curl -X PUT -u admin:admin123 -T /var/jenkins_home/workspace/Newdeployment/target/my-app-v1.${BUILD_NUMBER}.jar http://18.218.59.72:8082/artifactory/EY/my-app-v1.${BUILD_NUMBER}.jar'"
        }
    }      
    stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
