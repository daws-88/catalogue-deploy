pipeline { 
    agent { 
        node { 
            label 'AGENT-1' 
        } 
    } 

    environment { 
        COURSE = "jenkins" 
        APP_VERSION = ""
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
        REGION = "us-east-1"
    } 
    options {
        timeout(time: 50, unit: 'MINUTES')
        disableConcurrentBuilds()
     }
      parameters {
        string(name: 'APP_VERSION', description: 'Which version you want to deploy?')
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: 'Pick something')
    
    }
    stages {       
        stage('depoly') { 
            steps { 
                script { 
                     withAWS(region:'us-east-1',credentials:'aws-creds') {
                        sh """
                            aws eks update-kubeconfig --region ${REGION} --name ${PROJECT}-${params.deploy_to}
                            kubectl get nodes
                        """
    
                } 
            } 
         } 
        }
    }
    
    post { 
        always {  
            echo 'I will always say Hello again!' 
            cleanWs()  
        } 

        success { 
            echo 'Run if pipeline success' 
        } 

        failure { 
            echo 'Run if pipeline failure' 
        } 
        aborted {
            echo "pipeline is aborted"
        }
    } 
}
