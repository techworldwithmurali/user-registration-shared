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
            dockerBuildforECR('361769595507', 'us-east-1', 'user-registration', IMAGE_TAG)
        }
    }
}
        

    }

}
