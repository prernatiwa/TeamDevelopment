def props
def VERSION
def FIX
def RELEASE

def loadProperties() {
   props = null
   props = readProperties file:'props.txt'
   echo "version is" "${props.version}"
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