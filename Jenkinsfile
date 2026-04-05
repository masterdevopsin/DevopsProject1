pipeline {
    agent any
    
    tools{
        maven 'mymaven'
    }

    stages {
        stage('CloneRepo') {
            steps {
                echo 'cloning the repo'
                git 'https://github.com/masterdevopsin/DevopsProject1.git'
            }
        }
         stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('CodeReview') {
            steps {
                sh 'mvn pmd:pmd'
            }
            post{
                    success{
                        recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                    }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post{
                    success{
                        junit 'target/surefire-reports/*.xml'
                    }
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
