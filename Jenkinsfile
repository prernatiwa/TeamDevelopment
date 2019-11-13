def readprops
def usernameLocal
def passwordLocal
  def loadProperties() {
      readprops = readProperties file:'env_dev.properties'
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
     stage('Test') {
      steps {
          withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'simple_creds', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME']]) {
            echo "echo step - env: ${env.USERNAME} - password through ${env.PASSWORD}"
            sh 'echo "sh step - echo: ${USERNAME} - ${PASSWORD}"'
            script{
            usernameLocal = env.USERNAME
            passwordLocal = env.PASSWORD
            }
            echo "echo step (in block) - vars: ${usernameLocal} - ${passwordLocal}"
          } 
          echo "echo step (out of block) - vars: ${usernameLocal} - ${passwordLocal}"
      }
    }
    stage('Build') {
      steps {
        sh '''echo "Creating Project Package"
          echo "Project Workspace is  ${WORKSPACE}"
          echo "${APIGWDEPLOYTOOLS}/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}/APIProject11 --projpass-none --add ${WORKSPACE}/APIProject22 --projpass-none --add ${WORKSPACE}/commonProjectDefault --projpass-none"
          $APIGWDEPLOYTOOLS/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}"/APIProject11" --projpass-none --add ${WORKSPACE}"/APIProject22" --projpass-none --add ${WORKSPACE}"/commonProjectDefault" --projpass-none
          cp common.pol /home/ec2-user/'''
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'simple_creds', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME']]) {
            echo "echo step - env: ${env.USERNAME} - password through ${env.PASSWORD}"
            sh 'echo "sh step - echo: ${USERNAME} - ${PASSWORD}"'
            script{
            usernameLocal = env.USERNAME
            passwordLocal = env.PASSWORD
            }
            echo "echo step (in block) - vars: ${usernameLocal} - ${passwordLocal}"
          
        
        sh '''  
          echo "Deploy Project"
          ${APIGWDEPLOYTOOLS}/apigateway/posix/bin/projdeploy --dir=. --passphrase-none --name=common --type=pol --apply-env=${WORKSPACE}/EnvironmentConfig/DEV/config.env --deploy-to --host-name=${ADMINNM} --port=${PORT} --user-name="${usernameLocal}" --password="${passwordLocal}" --group-name=${GNAME} --change-pass-to-none
          echo "DEPLOYED"'''
        }
        
      }
    }
   
    
    
  }

}
