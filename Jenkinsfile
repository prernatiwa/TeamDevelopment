def props
def VERSION
def FIX
def RELEASE

def loadProperties() {
   props = readProperties file:'props.txt'
   VERSION = props['version']
   FIX = props['fix']
   RELEASE = VERSION + "_" + FIX
}

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
         loadProperties()
         echo "${props.version}"
         echo "${RELEASE}"

      }
   }
   }
}