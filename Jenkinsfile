pipeline {
    agent any

    environment {
        // Prevents t2.micro from running out of memory during compilation
        MAVEN_OPTS = "-Xmx300m"
    }

    stages {
        stage('Checkout') {
            steps {
                // Jenkins automatically pulls the code if you set up "Pipeline from SCM"
                // But this confirms the version being used
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the WAR file with Maven...'
                // -DskipTests speeds up the process for initial setup
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Apache Tomcat...'
                // 1. Copy the WAR file to the webapps directory
                // 2. Use 'touch' to ensure Tomcat notices the timestamp change and redeploys
                sh 'sudo cp target/typing-game.war /opt/tomcat9/webapps/'
                sh 'sudo touch /opt/tomcat9/webapps/typing-game.war'
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
            echo 'Access your game at http://16.170.255.143:8081/typing-game/'
        }
        failure {
            echo 'The build failed. Please check the Console Output for errors.'
        }
    }
}
