
def VERSION
def FIX
def RELEASE

def loadProperties() {
   def props = readProperties file:'props.txt'
   echo ${props.version}
   keys= props.keySet()
    for(key in keys) {
        value = props["${key}"]
        env."${key}" = "${value}"
    }
    echo ${env.version}
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