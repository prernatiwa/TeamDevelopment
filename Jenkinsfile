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
        sh '''echo "Creating Project Package"
          echo "Project Workspace is  ${WORKSPACE}"
          echo "${APIGWDEPLOYTOOLS}/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}/APIProject11 --projpass-none --add ${WORKSPACE}/APIProject22 --projpass-none --add ${WORKSPACE}/commonProjectDefault --projpass-none"
          "${APIGWDEPLOYTOOLS}/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}/APIProject11 --projpass-none --add ${WORKSPACE}/APIProject22 --projpass-none --add ${WORKSPACE}/commonProjectDefault --projpass-none"'''
        sh '''  
          echo "Deploy Project"
          "${APIGWDEPLOYTOOLS}/apigateway/posix/bin/projdeploy --dir=. --passphrase-none --name=common --type=pol --apply-env=${WORKSPACE}/EnvironmentConfig/DEV/config.env --deploy-to --host-name=${ADMINNM} --port=8090 --user-name=admin --password=changeme --group-name=${GNAME} --change-pass-to-none"
          echo "DEPLOYED"'''
           
      }
    }
     stage('Test') {
      steps {
        sh 'echo "Testing"'
      }
    }
    
    
  }

}
