pipeline {
    agent any
    tools{
     maven 'My Maven'   
    }
    stages {
        stage('Source Repo') {
            steps {
                echo 'This is stage 1'
                git 'https://github.com/Yrus0105/DevOpsClassCodes_me.git'
            }
        }
        stage('Comilation') {
            steps {
                echo 'this is stage 2'
                sh 'mvn compile'
            }
        }
    
        stage('Code review') {
            steps {
                echo 'This is stage 3'
                sh 'mvn pmd:pmd'
            }
            post{
                success{
                recordIssues(tools: [pmdParser(pattern: 'target/pmd.xml')])
                }
            }
        }
    
        stage('Testing Phase') {
            steps {
                echo 'This is stage 4'
                sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }
    
        stage('Package') {
            steps {
                echo 'This is last stage'
                sh 'mvn package'
            }
        }
    }
}
