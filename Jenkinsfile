pipeline {
    agent {
        label 'slave1'
    }
    environment{
        SONAR_TOKEN = '9fa3df25f98ade234a3581f3291de083c161ee60'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
//         stage('Sonar-Report') {
//             steps {
//             sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=jenkins_project \
//   -Dsonar.host.url=http://localhost:9000 \
//   -Dsonar.login=5f09ded7e5db4d0ea0dcfd937c181af706e60475'
//             }
//         }
        stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
        stage('Sonar-Report') {
            steps {
               // bat 'mvn clean install sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.analysis.mode=publish'
               bat 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=nazgul19_webapp'
            }
        }
    }
}
