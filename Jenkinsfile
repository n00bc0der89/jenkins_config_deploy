def remote = [:]
remote.name = 'test-server'
remote.host = '192.168.0.150'
remote.allowAnyHosts = true

def config_file_path='deployment-apps'
def test_server_deployment_path='/tmp/'

pipeline {
    agent any
    
    environment {
        TEST_SERVER_CREDENTIALS = credentials('test-credentials')
     }

    stages {
            stage("Deploy config to test server"){
                steps{
                     withCredentials([string(credentialsId: 'test-credentials', variable: 'username',variable: )]) {
                            echo "Deploying config to Test server"
                            remote.user = $TEST_SERVER_CREDENTIALS_USR
                            remote.password = $TEST_SERVER_CREDENTIALS_PSW
                            sshPut remote: remote, from: config_file_path, into: 'test_server_deployment_path'
                     }

                }
            }

            stage("Deploy config to prod server"){
                 when {
                    branch 'master' 
                }
                steps{
                    echo "Deploying config to Prod server"
                }
            }

        }

}