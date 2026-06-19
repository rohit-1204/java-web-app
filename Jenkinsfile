pipeline {
    agent any

    triggers { 
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('checkout') {
            steps {
                git branch:"master",
                url:"https://github.com/rohit-1204/java-web-app.git"
            }
        }

        stage('Installing Maven ') {
            steps {
                sh 'sudo apt update'
                sh 'sudo apt install maven -y'
                sh 'mvn -version'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Installing Tomcat') {
            steps {
                sh 'sudo apt update'
                sh 'sudo apt install tomcat9 -y'
                sh 'sudo systemctl start tomcat9'
                sh 'sudo systemctl enable tomcat9'

            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo cp target/java-web-app-1.0-SNAPSHOT.war /var/lib/tomcat9/webapps/'
            }

        }
        stage('Testing') {
            steps {
                sh 'curl http://localhost:8080/java-web-app-1.0-SNAPSHOT/'
            }
        }   
    }
}
