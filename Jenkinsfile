pipeline {
    agent any

    tools {
        maven "maven3"
    }

    stages {
        stage('SCM checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ArjunSwarnaDwijanand/springsecurity-demo.git']])
            }
        }
        stage('Build Process'){
            steps{
                script{
                    sh 'mvn clean install'
                }
            }
        }
        stage('Deploy to Container'){
            steps{
               deploy adapters: [tomcat9(credentialsId: '4c68b31f-663e-4fea-af8c-9e5c994bd335', path: '', url: 'http://localhost:5051/')], contextPath: 'springsecurity-demo', war: '**/*.war'
            }
        }
    }

    post{
        always{
            emailext attachLog: true,
            body: '''<html>
                        <body>
                           <p>Build Status :  ${BUILD_STATUS} </p>
                           <p>Build Number:  ${BUILD_NUMBER}</p>
                           <p>Check the <a href="${BUILD_URL}">console output</a>.</p>
                        </body>
                      </html>''',
            mimeType: 'text/html',
            replyTo: 'nagarjuna.anke3@gmail.com',
            subject: 'Pipeline Status: ${BUILD_NUMBER}',
            to: 'nagarjuna.anke3@gmail.com'
        }
    }
}

//SCM checkout
//build
//deploy WAR
//Email
