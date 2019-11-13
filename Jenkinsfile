
def VERSION
def readprops
def FIX
def RELEASE

def loadProperties() {
   readprops = readProperties file:'props.txt'
   echo "version is ${readprops['version']}"
   VERSION = readprops['version']
   FIX = readprops['fix']
}

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
         script {
         loadProperties()
         echo "${FIX}"
         }
      }
   }
   }
}