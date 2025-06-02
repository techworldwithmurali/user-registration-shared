@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'eks', description: 'Branch name to clone')
 choice(name: 'region', choices: ['us-east-1','us-west-2'], description: 'Select AWS region')
        choice(name: 'clusterName', choices: [ 'infra-cluster', 'dev-cluster', 'test-cluster',
            'qa-cluster', 'uat-cluster', 'pre-prod-cluster', 'prod-cluster'  ], description: 'Select cluster name')
        
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
        
stage('Connect to EKS') {
    steps {
        connectToEks(params.clusterName, params.region)
    }
}

        
    }
}
