pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''echo "Creating Project Package"
echo "Project Workspace is " ${WORKSPACE}

$APIGWDEPLOYTOOLS/apigateway/posix/bin/projpack --create  --dir=. --passphrase-none --name=common --type=pol --add ${WORKSPACE}"/APIProject11" --projpass-none --add ${WORKSPACE}"/APIProject22" --projpass-none --add ${WORKSPACE}"/commonProjectDefault" --projpass-none 
cp common.pol /home/ec2-user/'''
        sh '''echo "Deploy Project"

$APIGWDEPLOYTOOLS/apigateway/posix/bin/projdeploy --dir=. --passphrase-none --name=common --type=pol --apply-env=${WORKSPACE}"/EnvironmentConfig/DEV/config.env" --deploy-to --host-name=$ADMINNM --port=8090 --user-name=admin --password=changeme --group-name=$GNAME --change-pass-to-none
echo \'DEPLOYED\''''
      }
    }
    stage('Test') {
      steps {
        sh 'echo "Testing "'
      }
    }
  }
  environment {
    ADMINNM = '54.206.109.15'
    GNAME = 'DEV'
    REPO = '/home/ec2-user/repo/TeamDevelopment'
    GWLB = '54.206.109.15'
    APIGWDEPLOYTOOLS = '/home/ec2-user/Axway-7.7.0'
    SITGWELB = 'GW-UAT-LB-371846769.us-east-1.elb.amazonaws.com'
  }
}