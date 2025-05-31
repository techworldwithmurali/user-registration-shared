
#### INSTRUCTOR DETAILS

|  Information             | Details                                                                      |
|----------------------    |------------------------------------------------------------------------------|
| **Name**                 | Moole Muralidhara Reddy                                                      |
| **Email**                | techworldwithmurali@gmail.com                                                |
| **Website**              | https://www.techworldwithmurali.com               |
| **LinkedIn profile**     | [Moole Muralidhara Reddy](https://www.linkedin.com/in/moole-muralidhara-reddy) |

## **Jenkins Shared Library:  Static Code Analysis using SonarQube** 

### 📂 GitHub Repository Information

**Repository Name:** `user-registration-shared`  
**Owner:** `techworldwithmurali`  
**Repository URL:** [https://github.com/techworldwithmurali/user-registration-shared.git](https://github.com/techworldwithmurali/user-registration-shared.git)  
**Branch:** `sonarqube`

### **staticCodeAnalysis.groovy**

```groovy
def call() {
    stage('Static code analysis') {
        withSonarQubeEnv('sonarqube-token') {
            sh 'mvn sonar:sonar'
        }
    }
}

}

```

### **In Jenkinsfile**

```groovy
stage('Static Code Analysis') {
            steps {
                staticCodeAnalysis()
            }
        }
```

## 📄 Final Jenkinsfile

```groovy

```
