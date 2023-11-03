pipeline{
    agent any
    tools{
        maven "Maven"
    }
    stages{
        stage('git'){
            steps{
                git credentialsId: 'git-credentials', url: 'https://github.com/rajeshvr7/judy.git'
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('file permissions'){
            steps{
                dir('/var/lib/jenkins/workspace/judy/target'){
                    sh 'chmod 700 Uber.jar'
                }
            }
        }
        stage('run jar'){
            steps{
                dir('/var/lib/jenkins/workspace/judy/target') {
                    sh 'pwd'
                    sh 'ls -l'
                    sh 'ls -l /var/lib/jenkins/workspace/judy/target' 
                    sh 'java -jar Uber.jar'
                }    
            }
        }
    }
}



AND go to application properities
