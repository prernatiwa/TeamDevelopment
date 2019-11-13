def readprops
  def loadProperties() {
      readprops = readProperties file:'props.txt'
      keys= readprops.keySet()
      for(key in keys) {
          value = readprops["${key}"]
          env."${key}" = "${value}"
         
      }
       echo "version is ${env.ADMINNM}"
    }

pipeline {
  agent any
  stages {
    stage('LoadConfiguration'){
        steps {
          script {
                 loadProperties() 
         }
        }
    }
    stage('Build') {
      steps {
        script {
          echo "Creating Project Package"
          echo "Project Workspace is " ${WORKSPACE}
          
            echo "${env.ADMINNM}"
            echo "Hello dear" 
         
          
           
      }
    }
    }
    
    stage('Test') {
      steps {
        sh 'echo "Testing"'
      }
    }
  }

}
