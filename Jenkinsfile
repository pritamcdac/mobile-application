pipeline {
    agent any

    environment {
        ANDROID_HOME = 'E:\\softwares\\sohampa\\AppData\\Local\\Android\\Sdk'
        PATH = "${env.ANDROID_HOME}\\platform-tools;${env.ANDROID_HOME}\\tools;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/pritamcdac/mobile-application.git'
            }
        }

        stage('Setup JDK & Gradle') {
            steps {
                bat 'java -version'  // Verify Java version (should be 17)
                bat 'gradlew.bat --version'  // Verify Gradle
            }
        }


        stage('Build APK') {
            steps {
                bat 'gradlew.bat :app:assembleDebug --stacktrace'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'gradlew.bat :app:test'
            }
        }

        stage('Upload APK') {
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/apk/debug/*.apk', fingerprint: true
            }
        }
    }
}
