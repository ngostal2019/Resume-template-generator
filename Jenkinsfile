pipeline {
  agent any

  environment {
    TOMCAT_DEPLOYER_ID='deployer'
    TOMCAT_SERVER_IP='34.205.247.151'
    TOMCAT_SERVER_PORT='8080'
  }

  tools {
        // Must match the name defined in Jenkins global tool configuration
        maven 'maven3' 
        jdk 'java25'
    }

  stages{
    stage('Maven Clean') {
      steps {
        sh 'mvn clean'
      }
    }
    stage('Maven Install') {
      steps {
        sh 'mvn -B install -DskipTests'
      }
    }
    stage('Maven Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Maven Package WAR file') {
      steps {
        sh 'mvn package -DskipTests'
      }
    }
    stage('Print Envs') {
      steps {
        sh 'printenv'
      }
    }
    stage('Deploy to Tomcat 11') {
      steps {
          // Deploy step provided by the Deploy to Container Plugin
          sh 'pwd'
          sh 'ls -l target/'
          deploy adapters: [tomcat9(
                  alternativeDeploymentContext: '',
                  credentialsId: "${env.TOMCAT_DEPLOYER_ID}",
                  path: '',
                  url: 'http://${env.TOMCAT_SERVER_IP}:${env.TOMCAT_SERVER_PORT}/'
                  )
            ],
            
                contextPath: null, 
                war: '**/*.war',
                onFailure: false
      }
    }
  }
  // post {
  //     always {
  //         // Clean up workspace to prevent disk space issues
  //         cleanWs()
  //     }
  //     failure {
  //         echo "Pipeline failed. Check build logs or server connectivity."
  //     }
  // }
}
