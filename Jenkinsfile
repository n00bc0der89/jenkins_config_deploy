def remote = [:]
remote.name = 'test-server'
remote.host = '192.168.0.150'
remote.allowAnyHosts = true

def config_file_path='deployment-apps'
def test_server_deployment_path='/tmp'

pipeline {
    agent any
    
    environment {
        TEST_SERVER_CREDENTIALS = credentials('test-credentials')
     }

    stages {
            stage("Deploy config to test server"){
                steps   
                {
                    script {
                            echo "Deploying config to Test server"
                            remote.user = "${TEST_SERVER_CREDENTIALS_USR}"
                            remote.password = "${TEST_SERVER_CREDENTIALS_PSW}"
                            sshCommand remote: remote, command: "timestamp=`date +\"%T\"`; mv $test_server_deployment_path/$config_file_path $test_server_deployment_path/$config_file_path_$timestamp"
                            sshPut remote: remote, from: config_file_path, into: test_server_deployment_path, override: true

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
