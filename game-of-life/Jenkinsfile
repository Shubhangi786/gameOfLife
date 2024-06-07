pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Shubhangi786/gameOfLife.git']])
                
            }
        }
        stage('Build'){
            steps {
                dir('\\game-of-life') {
                        bat 'mvn package'
                    }
            }
        }
        
        stage('Archiving war....'){
            steps{
                archiveArtifacts artifacts: '\\game-of-life\\gameoflife-web\\target\\*.war', followSymlinks: false
            }
        }
        
        stage('Deploying to localhost address - http://192.168.0.154:9999'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcatLogin', path: '', url: 'http://192.168.0.154:9999')], contextPath: 'gof', war: '**/*.war'
            }
        }
    }
}
