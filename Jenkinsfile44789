pipeline {
    agent any
    
    tools{
        maven 'mymaven'
    }

    stages {
        stage('CloneRepo') {
            steps {
                echo 'This is stage 1'
                git 'https://github.com/NikitasGithub/DevOpsClassCodes.git'
            }
        }
        stage('Compile Stage') {
            steps {
                echo 'This is stage 2'
                sh 'mvn compile'
            }
            
        }
        stage('Code review Stage') {
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
        stage('Code testing Stage') {
            steps {
                echo 'This is stage 4'
                sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/*.xml'
                }
            }
            
        }
        stage('Code package Stage') {
            steps {
                echo 'This is stage 5'
                sh 'mvn package'
            }
            
            
        }
    }
}
