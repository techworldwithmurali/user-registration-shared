@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'helm', description: 'Branch name to clone')
        string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker image tag to update in the deployment YAML')
        choice(name: 'ENVIRONMENT', choices: ['dev','test','qa','uat','preprod','prod'], description: 'Target environment')
        string(name: 'RELEASE_NAME', defaultValue: 'user-registration', description: 'Helm release name')
        string(name: 'NAMESPACE', defaultValue: 'user-managment', description: 'Kubernetes namespace')	
        
}
    stages {
        stage('Clone the repository') {
            steps {
                gitClone(params.branchName, 'github-cred', 'https://github.com/techworldwithmurali/user-registration-shared.git')
            }
        }

stage('Install Helm3') {
    steps {
        installHelm()
        // installHelm('v3.14.0') for a specific version
    }
}
 

     stage('Set Kubeconfig') {
            steps {
                withCredentials([file(credentialsId: "kubeconfig-infra", variable: 'KUBECONFIG')]) {
                    sh '''
                        kubectl config get-contexts
                        kubectl get nodes
                    '''
                }
            }
        }


    stage('Helm Deploy') {
    steps {
        helmDeploy(
            params.ENVIRONMENT,
            params.RELEASE_NAME,
            params.NAMESPACE,
            params.IMAGE_TAG
        )
    }
}

        
    }
}
