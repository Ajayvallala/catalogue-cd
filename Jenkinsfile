pipeline{
    agent{
        label 'AGENT-1'
    }
    options {
        ansiColor('xterm')
    }
    parameters{
        string(name: 'appVersion', defaultValue: '', description: 'Please enter Image version')
        choice(name: 'deploy', choices: ['dev', 'qa', 'prod'], description: 'Pick Environment')

    }
    stages{
        stage('Deploy'){
            steps{
                withAWS(credentials: 'aws-creds', region: 'us-east-1'){
                 script{
                    sh """
                    aws eks update-kubeconfig --name roboshop-dev --region us-east-1
                    sed -i "s/IMAGEVERSION/${params.appVersion}/g" values.yaml
                    helm upgrade --install nginx -f values.yaml
                    """
                  }
                }
               
            }
        }
    }
}