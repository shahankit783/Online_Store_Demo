pipeline {
  environment {
    //This variable need be tested as string
    doError = '10'
  }
  agent any
  stages {
    stage("Env Build Number"){
            steps{
                echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}"                                                
            }
    }
    stage('Error') {
      when {
        expression { doError == '1' }
      }
      steps {
        echo "Failure"
        error "failure test. It's work"
      }
    }
    stage('Success') {
      when {
        expression { doError == '0' }
      }
      steps {
        echo "ok"
      }
    }
  }
  post {
    always {
      echo 'I will always execute'
    }
  }
}
