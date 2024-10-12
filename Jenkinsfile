pipeline {
    agent any
    stages {
        stage('checkout'){
            steps{
                script{
                    git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mpr399/https://github.com/mpr399/CWMS-Project-using-PHP.git'
                }
            }
        }
        stage('build'){
            steps{
                script{
                    sh 'cd $HOME/workspace/cwms/app && docker build -t mvpar/cwmsapp .'
                    sh 'cd $HOME/workspace/cwms/db && docker build -t mvpar/cwmsdb .'
                }
            }
        }
        stage('push'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'REGISTRY_PWD', usernameVariable: 'REGISTRY_USER')]) {
                        sh 'docker login -u=$REGISTRY_USER -p=$REGISTRY_PWD'    
                        sh 'docker push mvpar/cwmsapp'
                        sh 'docker push mvpar/cwmsdb'
                    }    
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                     sh "cd $HOME/workspace/cwms && docker-compose down && docker-compose up -d"
                }
            }
        }
    }
}