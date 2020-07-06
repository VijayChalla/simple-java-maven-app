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
    stage('Deploy to artifactory')
        
    stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
