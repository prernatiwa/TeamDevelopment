
def VERSION
def readprops
def FIX
def RELEASE

def loadProperties() {
   readprops = readProperties file:'props.txt'
   echo "version is ${readprops['version']}"
   VERSION = readprops['version']
   echo "version1 is ${VERSION}"
   env.FIX = readprops['fix']
   env.custom_var = readprops['version']
}

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
         script {
         loadProperties()
         echo "${env.FIX}"
         echo "${env.custom_var}"
         }
      }
   }
   }
}