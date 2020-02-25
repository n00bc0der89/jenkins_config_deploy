pipeline {

    stages {
            stage("Deploy config to test server"){
                steps{
                    echo "Deploying config to Test server"
                    
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