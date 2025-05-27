@Library('my-shared-library') _

pipeline {
    agent any
    tools {
  maven 'Maven-3.9.8'
}

    parameters {
    string(name: 'branchName', defaultValue: 'develop', description: 'Branch name to clone')
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
        
    }
}
