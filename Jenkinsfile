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
                bat 'java -version'  // Verify Java version (should be 17)
                bat 'gradlew.bat --version'  // Verify Gradle version
            }
        }

        stage('Build APK') {
            steps {
                bat 'gradlew.bat assembleDebug'  // Use Windows format
            }
        }

        stage('Run Tests') {
            steps {
                bat 'gradlew.bat test'
            }
        }

        stage('Upload APK') {
            steps {
                archiveArtifacts artifacts: 'app\\build\\outputs\\apk\\debug\\*.apk', fingerprint: true
            }
        }
    }
}
