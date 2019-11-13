def readprops
  def loadProperties() {
      readprops = readProperties file:'env_dev.properties'
      echo "version is ${readprops['ADMINNM']}"
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
          echo "Project Workspace is " ${WORKSPACE}
          echo "version1 is ${readprops['ADMINNM']}"
          $APIGWDEPLOYTOOLS/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}"/APIProject11" --projpass-none --add ${WORKSPACE}"/APIProject22" --projpass-none --add ${WORKSPACE}"/commonProjectDefault" --projpass-none 
          cp common.pol /home/ec2-user/'''
         sh '''echo "Deploy Project"
          $APIGWDEPLOYTOOLS/apigateway/posix/bin/projdeploy --dir=. --passphrase-none --name=common --type=pol --apply-env=${WORKSPACE}"/EnvironmentConfig/DEV/config.env" --deploy-to --host-name=$ADMINNM --port=8090 --user-name=admin --password=changeme --group-name=$GNAME --change-pass-to-none
          echo \'DEPLOYED\''''
      }
    }
    stage('Test') {
      steps {
        sh 'echo "Testing"'
      }
    }
  }
}

