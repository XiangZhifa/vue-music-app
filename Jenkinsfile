pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'cd73afdc-8995-4b76-ac2d-610d9f267e60', url: 'https://github.com/XiangZhifa/vue-music-mobile.git']]])
            }
        }
        stage('build project') {
            steps {
                sh 'rm -rf /var/lib/jenkins/workspace/vue-music-mobile-pipeline/dist'
                sh 'cd /var/lib/jenkins/workspace/vue-music-mobile-pipeline'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('publish project') {
            steps {
                sh 'rm -rf /opt/tomcat/apache-tomcat-8.5.65/webapps/vue-music-mobile/*'
                sh 'mv /var/lib/jenkins/workspace/vue-music-mobile-pipeline/dist/* /opt/tomcat/apache-tomcat-8.5.65/webapps/vue-music-mobile'
            }
        }
    }
}
