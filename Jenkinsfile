pipeline {
    agent { label 'MAVEN' }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/Nikhita-A/spring-petclinic.git',
                    branch: 'dev'
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
                failure {
                    mail subject: 'build stage failed',
                         from: 'devops@gmail.com',
                         to: 'dev@gmail.com',
                         body: 'Refer to $BUILD_URL for more info'
                }
            }
        }
    }
}