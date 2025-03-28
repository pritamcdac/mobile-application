pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/pritamcdac/mobile-application.git'
            }
        }

        stage('Setup JDK & Gradle') {
            steps {
                sh 'java -version'  // Verify Java version (should be 17)
                sh 'chmod +x gradlew'  // Ensure Gradle wrapper is executable
            }
        }

        stage('Build APK') {
            steps {
                sh './gradlew assembleDebug'
            }
        }

        stage('Run Tests') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Upload APK') {
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/apk/debug/*.apk', fingerprint: true
            }
        }
    }
}
