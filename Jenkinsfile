pipeline {
    agent any
    tools {
        maven 'Maven 3.8.1' // Ensure this matches the name configured in the Global Tool Configuration
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/subha4256/java-hello-world-webapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'your-server',
                        transfers: [
                            sshTransfer(
                                sourceFiles: 'target/yourapp.war',
                                removePrefix: 'target',
                                remoteDirectory: '/opt/apache-tomcat-9.0.65/webapps',
                                execCommand: 'sudo systemctl restart tomcat'
                            )
                        ]
                    )
                ])
            }
        }
    }
}

