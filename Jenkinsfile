pipeline {
    agent any
    
    stages {
        stage('Display Build Info') {
            steps {
                sh """
                echo ${env.BUILD_NUMBER}
                echo ${env.JENKINS_URL}
                sleep 5
                """
            }
        }
        stage('Display SCM Info') {
            steps {
                sh """
                echo ${BUILD_TAG}
                """
            }
        }
    }
}
