def props
def VERSION
def FIX
def RELEASE

node {
   props = readProperties file:'props.txt'
   VERSION = props['version']
   FIX = props['fix']
   RELEASE = VERSION + "_" + FIX
}

pipeline {
   agent any
   stages {
      steps {
      stage('Build') {
         echo ${RELEASE}
      }
   }
   }
}