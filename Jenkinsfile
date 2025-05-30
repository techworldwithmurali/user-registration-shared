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
    string(name: 'branchName', defaultValue: 'dockerhub', description: 'Branch name to clone')
        string(name: 'dockerHubRepoName', defaultValue: 'user-registration', description: 'dockerHubRepoName')
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
            dockerBuildForDockerHub('mmreddy424', params.dockerHubRepoName , IMAGE_TAG)
        }
    }
}

        stage('Push to DockerHub') {
    steps {
        script {
            dockerImagePushToDockerHub('mmreddy424', params.dockerHubRepoName, IMAGE_TAG)
        }
    }
}
        
    }
}
