@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'eks', description: 'Branch name to clone')
}

    stages {
        stage('Clone the repository') {
            steps {
                gitClone(params.branchName, 'github-cred', 'https://github.com/techworldwithmurali/user-registration-shared.git')
            }
        }

stage('Install Kubectl') {
    steps {
        installKubectl()
    }
}
        
        
    }
}
