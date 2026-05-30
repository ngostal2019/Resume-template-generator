pipeline {
  agent any

  environment {
    TOMCAT_DEPLOY_ID='deployer'
    TOMCAT_SERVER_IP='34.205.247.151'
    TOMCAT_SERVER_PORT='8080'
    WAR_FILE_BUILT='**/*.war'
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
    // stage('Deploy to Tomcat 11') {
    //   steps {
    //       // Deploy step provided by the Deploy to Container Plugin
    //       deploy artifacts: '${env.WAR_FILE_BUILT}', 
    //             contextPath: '', 
    //             war: null, 
    //             containers: [
    //                 tomcat9x(
    //                     url: 'http://${env.TOMCAT_SERVER_IP}:${env.TOMCAT_SERVER_PORT}',
    //                     credentialsId: "${env.TOMCAT_DEPLOY_ID}",
    //                 )
    //             ]
    //   }
    // }
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
