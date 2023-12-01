pipeline {
    agent { label 'MAVEN' }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        cron('30 14 * * *')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/Nikhita-A/spring-petclinic.git',
                    branch: 'release'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                    junit testResults: '**/TEST-*.xml'
                }
            }
        }
    }
}