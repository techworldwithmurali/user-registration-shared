@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'helm-eks', description: 'Branch name to clone')
        choice(name: 'ENVIRONMENT', choices: ['dev','test','qa','uat','preprod',infra,'prod'], description: 'Target environment')
        string(name: 'RELEASE_NAME', defaultValue: 'user-registration', description: 'Helm release name')
        string(name: 'NAMESPACE', defaultValue: 'user-managment', description: 'Kubernetes namespace')
        string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker image tag')	
        
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

        stage('Install Kubectl') {
    steps {
        installKubectl()
    }
}


 stage('Set Kubeconfig') {
    steps {
        setKubeconfig('kubeconfig-infra')
    }
}

stage('Helm Deploy') {
    steps {
            helmDeploy(
               "kubeconfig-infra",
                params.ENVIRONMENT,
                params.RELEASE_NAME,
                params.NAMESPACE,
                params.IMAGE_TAG
            )
       
    }
}
        
        
    }
}
