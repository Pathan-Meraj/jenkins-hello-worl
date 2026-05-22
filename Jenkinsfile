pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK21'
    }

    stages {

        stage('Maven Version') {
            steps {
                bat 'echo Print Maven Version'
                bat 'mvn -version'
            }
        }

        stage('Build') {
            steps {

                git branch: 'main',
                url: 'https://github.com/Pathan-Meraj/jenkins-hello-worl.git'

                bat 'mvn clean package -DskipTests=true'

                archiveArtifacts 'target/hello-demo-*.jar'
            }
        }

        stage('Test') {
            steps {

                bat 'mvn clean test'

                junit(
                    testResults: 'target/surefire-reports/TEST-*.xml',
                    keepProperties: true,
                    keepTestNames: true
                )
            }
        }
    }

    post {

        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
