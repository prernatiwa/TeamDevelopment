def props = null
def VERSION
def FIX
def RELEASE

def loadProperties() {
   props = readProperties file:'props.txt'
   echo "version is" "${props.version}"
}

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
         loadProperties()
         echo "${props.version}"

      }
   }
   }
}