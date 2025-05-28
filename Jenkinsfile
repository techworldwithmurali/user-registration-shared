@Library('my-shared-library') _

pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}

        environment {
        IMAGE_TAG = "${GIT_COMMIT.substring(0, 6)}"
    }

    
    parameters {
    string(name: 'branchName', defaultValue: 'aws-ecr', description: 'Branch name to clone')
    string(name: 'ecrRepoName', defaultValue: 'user-registration', description: 'ecrRepoName')
    string(name: 'accountNumber', defaultValue: '361769595507', description: 'accountNumber')
    choice(name: 'region', choices: ['us-east-1','us-west-2'], description: 'Select AWS region')

}
    
    stages {
        stage('Clone the repository') {
            steps {
                gitClone(params.branchName, 'github-cred', 'https://github.com/techworldwithmurali/user-registration-shared.git')
            }
        }


         stage('Build the code') {
            steps {
                buildCode()
            }
        }

stage('Build and Tag Docker Image') {
    steps {
        script {
        //    dockerBuildforECR('361769595507', 'us-east-1', 'user-registration', IMAGE_TAG)

            
dockerBuildforECR(params.accountNumber, params.region, params.ecrRepoName, IMAGE_TAG)
            
        }
    }
}


stage('Push to ECR') {
    steps {
        script {
            dockerImagePushToECR(params.accountNumber, params.region, params.ecrRepoName, IMAGE_TAG)
        }
    }
}
        

    }

}
