
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

   keys= readprops.keySet()
    for(key in keys) {
        value = readprops["${key}"]
        env."${key}" = "${value}"
    }
}

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
         script {
         loadProperties()
         echo "${env.fix}"
         echo "${env.custom_var}"
         }
      }
   }
   }
}