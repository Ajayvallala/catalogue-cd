pipeline{
    agent{
        label 'AGENT-1'
    }
    options {
        ansiColor('xterm')
    }
    parameters{
        string(name: 'Imageversion', defaultValue: '', description: 'Please enter Image version')
        choice(name: 'Deploy', choices: ['dev', 'qa', 'prod'], description: 'Pick Environment')

    }
    stages{
        stage('Deploy'){
            steps{
                withAWS(credentials: 'aws-creds', region: 'us-east-1'){
                 script{
                    sh """
                    aws eks update-kubeconfig --name roboshop-dev --region us-east-1
                    kubectl get nodes
                    """
                  }
                }
               
            }
        }
    }
}