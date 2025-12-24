pipeline {
    agent any
    environment { MAVEN_OPTS = "-Xmx300m" }
    stages {
        stage('Build') {
            steps { sh 'mvn package -DskipTests' }
        }
        stage('Deploy') {
            steps {
                sh 'sudo cp target/typing-game.war /opt/tomcat9/webapps/'
                sh 'sudo touch /opt/tomcat9/webapps/typing-game.war'
            }
        }
    }
}
