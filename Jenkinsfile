
def VERSION
def FIX
def RELEASE

def loadProperties() {
   def props = readProperties file:'props.txt'
   keys= props.keySet()
    for(key in keys) {
        value = props["${key}"]
        env."${key}" = "${value}"
    }
   echo "version is" "${env.version}"
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