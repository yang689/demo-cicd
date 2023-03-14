pipeline {
  agent any
  //tools {
    //jdk 'oracle-7u80'
  //}
  //agent {
    //docker {
      //image 'openjdk:11'
      //args '-v /tmp:/tmp'
      //reuseNode true
    //}
  //}
  environment{
    DOCKER_IMAGE = "hoanglvh/cicd-pipeline"
    npm_config_cache = 'npm-cache'
  }
  
  stages {
    stage("run frontend"){
      steps {
        echo 'executing yarn...'
        nodejs('Node-17.0'){
          sh '$(whoami)'
          //sh 'chown -R $(whoami) "/.npm"'
          sh 'cd /var/lib/jenkins/workspace'
          sh 'chown -R 1003:998 "$(workspace)/.npm"'
          sh 'yarn install'
      }
    }
  }
    stage("run backend"){
      steps{
        echo 'executing gradle...'
        withGradle(){
          sh './gradlew -v'
      }
    }
  }
    stage('Java version'){
      steps{
        sh '''
            env |grep -e PATH -e JAVA_HOME
            which java
            java -version
        '''
      }
    }
    stage ('Build'){
      steps {
        echo 'Running build automation'
        sh './gradlew clean build'
      }
    }
  }
}
