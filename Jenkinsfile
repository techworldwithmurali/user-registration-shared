@Library('my-shared-library') _

pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}

    parameters {
    string(name: 'branchName', defaultValue: 'aws-ecr', description: 'Branch name to clone')
        
    string(name: 'ecrRepoName', defaultValue: 'user-registration', description: 'ecrRepoName')
    string(name: 'accountNumber', defaultValue: '361769595507', description: 'accountNumber')
    choice(name: 'region', choices: ['us-east-1','us-west-2'], description: 'Select AWS region')
}

stage('Build and Tag Docker Image') {
    steps {
        script {
            dockerBuild(params.accountNumber, params.region, params.ecrRepoName)
        }
    }
}
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
          //   dockerBuild('361769595507', 'us-east-1', 'user-registration')
            dockerBuild(params.accountNumber, params.region, params.ecrRepoName)
            
        }
    }
}
        
    }
}

