@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'eks', description: 'Branch name to clone')
        string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker image tag to update in the deployment YAML')
}

    environment {
    DEPLOYMENT_FILE = 'k8s/deployment.yaml'
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


        stage('Update Image Tag in Deployment') {
    steps {
        updateTagInDeployment(env.DEPLOYMENT_FILE, params.IMAGE_TAG)
    }
}


         stage('Set Kubeconfig') {
            steps {
                script {
                    setKubeconfig('kubeconfig-infra')
                }
            }
        }
        
    }
}
