
def VERSION
def readprops
def FIX
def RELEASE

def loadProperties() {
   readprops = readProperties file:'props.txt'
   echo "version is ${readprops['version']}"
   VERSION = readprops['version']
   echo "version1 is ${VERSION}"
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

         if (env.BRANCH_NAME != 'master' && env.BRANCH_NAME != 'staging') {
                echo 'This is not master or staging'
            } else {
                echo 'things and stuff'
                loadProperties()
                echo "${env.fix}"
                echo "${env.custom_var}"
            }

         }
      }
   }
   stage('Prep') {
      steps {
         echo "${env.custom_var}"
      }
     }
   }
}