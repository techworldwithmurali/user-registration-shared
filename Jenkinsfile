@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
    string(name: 'branchName', defaultValue: 'eks', description: 'Branch name to clone')
 choice(name: 'region', choices: ['us-east-1','us-west-2'], description: 'Select AWS region')
        choice(name: 'clusterName', choices: [ 'infra-cluster', 'dev-cluster', 'test-cluster',
            'qa-cluster', 'uat-cluster', 'pre-prod-cluster', 'prod-cluster'  ], description: 'Select cluster name')

        string(name: 'IMAGE_TAG', defaultValue: '', description: 'Docker image tag to update in the deployment YAML')
        
}
    environment {
    DEPLOYMENT_FILE = 'k8s/deployment.yaml'
        YAML_DIR = 'k8s/'
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

stage('Update Image Tag in Deployment') {
    steps {
        updateTagInDeployment(env.DEPLOYMENT_FILE, params.IMAGE_TAG)
    }
}


        stage('Apply Kubernetes YAMLs') {
    steps {
        applyK8sYaml(YAML_DIR)
    }
}
        
    }
}
