pipeline {
    agent any

    stages {
        stage('Clone the repository') {
            steps {
                gitClone('develop', 'github-cred', 'https://github.com/techworldwithmurali/user-registration-shared.git')
            }
        }
        
    }
}
