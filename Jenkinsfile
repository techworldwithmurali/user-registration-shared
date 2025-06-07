@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'helm-eks', description: 'Branch name to clone')
        
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
        
    }
}
