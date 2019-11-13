def readprops
  def loadProperties() {
      readprops = readProperties file:'props.txt'
      keys= readprops.keySet()
      for(key in keys) {
          value = readprops["${key}"]
          env."${key}" = "${value}"
         
      }
       echo "version is ${env.ADMINNM}"
    }

pipeline {
  agent any
  stages {
    stage('LoadConfiguration'){
        steps {
          script {
                 loadProperties() 
         }
        }
    }
    stage('Build') {
      steps {
        script {
          echo "Creating Project Package"
         
          echo "${env.ADMINNM}"
          echo "Hello dear" 
          echo "Project Workspace is  ${WORKSPACE}"
          echo "${env.APIGWDEPLOYTOOLS}/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}/APIProject11 --projpass-none --add ${WORKSPACE}/APIProject22 --projpass-none --add ${WORKSPACE}/commonProjectDefault --projpass-none"
          ./"${env.APIGWDEPLOYTOOLS}/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}/APIProject11 --projpass-none --add ${WORKSPACE}/APIProject22 --projpass-none --add ${WORKSPACE}/commonProjectDefault --projpass-none"
          echo "Deploy Project"
          ./"${env.APIGWDEPLOYTOOLS}/apigateway/posix/bin/projdeploy --dir=. --passphrase-none --name=common --type=pol --apply-env=${WORKSPACE}/EnvironmentConfig/DEV/config.env --deploy-to --host-name=${env.ADMINNM} --port=8090 --user-name=admin --password=changeme --group-name=${env.GNAME} --change-pass-to-none"
          echo "DEPLOYED"
           
      }
    }
    }
    
    stage('Test') {
      steps {
        sh 'echo "Testing"'
      }
    }
  }

}
