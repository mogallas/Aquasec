pipeline {
    agent any
    stages {
        stage('Scan Base Image') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/mogallas/Aquasec.git'
                sh label: '', script: 'trivy client --remote http://54.144.250.10:8080 centos:8'
            }
        }
        stage('Create Docker Image') {
            steps {
                sh label: '', script: 'docker build -t thinknyx/devopsinaction:1.0 --build-arg downloadLink=http://apachemirror.wuchna.com/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz --build-arg tomcatVersion=8.5.57 .'
            }
        }
        stage('Scan App Image') {
            steps {
                sh label: '', script: 'trivy client --remote http://54.144.250.10:8080 thinknyx/devopsinaction:1.0'
            }
        }
    }
}
